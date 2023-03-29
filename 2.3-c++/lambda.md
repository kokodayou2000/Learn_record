# Lambda

`Lambda`

在C++中可以被调用的对象有

1. 函数
2. 函数指针
3. class 操作符
4. lambda

格式

`[捕获的列表](参数列表)->返回值类型 {函数体}`

```
/**
 * callable object c++ 4
 *  1.function
 *  2.function pointer
 *  3.class operator()
 *  4.lambda
 *      format
 *          [capture list](parameter list) -> return type {function body}
 *
 */
```



```cpp
int main(int argc, char **argv)
{

    int inner = 1;
    auto my_lambda = [&](int a) -> int
    {
        cout << "inner: " << inner << endl;
        return a;
    };

    int a = my_lambda(100);
    cout << a << endl;

    return 0;
}
```

当成函数来使用

```c
vector<int> vec = {3, 2, 5, 1, 4};
auto wannBigger = [&](const int &i1, const int &i2) -> bool
{
    return i1 > i2;
};
std::sort(vec.begin(), vec.end(), wannBigger);
for (auto it = vec.begin(); it != vec.end(); it++)
{
    cout << *it << endl;
}
```

#### 值拷贝和应用拷贝

lambda是在创建的时候进行拷贝的，而不是使用的时候才拷贝的

拷贝方式

* `[]`
* `[=]  值拷贝`
* `[&] 引用拷贝`
* `[=,reference list...] 先值拷贝后引用拷贝`
* `[&,value list...] 先引用拷贝后值拷贝`

区别

```c
int main() {
    int sz = 5;

    //值拷贝
    auto lambda_by_value = [=](){
        return sz;
    };

    //引用拷贝
    auto lambda_by_reference = [&](){
        return sz;
    };

    sz = 100;

    cout<< lambda_by_value()<<endl;
    cout<< lambda_by_reference()<<endl;
}
```



