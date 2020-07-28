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

## 特质

Traits用于在类（Class）之间共享程序接口（Interface）和字段（Fields）。它们类似于Java 8的接口。 类和对象 (Objects)可以扩展特质，但是特质不能被实例化，因此特质没有参数。

## 案例类

### 定义

一个最简单的案例类定义由关键字`case class`，类名，参数列表（可为空）组成：

```scala
case class Book(isbn: String)

val frankenstein = Book("978-0486282114")
```

注意在实例化案例类`Book`时，并没有使用关键字`new`，这是因为案例类有一个默认的`apply`方法来负责对象的创建。

当你创建包含参数的案例类时，这些参数是公开（public）的`val`

### 比较

案例类在比较的时候是按值比较而非按引用比较：

```scala
case class Message(sender: String, recipient: String, body: String)

val message2 = Message("jorge@catalonia.es", "guillaume@quebec.ca", "Com va?")
val message3 = Message("jorge@catalonia.es", "guillaume@quebec.ca", "Com va?")
val messagesAreTheSame = message2 == message3  // true
```

### 拷贝

你可以通过`copy`方法创建一个案例类实例的浅拷贝，同时可以指定构造参数来做一些改变。

```scala
case class Message(sender: String, recipient: String, body: String)
val message4 = Message("julien@bretagne.fr", "travis@washington.us", "Me zo o komz gant ma amezeg")
val message5 = message4.copy(sender = message4.recipient, recipient = "claire@bourgogne.fr")
message5.sender  // travis@washington.us
message5.recipient // claire@bourgogne.fr
message5.body  // "Me zo o komz gant ma amezeg"
```

上述代码指定`message4`的`recipient`作为`message5`的`sender`，指定`message5`的`recipient`为”claire@bourgogne.fr”，而`message4`的`body`则是直接拷贝作为`message5`的`body`了。




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