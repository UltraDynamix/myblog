# How the C++ Linker works

**任何常量都可以在编译的时候计算出来。**

当我们完成代码的编译之后，我们需要进行一个叫做 **链接** 的过程。  

> 链接的 **主要工作** 就是：**找到每个符号和函数的<u>位置</u>**，并将它们链接在一起。  

**在编译的时候：**每个文件被编译成一个独立的obj文件作为 **translation unit**。他们之间没有任何关系，这些文件实际上没法沟通（**如果不通过Linker进行链接的话**）。因此，如果我们决定将程序写在多个C++文件中的话，**我们需要一种方法将这些C++文件链接到<u>一个程序中</u>**。

即使当你没有任何外部文件，当你把所有的程序函数写在一个文件之中的时候，应用程序还是需要知道**程序的入口点在哪儿**——你的 **Main()函数在哪儿**。所以这种情况下，Linker仍然需要链接主函数和其他东西。

当你选择 **编译** 的时候，VS只会编译你的程序，不会进行任何的链接操作，但是当你选择 **build** 你的程序的时候(或者说按下**F5**)的时候，它会进行编译操作，紧接着还会进行链接操作。

在一个 **不含有Main()** 函数的C++文件下，如果我们选择编译，控制台不会输出任何错误信息，而是会显示编译通过。但如果我们在这同一个文件中选择build，这是控制台会输出 **Linker连接错误** 的错误信息。

> 所以，实际上我们可以通过 **控制台输出的错误代码** 推断出我们的错误发生在哪个阶段，**我们会得到与每个阶段相关的不同类型的错误消息。**
>
> - 比如，如果是编译错误，控制台会输出类似 **C2143** 的错误代码，即以 <u>**C**开头</u>的错误代码。
> - 如果是链接错误，控制台会输出类似 **LNK1561** 的错误代码，即以 <u>**LNK**开头</u>的错误代码。
>
> **知道我们犯的是什么类型的错误是非常重要的。**

**⭐当编译器报错说 <u>入口函数必须被定义</u>的时候，这是因为我们是将代码编译成为一个应用程序，或者说一个exe可执行文件。**

如果我们进入我们项目的 **属性面板**，我们可以看到面板中的 **Configuration Type** 选项，一般情况下就是 **Application(exe)**，**⭐每一个exe文件都必须有一个程序入口点！！！** 

如果我们进入到Linker链接器的设置中，选择 **Advanced高级** 选项卡，可以看到一个 **Enter Point** 的自定义程序入口点，所以实际上我们是可以 **自定义一个入口点** 的，而非必须是Main()函数，但通常都是用Main()。

举例一个我们可能遇到的链接错误：

**unresolved external symbol （未解决的外部符号）**—— **当链接器找不到它需要的东西时，就会发生这种情况。**

```cpp
#include <iostream>

void Log(const char* message); // 此处声明了Log函数

int Multiply(int a, int b){
    Log("Multiply"); // 此处使用了Log函数
    return a * b;
}

int main(){
    std::cout << Multiply(5, 8) << std::endl;
}
```

在编译阶段，只要是 **声明过了的** 函数，我们在编译的时候，是不会报错的，编译会成功通过，编译器会 **相信你的函数声明，并相信某处一定存在着这个函数的定义**，即使事实上并没有任何地方存在这个函数的定义。

**找到你声明的函数的具体定义，是 <u>Linker的责任</u> 。**所以上面的代码在我们build整个项目的时候，会报错 **unresolved external symbol （未解决的外部符号）**。因为我们 **引用，或者说调用了** 一个没有具体定义，找不到定义的函数 **Log**。

```cpp
#include <iostream>

void Log(const char* message); // 此处声明了Log函数

int Multiply(int a, int b){
    //Log("Multiply"); **注释该行，不调用Log()**
    return a * b;
}

int main(){
    std::cout << Multiply(5, 8) << std::endl;
}
```

所以，如上，如果我们注释掉那行 **Log("Multiply");**，也就是 **不调用Log()** 这个函数，那么即使它没有定义，build之后也不会报错，因为我们没有使用它。

但是：

