---
layout: page
title: “学习笔记-hive"
date: 2020-05-31
author: ynwa
category: up
tags: stars,hive
finished: false
---



# 记一次SQL问题排查

```sql
explain
with 
t0 as (
  select model_code
        ,count(distinct case when inventory_status in (201,103,102) and sample_car_order_match_status<>2 and is_can_sale=1 then purchase_bill_item_id else null end) as can_sale_car
        ,count(distinct case when sample_car_order_match_status=2 and inventory_status not in (109,104,108,207,204,205,206) then purchase_bill_item_id else null end) as locked_sample_car_can_sale
        ,count(distinct case when inventory_status in (109,104,108,207,204,205,206) and  (inventory_status in (103,102,105,201,202,203) and sample_car_order_match_status<>2  and is_can_sale=0) then purchase_bill_item_id else null end) as to_be_delivered_car
      from edw_scm.dwb_gds_ety_scmf_inventory_dd
      where ds='2021-02-03' and purchase_refund = 0 and purchase_changed = 0 
      group by model_code
)
,t7 as (
	select a.brand_name,a.model_code,a.model_name
  from (
    select brand_name,model_code,model_name
    ,row_number() over (partition by model_code order by  brand_name desc ) num
    from edw_scm.dwb_gds_ety_scmf_inventory_dd
    where ds='2021-02-03' and purchase_refund = 0 and purchase_changed = 0 
  ) a where a.num = 1
  group by brand_name,model_code,model_name
)
,t4 as (
	select a.model_code
    	,count(distinct case when a.order_type =1 and datediff('2021-02-03',a.prepaid_date)<7 then a.order_id else null end) as fullpay_last_7_days_order_num
    	,count(distinct case when a.order_type in(2,4) and datediff('2021-02-03',a.prepaid_date)<7 then a.order_id else null end) as partpay_last_7_days_order_num
    	,count(distinct case when a.order_type in(3,5) and datediff('2021-02-03',a.prepaid_date)<7 then a.order_id else null end) as rent_last_7_days_order_num

    	,count(distinct case when a.order_type =1 and substring(a.prepaid_date,1,7)=substring('2021-02-03',1,7) then a.order_id else null end ) as fullpay_last_month_order_num
    	,count(distinct case when a.order_type in(2,4) and substring(a.prepaid_date,1,7)=substring('2021-02-03',1,7) then a.order_id else null end ) as partpay_last_month_order_num
    	,count(distinct case when a.order_type in(3,5) and substring(a.prepaid_date,1,7)=substring('2021-02-03',1,7) then a.order_id else null end ) as rent_last_month_order_num
    from (
        select order_id,order_type,brand_name,model_code,model_name,prepaid_date
            ,case when substring(prepaid_date,1,7)=substring('2021-02-03',1,7) or datediff('2021-02-03',prepaid_date)<7  then 1 else 0 end as label --对当月和近七天的销量数据进行打标
        from dm_tgc.bm_evt_trd_full_order_info_dd
        where ds='2021-02-03' and prepaid_date is not null
            and order_status_code not in (1000,7000,8000)  -- 不含退单
    ) a where a.label = 1
    group by a.model_code
)


,ttt as (
  select t0.model_code,t7.brand_name,t7.model_name -- ,t4.model_code
  from t0 
  left join t7 on t0.model_code = t7.model_code
)

select 
t0.model_code,t0.brand_name,t0.model_name,t4.model_code
from ttt t0 
left join t4 on t0.model_code = t4.model_code
```

### 问题描述

| 场景                        | count(model_code) | count(brand_name) |
| --------------------------- | ----------------- | ----------------- |
| 1：t0 join t7               | 1243              | 1211              |
| 2：t0 join t7 join t4       | 1243              | 1075              |
| 3：(t0 join t7) ttt join t4 | 1243              | 1211              |

### 排查思路

1. 查看执行计划：执行计划都是merge join，join的核心问题在于key的分布

2. 执行计划的差异在于：string作为key  <em>VS</em> UDFToDouble

   ```json
   keys:{"0":"_col0 (type: string)","1":"_col1 (type: string)","2":"_col0 (type: string)","3":"_col0 (type: string)","4":"_col0 (type: string)","5":"_col0 (type: string)","6":"_col0 (type: string)"}
   
   keys:{"0":"UDFToDouble(_col0) (type: double)","1":"UDFToDouble(_col1) (type: double)","2":"UDFToDouble(_col0) (type: double)","3":"UDFToDouble(_col0) (type: double)","4":"UDFToDouble(_col0) (type: double)","5":"UDFToDouble(_col0) (type: double)","6":"UDFToDouble(_col0) (type: double)","7":"UDFToDouble(_col0) (type: double)"}
   ```

3. 验证：t4中的cast(model_code as string)处理后再执行场景2，结果正常



### 参考

+ [Hive map阶段缓慢，优化过程详细分析](https://developer.aliyun.com/article/181138)，也反映了类型不一致会导致的问题

+ 查看数据(9991-n)，无法匹配 -> 查看UDFToDouble源码 -> null != null ,导致key值无法匹配

  ```java
  try {
    doubleWritable.set(Double.valueOf(i.toString()));
    return doubleWritable;
  } catch (NumberFormatException e) {
    // MySQL returns 0 if the string is not a well-formed double value.
    // But we decided to return NULL instead, which is more conservative.
    return null;
  }
  ```

  

  