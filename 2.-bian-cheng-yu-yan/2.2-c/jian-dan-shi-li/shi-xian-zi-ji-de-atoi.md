---
description: 将字符串"123"转换成int类型的123
---

# 实现自己的Atoi

```c
//gcc my_atou.c -lm -o my_atoi
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



