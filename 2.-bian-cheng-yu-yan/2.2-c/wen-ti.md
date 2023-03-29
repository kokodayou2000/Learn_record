# 问题

关于C的一些问题

**1. 变量的声明和定义的区别**

一个变量可以声明多次但只能定义一次。声明并不分配内存，具体使用的时候才会初始化。

**2.简述#ifdef、#else、#endif和 #ifndef的作用**

* 使用#ifdef、#endif将功能模块包裹进去，可以向特定用户提供功能。在不需要的时候用户可以将其屏蔽掉

```c
#ifdef MATH
#include "math.c"
#endif
```

* debug和trace

```c
#ifdef DEBUGprintf("debug...");
#endif
```

**3.结构体之间能直接赋值吗？**

相同结构体的不同变量是能直接赋值的，但是结构体中含有指针成员要小心。

**4.sizeof 和 strlen的区别**

* sizeof是操作符，strlen是\<stirng.h>的函数
* sizeof的参数sizeof(int) or sizeof(value)，而strlen只能以结尾是'\0'的字符串结尾
* 编译器在编译器就把sizeof的结果算出来了，strlen在运行的时候才能计算出来
* sizeof计算的的内存大小，strlen计算的实际字符串长度
* 数组在传递给strlen就退化成指针了

**5.c的static 和 c++的static的区别**

C的static只能修饰局部变量和外部静态变量，但是C++可以定义类的成员变量和函数。

```cpp
class A{
public:
    int a_;
    A(int a): a_(a){}
    void func() const{
        cout<< "const function" <<end
    }
}
```

**6. C的 malloc 和C++中new的区别**

* new,delete只能在C++中使用
* malloc,free能在C/C++中使用
* new 可以调用对象的构造函数，对应的delete调用析构函数
* malloc仅仅分配内存，free仅仅释放内存
* new,delete返回的是数据类型的指针，malloc,free只能返回(void\*)

**7.宏示例**

```c
#define MAX(a,b) ((a)>=(b)?(a):(b))
```

**8.volatile的作用**

* 禁止指令重排
* 当修饰的值发生变化的时候，别的线程一定能感知到

常用于

* 状态寄存器的并行设备硬件寄存器
* 一个中断服务子程序会访问到的非自动变量
* 多线程间被几个任务共享的变量

**9.为什么会有 const volatile int a = 10;**

* 这个变量在程序内部是只读的
* 只会在程序外部条件变化下变化
* const只在编译器发货作用，不能实际的禁止该端内存的读写特性。

**10.结构体内存对齐**

`#pragma pack(1)#pragma unpack()`

```c
#include <stdio.h>
#pragma pack(1) // 按照一字节对齐
struct S1
{
    int i;
    char j;
} s1;
#pragma unpack()

#pragma pack(2) // 按照二字节对齐
struct S2
{
    int i;
    char j;
} s2;

#pragma unpack()
struct S3
{
    int i;
    char j;
} s3;

int main()
{
    printf("%ld\n", sizeof(s1));
    printf("%ld\n", sizeof(s2));
    printf("%ld\n", sizeof(s3));

    return 0;
}
```

第 一 个 成 员 的 地 址 和 整 个 结 构 的 地 址 相 同 ， 向 结 构 体 成 员 中 s i z e 最 大 的 成 员 对 齐 。实际上默认的会要求按照4或者8的倍数。

**11.全局变量是如何实现的？操作系统和编译器是怎么知道的？**

* 通过内存分配的位置来知道的，全局变量分配在全局数据段，并且在程序开始的时候被加载，局部变量分配到堆栈中
* 全局变量是生命周期是在整个程序中

**13.C/C++的内存分配**

* 从静态存储区域分配
  * 全局变量，static变量，常量字符串
* 在栈上分配
  * 默认为2m的栈大小
* 从堆上分配
  * 程序可以使用malloc或者new分配任意大小的内存，更加灵活。频繁的分配和释放会产生内存碎片

内存布局

* 参数区
* 栈区
* 堆区
* 全局变量区
* 文字常量区
* 程序代码区

