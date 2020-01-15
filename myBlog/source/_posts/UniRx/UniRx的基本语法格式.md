---
title: #5 UniRx的基本语法格式
top: false
cover: false
toc: true
mathjax: true
date: 2019-01-15 16:39:54
password:
summary:
tags: Unity3D
categories: UniRx
---

先来看一下之前的一段代码：

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UniRx;
using System;

namespace UniRxLessons
{
    public class UniRxTimerExample : MonoBehaviour
    {
        // Start is called before the first frame update
        void Start()
        {
            Observable.Timer(TimeSpan.FromSeconds(5.0f))
                .Subscribe(_ =>
                {
                    Debug.Log("UniRxTimer");
                })
                .AddTo(this);
        }
    }
}
```

**⭐Observable.XXX().Subscrible()**时非常典型的UniRx格式。

只要理解什么意思就可以看懂大部分的UniRx的用法了。

## 首先解决词汇问题吧：

1. Observable: 可观察的，是boss，大老板。
2. Timer: 定时器，干活的小工，Observable就是盯着Timer干活的，使唤Timer做事儿。
3. Subscribe: 订阅，他是监工，监谁呢？就是前面的Timer，如果Timer要做的事儿做完了，监工就开始汇报他的监督工作。

前面说的什么Obervable和Subscribe其实并不是UniRx的侧重点，说这两个只是为了便于理解**事件从发布者到订阅者**之间的过程如何处理。

所以两个点不重要，重要的是两点之间的线，也就是事件的传递过程。