```cpp
#include <iostream>

void Log(const char* message); // 此处声明了Log函数

int Multiply(int a, int b){
    Log("Multiply"); // 此处使用了Log函数
    return a * b;
}

int main(){
    // std::cout << Multiply(5, 8) << std::endl;
    // 如果我们注释这一行
}
```

如上，如果我们注释掉调用了Multiply()的那一行，再进行build，控制台仍会报错！！！虽然从逻辑上来说，我们注释掉了Multiply()也就是我们没有调用Multiply()函数，也就是没有调用Log()函数，**那么为啥子它还是会报linking error呢？？？**

> 这是因为！虽然我们当前文件中并没有调用Multiply，但是链接器会认为可能其他文件中会调用这个Multiply，而Multiply中，调用了一个没有定义的Log函数，链接器首先要确认这个Log能够正确链接到一个可用的定义，然后去将调用了Multiply的文件链接到一起。

当然，如果我们确定一个方法只会在当前这个文件中自己使用，不会让别人用，那么我们完全可以消除这种linking的必要，因为multiply完全没有被调用过，也就是说我们永远都不需要调用Log()。那么如何做到呢？——

```cpp
#include <iostream>

void Log(const char* message); // 此处声明了Log函数

static int Multiply(int a, int b){
    Log("Multiply"); // 此处使用了Log函数
    return a * b;
}

int main(){
    std::cout << Multiply(5, 8) << std::endl;
}
```

如上，我们 **在Multiply()这个函数前加上<u>static</u>**，**这基本意味着这个乘法函数只是为这个translation unit声明的，也就是为当前这个.cpp文件声明的。**这个时候如果我们再进行build操作，我们就不会再收到任何的linking errors了。

**⭐你的函数声明和函数定义，它们两者的名称，返回值，参数类型，参数数量等等，要完全一致！**

## 还有什么情况会导致链接错误？

如果你定义并声明了两个一模一样的函数(名称、参数、返回值)，链接器也会报错，因为它不知道究竟应该把你对这个函数的调用链接到哪一个函数上。

不过这也有两种情况——

1. 将这个双胞胎函数写在同一个文件中：

   ```cpp
   void Log(const char* msg){
       std::cout << message << std::endl;
   }
   
   void Log(const char* msg){
       std::cout << message << std::endl;
   }
   ```

   这个时候进行build的话，会报编译错误，而没有链接错误，因为！两个完全一样的函数声明和定义，在同一个文件中，编译器就无法通过，还到不了链接的阶段，程序就报错终止了。

2. 但是如果我们把这个双胞胎分开成两个文件放的话，这时候build就不会报编译错误了，会报链接错误。

## 上面这种错误，有哪种实现方式？

我们创建一个头文件 —— **Log.h**

```cpp
// Log.h
void Log(const char* message){
    std::cout << message << std::endl;
}
```

然后我们在一个.cpp文件中调用Log()：

```cpp
// InitLog.cpp
#include <iostream>
#include "Log.h" // 为了使用Log()函数，我们引入Log.h头文件

 void InitLog(){
     Log("Initialized Log");
 }
```

此外，我们还在另一个.cpp文件中调用Log()：

```cpp
// main.cpp
#include <iostream>
#include "Log.h" // 为了使用Log()函数，我们引入Log.h头文件

static int Multiply(int a, int b){
    Log("Multiply"); // 此处使用了Log函数
    return a * b;
}

int main(){
    std::cout << Multiply(5, 8) << std::endl;
}
```

这时，如果我们build这个项目，会报错！ **错误提示，我们的log函数已经在 <u>log.obj</u> 中定义了！**，也就是说我们得到了一个重复符号的错误信息，然而我们明明 **只在Log.h中定义了Log()函数。**那这是为什么呢？

这就要回顾之前我们所说的 **include 的作用**——当我们include一个头文件的时候，我们事实上也就是把这个头文件的内容复制粘贴到我们的include语句的位置，也就是说，上面的两段代码其实真正的面貌是这个样子的：

