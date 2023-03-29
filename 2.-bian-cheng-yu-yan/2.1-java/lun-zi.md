# 轮子

## 实现字符串指定位置反转

需求：C++中有一个reverse(),这个方法的优点是能指定位置

C++demo

```cpp
// reverse algorithm example
#include <iostream>     // std::cout
#include <algorithm>    // std::reverse
#include <vector>       // std::vector

int main () {
  std::vector<int> myvector;
  // set some values:
  for (int i=1; i<10; ++i) myvector.push_back(i);   // 1 2 3 4 5 6 7 8 9
  std::reverse(myvector.begin(),myvector.end());    // 9 8 7 6 5 4 3 2 1
  return 0;
}
```

Java实现reverse

```java
public class Reverse {    
    public void reverse(StringBuffer s,int begin,int end){
        String s1 = s.substring(begin, end);
        StringBuffer reverse = new StringBuffer(s1).reverse();
        for (int i = begin; i < end; i++) {
            s.replace(begin,end,reverse.toString());
        }
    }

    public static void main(String[] args) {
        String str = "Good";
        StringBuffer sb = new StringBuffer(str);
        new Reverse().reverse(sb,0,2);
        System.out.println(sb.toString());
    }
}

```

Learn:

Tips:**String StringBuffer  StringBuilder**

当时想使用String作为参数传递，发现String在函数之间的传递是`值传递`

就是当传递字符串的时候，是将引用传递过去，但是当你修改该字符串的时候，只是修改引用的地址

* 字符串常量是无法修改的因为放到了JVM的静态常量池中
* 当传递字符串的时候，对字符串的任何修改，只是会创建一个新的内存空间，并将该引用指向这个内存空间中。
* StringBuffer 线程安全，多线程下使用这个
* StringBuilder 线程不安全，但是效率快一些





