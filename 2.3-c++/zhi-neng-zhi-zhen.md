---
description: 能很好的避免内存泄漏
---

# 智能指针

1. 1.智能指针的概述
2. 2.独占指针: `unique_ptr`
3. 3.`unique_ptr`与函数
4. 4.计数指针：`shared_ptr`
5. 5.`shared_ptr`与函数
6. 6.`shared_ptr`与 `unique_ptr`的转化
7. 7.`weak_ptr`: shared\_ptr的补充

​

#### 1、智能指针概述 <a href="#1-zhi-neng-zhi-zhen-gai-shu" id="1-zhi-neng-zhi-zhen-gai-shu"></a>

* C++的指针包括两种
  * 原始指针
  * 智能指针
* 智能指针是对原始指针的封装，避免内存泄漏

**智能指针与原生指针**

* 不是所有指针都能封装成智能指针
* 最常用的是`unique_ptr`和`shared_ptr`
* `weak_ptr`只是`shared_ptr`的补充，应用场景较少

智能指针只解决了一部分问题，**即独占/共享所有权指针的释放、传输**智能指针并没有完全解决C++内存安全，所有Rust出现了

#### 2、独占指针：unique\_ptr <a href="#2-du-zhan-zhi-zhen-uniqueptr" id="2-du-zhan-zhi-zhen-uniqueptr"></a>

* unique\_ptr
  * 在任何给定时刻，只能有一个指针管理内存
* 当指针超出作用域时，内存将被释放
* 该类型指针不可被Copy，只可以Move
  * Copy是指复制构造该变量
    * 新建一个堆内存
  * Move只是移动构造该变量
    * 引用原有的堆内存

**创建方式**

* 三种创建方式
  * 通过已有的裸指针创建
    * 之后建议释放掉裸指针
  * 通过new创建
  * 通过std::make\_unique创建(best)
* unique\_ptr可以通过get()获取地址
* unique\_ptr实现了 -> 与 \*
  * 可以通过 -> 调用成员函数
  * 可以用 \* 调用 dereferencing 解引用

**example**

裸指针和unique\_ptr的不同使用裸指针要将原有指针设置为nullptr，这样才算是符合 unique\_ptr中的 unique创建的三种方式

1. 1.`Cat *p1 = new Cat("p1"); std::unique_ptr<Cat> u_c_p1{p1};`
2. 2.`std::unique_ptr<Cat> u_c_p2{new Cat("p2")};`
3. 3.最推荐的方式 `std::unique_ptr<Cat> u_c_p3 = std::make_unique<Cat>();`

get() 与 -> 和解引用

* get() 方法能返回指针指向的地址
  * `cout<< u_c_p3.get()<<endl;`
* \-> 能使用指针的成员变量
  * `u_c_p3->get_info();`
* \*能打印值
  * `std::unique_ptr<int> u_int_ptr = std::make_unique<int>(100);`
  * `cout<< *u_c_p3<<endl;`



