# 对字符串进行遍历

简单的遍历

* 字符串是以'\0'结束的

```c
#include <stdio.h>

void print(char *str)
{
    if (str == NULL)
    {
        return;
    }

    int len = 0;
    char *p = str;
    while (*p++ != '\0')
    {
        len++;
    }
    
    for (size_t i = 0; i < len; i++)
    {
        printf("str[%ld] = %c ", i, str[i]);
    }
    printf("\n");
    
    p = str;
    for (size_t i = 0; i < len; i++)
    {
        char temp = *p++;
        printf("str[%ld] = %c ", i, temp);
    }
}

int main()
{
    char *str = "Hello World";
    print(str);
}
```

