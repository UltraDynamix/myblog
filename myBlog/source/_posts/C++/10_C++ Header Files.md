# C++ Header Files

在C#和Java中，是没有头文件这个概念的，也没有存在两种不同的文件类型的概念。

所谓的两种不同文件类型的概念，比如在C++中，一种是cpp文件，一种是头文件。

在C++基础中，头文件传统上是用来声明某些函数类型，以便可以用于整个程序中。

```cpp
// 头文件保护方法（防止多次复制引用）
#ifndef _LOG_H
#define _LOG_H

void InitLog();
void Log(const char* message);

struct Player{};

#endif
```

上面这种形式过去经常使用，但是我们现在有这个新的预处理语句叫做**#pragma once**，所以我们现在大多数时候用**#pragma once**，**#pragma once**也更简洁一些。

#include语句中<>尖括号用于编译器内置的include路径下的头文件，而""双引号的形式可以用于所有。

为了区分C的标准库和C++标准库，C标准库里的头文件一般都有.h扩展名，而C++没有，比如iostream。