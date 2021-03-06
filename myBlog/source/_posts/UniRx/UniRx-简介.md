---
title: #1 UniRx 简介
top: false
cover: false
toc: true
mathjax: true
date: 2019-01-15 11:32:18
password:
summary:
tags:Unity3D
categories:UniRx
---

> UniRx是一个Unity3D的**编程框架**。—— <u>***专注于解决异步逻辑，使得异步逻辑更加优雅简洁。***</u>

## **UniRx的简洁优雅是如何体现的呢？**

- 比如，实现一个 <u>只处理第一次鼠标点击事件</u> 的功能，使用UniRx实现如下：

  ```csharp
  Observable.EveryUpdate()
      .where(_=>Input.GetMouseButtonUp(0))
      .First()
      .Subscribe(_=>{
          Debug.Log("mouse clicked!")
      });
  ```

当然，上述的功能也可以用Unity自带的Update()来做，但是如果用Update()的话，意味着除了实现鼠标事件监听这个功能之外，还要实现其他功能。那么Update里就会充斥着大量的状态判断等逻辑，使代码非常不容易阅读。而用UniRx就很好地解决了这个问题，下面我们就来看一下，这几行代码都做了什么：

1. 开启一个Update的事件监听。
2. 每次Update事件被调用时，进行一个鼠标是否抬起的判断。
3. 如果判断通过，则进行计数，并且只获取第一次的点击的事件。
4. 订阅 / 处理事件。

UniRx的强大当然不仅仅如此，它还可以：

- 优雅地实现MVP(MVC)架构模式。
- 对UGUI/Unity API提供了增强，很多需要写大量代码的UI逻辑，使用UniRx优雅实现。
- 轻松实现非常复杂的异步任务处理。

**最最重要的还是，它可以大大提升我们的编码效率。**

## **为什么要用UniRx?**

还用说吗!?当然是因为牛掰呀！  ← 这句是废话。。。

UniRx就是 **Unity Reactive Extensions** 。是Unity版本的Reactive Extensions。

Reactive Extensions 的擅长部分是**处理时间上异步的逻辑**。

游戏中的很多系统都是在**时间上**异步的。这也是为什么Unity官方提供了Coroutine这样的概念。详细点说的话，比如 **动画的播放**、**声音的播放**、**网络请求**、**资源加载/卸载**、Tween、场景过渡等等。

在进行上述的各种逻辑实现的时候常常会用到大量的回调，最终项目的扩张会导致传说中的“回调地狱”。**相对较好的方法则是使用消息/事件的发送，但是结果会导致 <u>消息漫天发</u>**，导致代码非常难以阅读。

虽然使用Coroutine也是非常不错的，但是，Coroutine本身的定义**是以一个方法的格式定义的**，写起来是非常**面向过程**的，当逻辑**稍微复杂一点**，就很容易造成**Coroutine嵌套Coroutine**，代码是非常不容易阅读的**（强耦合）**。

而UniRx**介于回调和事件之间**。

它有事件的概念，但是，**他的事件是像水流一样流过来的，我们要做的则是简单地进行组织、变换、过滤、合并。**

UniRx也用到了回调，只不过事件组织之后，只要简单一个回调就可以处理事情了。它的原理和Coroutine(迭代器模式)非常类似，但比Coroutine强大。

> **UniRx将（时间上）的异步事件转换为（响应式）的事件序列，通过LINQ操作可以简单地组合起来，还支持时间操作。**

⭐使用UniRx可以节省我们的时间，同时让代码更加简洁易读。

*注：**Rx**只是一套语言上的标准，在其他语言中也有实现，如：RxJava, Rx.cpp, SwiftRx 等等。