**14.简述strcpy、sprintf与memcpy的区别**

```c
char *strcpy (char *dest, const char *src);
```

实现两个字符串之间的拷贝

```c
void *memcpy (void *dest, const void *src,size_t __n);
```

memcpy的操作对象是两个可以操作的内存，不限制数据类型

```c
int sprintf (char *src,const char *format, ...);
```

格式化输出，src必须为字符，但是转换的可以是任意类型

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char src[40];
    char dest[100];

    //  全部填充'\0'
    memset(dest, '\0', sizeof(dest));

    strcpy(src, "This is runoob.com");
    strcpy(dest, src);

    printf("strcpy = %s\n", dest);

    char msrc[20] = "Hello memcpy";
    char mdest[20];

    memcpy(mdest, msrc, sizeof(msrc));
    printf("mcpy = %s\n", mdest);

    // 格式化输出
    char pstr[40];
    sprintf(pstr, "Pi's value  = %.4f", 3.1415);
    puts(pstr);

    return (0);
}
//output 
/** 
strcpy = This is runoob.com
mcpy = Hello memcpy
Pi's value  = 3.1415
*/
```

**15.((void \*)0)是什么？**

```c
#include <stdio.h>
// function pointer
int (*func)(int, int);
// function argument
int pCal(int (*func)(int, int), int a, int b);
//https://blog.csdn.net/songzhuo1991/article/details/105385866
//https://www.cnblogs.com/litifeng/p/7635220.html
#define NULL ((void *)0)
int main()
{
}
```

**16.typedef 和 define的区别是什么？**

* 用法不同：typedef 用来定义一种数据类型的别名，增强程序的可读性。define 主要用来定义常量，以及书写复杂使用频繁的宏。
* 执行时间不同：typedef 是编译过程的一部分，有类型检查的功能。define 是宏定义，是预编译的部分，其发生在编译之前，只是简单的进行字符串的替换，不进行类型的检查。
* 作用域不同：typedef 有作用域限定。define 不受作用域约束，只要是在define 声明后的引用 都是正确 的。
* 对指针的操作不同：typedef 和define 定义的指针时有很大的区别。
* typedef 是语句，需要加`;`

**17.指针常量和常量指针的区别**

指针常量强调指向一个只读对象，你不能通过指针常量来对对象修改

常量指针强调指针的不可变性​

```c
//函数参数,我希望是引用传递，但不允许参数在函数内部被修改
int sub(int *const a)
{
    return *a;
}

int *const p = &c;

```

指针常量是值定义一个指针，这个指针只能在定义的时候初始化，其他时刻无法改变。

```c
//我希望是引用传递，但不允许参数在函数内部被修改
int add(const int *a, const int *b)
{
    return *a + *b;
}
```

常量指针是定义一个指针，指向一个只读区域，不能通过常量指针来对该区域进行修改。​​​

<figure><img src="https://3731255506-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjqIJmJsRjNM2N5049rqA%2Fuploads%2FGbv4h1z2IcTIdoMMjDYq%2Fimage.png?alt=media&#x26;token=2d761b5b-5343-477b-9d11-55fed9542771" alt=""><figcaption></figcaption></figure>

这两种最大的用处还是在函数的形参上，保证实参在调用的时候，实参的不可变性。还有一种，指向常量的指针常量

```c
const int *const b = &c;
```



**18.设置修改指定地址上的值**

```c
#include <stdio.h>

int main()
{
    int *ptr;
    ptr = (int *)0x7777;
    *ptr = 0x6666;
    printf("%d\n", *ptr);
}
```

但是会段错误

**19.实现atoi()的功能**

```c
#include <stdio.h>
#include <math.h>

