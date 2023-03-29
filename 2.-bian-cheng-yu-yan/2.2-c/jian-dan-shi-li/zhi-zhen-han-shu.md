# 指针函数

关于函数指针的部分​

#### 函数指针的声明 <a href="#han-shu-zhi-zhen-de-sheng-ming" id="han-shu-zhi-zhen-de-sheng-ming"></a>

```c
int (*func)(int, int);
```

只要是这个结构的函数都可以使用该函数指针来指向，指向的是函数的地址

#### 函数指针作为参数 <a href="#han-shu-zhi-zhen-zuo-wei-can-shu" id="han-shu-zhi-zhen-zuo-wei-can-shu"></a>

```c
int pCal(int (*func)(int, int), int a, int b);
```

#### 函数指针示例 <a href="#han-shu-zhi-zhen-shi-li" id="han-shu-zhi-zhen-shi-li"></a>

**计算器**

```c
#include <stdio.h>
int add(int a , int b ){
    return a + b;
}
int minus(int a , int b ){
    return a - b;
}
int mul(int a,int b){
    return a * b;
}
int div(int a,int b){
    return a / b;
}
int pCal(int(*func)(int,int),int a ,int b)
{
    return func(a,b);
}
int main(int argc, char **argv){
    int res = pCal(&minus,5,3);
    printf("%d\n",res);
}
```

**更好的计算器**

```c
#include<stdio.h>
#include<stdint.h>
//定义方法
int64_t add_handler(int64_t num1 , int64_t num2){
    return num1 + num2;
}
int64_t sub_handler(int64_t num1 , int64_t num2){
    return num1 - num2;
}
int64_t mul_handler(int64_t num1 , int64_t num2){
    return num1 * num2;
}
int64_t div_handler(int64_t num1 , int64_t num2){
    return num1 / num2;
}
//定义函数原型
typedef int64_t (*handler_t)(int64_t,int64_t);
//定义操作数
typedef enum {
    ADD,
    SUB,
    MUL,
    DIV
}op_t;
//定义存放方法的数组
handler_t handler_table[4];
//将方法存放到数组中
void init_handler(){
    handler_table[ADD] = &add_handler;
    handler_table[SUB] = &sub_handler;
    handler_table[MUL] = &mul_handler;
    handler_table[DIV] = &div_handler;
}
//定义操作对象
typedef struct OB{
    op_t op;
    int64_t num1;
    int64_t num2;
}ob_t;
//执行方法的函数
void exec_handler(ob_t ob){
handler_t handler = handler_table[ob.op];
    printf("result is %d\n",handler(ob.num1,ob.num2));
}
int main(){
    ob_t ob;
    ob.op = ADD;
    ob.num1 = 12;
    ob.num2 = 4;
    init_handler();
    exec_handler(ob);
}

```
