# 比较器

用于排序什么的

**系统自带的对向量进行排序的方法**

```c
#include <iostream>
#include <vector>
#include <algorithm>

using std::cout;
using std::endl;
using std::vector;

void func()
{
    vector<int> vec = {3, 5, 9, 1, 2, 4, 0, 7, 6, 8};
    // sort
    std::sort(vec.begin(), vec.end());
    for (auto it = vec.begin(); it != vec.end(); it++)
    {
        cout << *it << endl;
    }
}
int main(int argc, char **argv)
{
    func();
    return 0;
}
```

系统自带的比较器扩展

```c
    std::sort(vec.begin(),vec.end(),std::less<int>());
    std::sort(vec.begin(),vec.end(),std::greater<int>());
```

**实现自己的比较器**

```c
//先打印大的
bool WannBigger(const int &i1, const int &i2)
{

    return i1 > i2;
}
//use std::sort(vec.begin(), vec.end(), WannBigger);
```

可以高度自定义

```c
//只是把0放到第一位
bool WannOneFirst(const int& i1,const int &i2){
    if (i1 == 0)
    {
        return true;
    }
    return false;
}

```
