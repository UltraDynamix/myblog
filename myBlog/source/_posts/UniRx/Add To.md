---
title: #4 Add To
top: false
cover: false
toc: true
mathjax: true
date: 2019-01-15 11:32:18
password:
summary:
tags: Unity3D
categories: UniRx
---

> AddTo API就是字面意思——**添加到**。添加到Unity的GameObject或者MonoBehaviour

## 为什么要添加到GameObject或者MonoBehaviour呢？

因为GameObject和MonoBehaviour可以获取到 **OnDestroy** 事件，也就是GameObject或者MonoBehaviour的销毁事件。

## 那么用这个销毁事件干嘛呢？

用来进行与UniRx进行销毁事件的绑定，也就是当GameObject或者MonoBehaviour被销毁时，同样去销毁正在进行的UniRx任务。

这就是AddTo API的作用。

其实用起来很简单，代码如下：

```csharp
Observable.Timer(TimeSpan.FromSeconds(1.0f))
    .Subscribe()
    .AddTo(this); // Or gameObject
```

这样的话，当this所在的gameObject销毁时，这个Timer就会被销毁。

## 为什么会这样？

本质上，AddTo 是一个静态扩展关键字，他对 IDisposable进行了扩展。只要任何实现了IDisposable的接口，都可以使用AddTo API，不管是不是UniRx的API。当GameObject销毁时，就会调用IDisposable的OnDispose这个方法。

## AddTo能做什么呢？

有了它，在开启 Observable.EveryUpdate 时调用当前脚本的方法，则不会造成引用异常等错误，它使得UniRx的使用更加安全。