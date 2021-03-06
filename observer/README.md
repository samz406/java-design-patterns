---
布局: 设计模式
设计类型: 观察者模式
folder: observer
permalink: /patterns/observer/
设计模式类型: 行为型模式
tags:
 - Java
 - Difficulty-Beginner
 - Gang Of Four
 - Reactive
---

## 别名
关联, 发布-订阅

## 目的
Define a one-to-many dependency between objects so that when one
object changes state, all its dependents are notified and updated
automatically.

![alt text](./etc/observer_1.png "Observer")

## 适用范围
Use the Observer pattern in any of the following situations

* when an abstraction has two aspects, one dependent on the other. Encapsulating these aspects in separate objects lets you vary and reuse them independently
* when a change to one object requires changing others, and you don't know how many objects need to be changed
* when an object should be able to notify other objects without making assumptions about who these objects are. In other words, you don't want these objects tightly coupled

## 典型使用方式

* changing in one object leads to a change in other objects

## 实际使用列子

* [java.util.Observer](http://docs.oracle.com/javase/8/docs/api/java/util/Observer.html)
* [java.util.EventListener](http://docs.oracle.com/javase/8/docs/api/java/util/EventListener.html)
* [javax.servlet.http.HttpSessionBindingListener](http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpSessionBindingListener.html)
* [RxJava](https://github.com/ReactiveX/RxJava)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Java Generics and Collections](http://www.amazon.com/Java-Generics-Collections-Maurice-Naftalin/dp/0596527756/)
