---
title: #3 独立的Update
top: false
cover: false
toc: true
mathjax: true
date: 2019-01-15 15:25:13
password:
summary:
tags: Unity3D
categories: UniRx
---

之前说过，如果在Update里面掺杂大量无关的逻辑和判断，会导致代码非常不容易阅读，这种情况还是比较常见的，比如：

```csharp
private void Update(){
    if(A){
        ...
    }
    
    if(B){
        ...
    }
}
```

一个不好的示例：

```csharp
void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Debug.Log("left mouseBtn clicked");
        }        

        if (Input.GetMouseButtonUp(0))
        {
            Debug.Log("left mouseBtn released");
        }
    }
```

如果用UniRx去做的话：

```csharp
void Start()
        {
            Observable.EveryUpdate()
                .Subscribe(_ =>
                {
                    if (Input.GetMouseButtonDown(0))
                        Debug.Log("mouse button down");
                    if (Input.GetMouseButtonUp(0))
                        Debug.Log("mouse button up");
                });
        }
```

