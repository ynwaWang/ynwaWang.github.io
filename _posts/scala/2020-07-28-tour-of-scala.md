---
layout: post
title: “tour of scala"
subtitle: "scala学习"
date: 2020-07-28
author: David
category: scala
tags: learn
finished: false
---



## 模式匹配

### 语法

```scala
x match {
	case 0 => "zero"
  case _ => "other"
}
```

### 用法

#### 案例类（case classes）的匹配

```scala
abstarct class Notification 
case class Email(sender:String,title:String,body:String) extends Notification
case class SMS(sender:String,message:String) extends Notification
case class VoiceRecording(contactName:String,link:String) extends Notification

def showNotification(notification: Notification): String = {
  notification match {
    case Email(sender,title,_) => 
      s"You got an email from $sender with title $title"
    case SMS(number,message) => 
      s"You got a SMS from $number!Message:$message"
    case VoiceRecording(name,link) => 
      s"You received a Void Recording from $name!Click the link to hear it:$link"
  }
}
```

#### 模式守卫（Pattern gaurds）

```scala
// 为了让匹配更加具体，可以使用模式守卫，也就是在模式后面加上if <boolean expression>
def showImportantNotification(notification: Notification, importantPeopleInfo: Seq[String]): String = {
  notification match {
    case Email(sender, _, _) if importantPeopleInfo.contains(sender) =>
      "You got an email from special someone!"
    case SMS(number, _) if importantPeopleInfo.contains(number) =>
      "You got an SMS from special someone!"
    case other =>
      showNotification(other) // nothing special, delegate to our original showNotification function
  }
}
```

#### 仅匹配类型

```scala
def showNotification(notification: Notification): String = {
  notification match {
    case e : Email => 
      s"You got an email"
    case s : SMS => 
      s"You got a SMS"
    case v : VoiceRecording => 
      s"You received a Void Recording"
  }
}
```

#### 密封类

特质（trait）和类（class）可以用`sealed`标记为密封的，这意味着其所有子类都必须与之定义在相同文件中，从而保证所有子类型都是已知的。

```scala
sealed abstract class Furniture
case class Couch() extends Furniture
case class Chair() extends Furniture

def findPlaceToSit(piece: Furniture): String = piece match {
  case a: Couch => "Lie on the couch"
  case b: Chair => "Sit on the chair"
}
```

这对于模式匹配很有用，因为我们不再需要一个匹配其他任意情况的`case`。