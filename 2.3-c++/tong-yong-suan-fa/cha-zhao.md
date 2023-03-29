---
description: find()等方法
---

# 查找

```
auto res = std::find(vec.begin(), vec.end(), 7);
vector<int>::iterator r = std::find(vec.begin(), vec.end(), 7);
```

`std::find() 查找序列中的的value`

返回的是一个迭代器，迭代器指向的是序列中的该元素的位置，如果找不到迭代器指向的应该是 `vec.end();`

```c
// find
auto res = std::find(vec.begin(), vec.end(), 7);
vector<int>::iterator r = std::find(vec.begin(), vec.end(), 7);

if (res == vec.end())
{
    cout << "can't find " << endl;
}
else
{
    cout << "can find " << endl;
}

for (const int &num : vec)
{
    cout << num << " ";
}
```