int myAtoi(char *str)
{
    int num = 0;
    int isNegative = 0;
    int n = 0;
    char *p = str;
    if (p == NULL)
    {
        return -1;
    }

    // 字符串长度
    while (*p++ != '\0')
    {
        n++;
    }
    // 重新赋值
    p = str;
    // 是否是负数
    if (p[0] == '-')
    {
        isNegative = 1;
    }
    char temp = '0';

    for (int i = 0; i < n; i++)
    {
        char temp = *p++;
        if (temp > '9' || temp < '0')
        {
            continue;
        }
        if (num != 0 || temp != '\0')
        {
            temp -= 0x30;
            double t = pow(10, n - 1 - i);
            num += temp * (int)t;
        }
    }

    if (isNegative)
    {
        return (~num + 1);
    }
    else
    {
        return num;
    }
}

int main()
{
    char a[] = "123";
    int res = myAtoi(a);
    printf("%d\n", res);

    return 0;
}
```

**20.C语言的结构体和C++的区别**

* C语言的结构体是不能有函数成员的
* C语言的没有访问限定`private public protected`
* C语言的结构体是没有继承关系的

**21.如何避免野指针**

delete或者free 之后应将指针设置为NULL指针越界，在指针作用域结束前释放内存，并让指针指向NULL

**22.句柄和指针的区别是什么**

句柄只是windows中用来标记资源的，这样可以隐藏系统的信息，只需要你去调用即可，句柄是一个32位的uint。指针是用来标记内存地址的(虚拟内存)

**23.new/delete和 malloc/free的区别是什么？**

* new能自动计算需要分配的资源，malloc需要手动计算
* new/delete返回的是有具体类型的指针，malloc/free返回void类型的指针
* new类型是安全的，编译器会识别一些错误的new
* new可以操作和构造。new操作可以重载，自定义内存分配策略
* new调用构造函数，delete调用析构函数
* new/delete是C++中自带的，不需要引入类似 \<stdlib.h>

**24.extern "C"是什么？**

被extern "C"修饰的会安装C的方式进行编译函数编译期最大的区别就是C语言不支持函数重载，编译器编译C的时候，不会带上函数的参数类型，编译C++的时候，会将函数的参数类型也添加上去。

* C++调用C语言代码
* 多人协作开发，让写C的人不会考虑C++编译器的情况

**25.C++中struct和class的区别**

* class默认继承权是private，struct默认是public
* class可以定义模板参数

**26.什么是右值引用和左值有什么区别？**

**27.多态？**

简单就是说子类可以使用父类的数据类型当参数

**28.C++中四种cast转换**

* const\_cast
  * 将const转换非const
* static\_const
  * 隐式转换
    * 非const转const
    * void\* 转 指针
    * 多态向上转化，向下转换不安全
* dynamic\_cast
  * 动态类型转换，只能用于包含虚函数的类
  * 用于类的向上或者向下转化，只能转换指针和引用
  * 如果向下转换可能会出现异常
* reinterpert\_cast
  * 什么都能转换，将int转换成指针，但出问题几率较大
* C的强制转换什么都能转，但不会进行错误检查，容易出错

​​

**29.理解 `(*(void(*)())0)();`**

* 是一个函数指针的强转
* 0是一个地址
* 0前面的 `(void(*)())`
  * void(\*)()int (\*func)(int, int);//空参数,没有名字，返回值是void的函数指针
  * 是一个函数指针（空参数）指向这个地址
* `(*(void(*)())0)`
  * 取出该地址的内容
* `(*(void(*)())0)()`
  * 执行

读变量技巧

* 从里往外
* 从右往左
* 一读函数
* 二找数组
* 三找指针

从变量开始读，先读优先级高的

**30.C++的空类有那些成员函数？**

* 构造函数
* 拷贝构造函数
* 析构函数
* 赋值运算符
* 取址运算符
* 取值运算符 const

**31.对C++的四种智能指针的理解**

* `shared_ptr`
* `unique_ptr`
* `weak_ptr`
* `auto_ptr`

智能指针的作用是管理一个指针，智能指针能很好的避免申请空间在函数结束时忘了释放，造成内存泄漏。智能指针本身就是一个类，有当超过了类的作用域，类就会调用析构函数，析构函数就能释放资源。智能指针的作用原理就是函数结束时自动释放内存空间，不需要手动释放内存空间。`auto_ptr已经在C11废弃`​​​​​​​​​​​​​​​