```cpp
// InitLog.cpp
#include <iostream>
// 原本的 #include "Log.h" 就是如下所示
void Log(const char* message){
    std::cout << message << std::endl;
}

 void InitLog(){
     Log("Initialized Log");
 }
```

```cpp
// main.cpp
#include <iostream>
// 原本的 #include "Log.h" 就是如下所示
void Log(const char* message){
    std::cout << message << std::endl;
}

static int Multiply(int a, int b){
    Log("Multiply"); // 此处使用了Log函数
    return a * b;
}

int main(){
    std::cout << Multiply(5, 8) << std::endl;
}
```

在链接的时候，其实链接器所看到的内容是这个样子的，这不就是重复定义了嘛？！那么如何解决这个问题呢？

1. 我们可以把Log.h中的Log()函数 **标记为static**

   ```cpp
   // Log.h
   static void Log(const char* message){
       std::cout << message << std::endl;
   }
   ```

   这意味着，对这个Log()函数进行链接的时候，链接操作只发生在链接文件的内部，也就是说，这样做之后，InitLog.cpp 和 main.cpp 会 **有他们”自己版本“的log()函数**，它们各自的log()函数对其他的obj文件都是不可见的。这时我们再编译这个项目，就不会报错了。

2. 另一种做法就是，把这个函数标记为 **inline**

   ```cpp
   // Log.h
   inline void Log(const char* message){
       std::cout << message << std::endl;
   }
   ```

   **inline**的意思就是说，我们调用这个Log()函数的时候，是直接把它的body也就是里面的这行内容：

   ```cpp
       std::cout << message << std::endl;
   ```

   拿过来使用，这样的话，之前的两个调用Log()的地方其实就是这样的：

   ```cpp
   // InitLog.cpp
   #include <iostream>
   
    void InitLog(){
       std::cout << "Initialized Log" << std::endl;
    }
   ```

   ```cpp
   // main.cpp
   #include <iostream>
   
   static int Multiply(int a, int b){
       std::cout << "Multiply" << std::endl;    
       return a * b;
   }
   
   int main(){
       std::cout << Multiply(5, 8) << std::endl;
   }
   ```

   这样的情况下，自然就不会存在什么重复生命重复定义链接错误的问题！

3. 还有一种方法，也是大概率被采用的方法，就是把**Log()的定义**移动到刚才两个translation unit其中一个，也就是 InitLog.cpp 和 main.cpp 其中一个当中，因为 **现在所发生的错误就是因为Log()这个函数被包含在了两个translation unit之中，导致了重复声明和定义**，所以我们可以把它 **移动到第三个translation unit，或者放到现有的其中一个translation unit中**，像这样：

   ```cpp
   // Log.h
   // 去掉 inline 标记， 并且只留下函数声明！
   inline void Log(const char* message);
   ```

   ```cpp
   // InitLog.cpp
   #include <iostream>
   
   // 将Log() 方法放到InitLog.cpp中进行定义
   void Log(const char* message);
   {
       std::cout << message << std::endl;
   }
   
   void InitLog(){
   	Log("Initialized Log");
   }
   ```

   ```cpp
   // main.cpp main()函数保持不变
   // main.cpp
   #include <iostream>
   #include "Log.h" // 为了使用Log()函数，我们引入Log.h头文件
   
   static int Multiply(int a, int b){
       Log("Multiply"); // 此处使用了Log函数
       return a * b;
   }
   
   int main(){
       std::cout << Multiply(5, 8) << std::endl;
   }
   ```

   这样一来，我们include的Log.h头文件中只有Log()函数的声明，实际链接的Log函数只在InitLog.cpp中include了一次， 也就是这个函数的定义只会出现在一个translation unit中， 然后通过linker链接后，main会调用它。这样的情况下，编译是会完美通过的，perfect！

>**总结：**
>
>以上就是关于linker的基本工作原理了，记住！
>
>**⭐链接器，就是要将编译操作中所产生的那些obj对象文件链接起来！**
>
>链接器还会导入我们可能使用的其他库，比如 **C Runtime Library / C++ Standard Library / Platform API (if  necessary)** and so on.
>
>并且 链接 还有各种 **形式/类别** ：有 **静态链接** ，**动态链接** 。

