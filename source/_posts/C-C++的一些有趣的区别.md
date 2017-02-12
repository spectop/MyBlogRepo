title: "C/C++的一些有趣的区别"
date: 2015-03-17 22:55:06
categories: "C/C++"
tags:
  - C/C++
---
在[geeksforgeeks](http://www.geeksforgeeks.org)上看到一篇文章，说的是一些在C中可以编译但在C++中不行的程序，觉得比较好玩，就翻译分享一下啦。

***

- 在C++中，在main()中使用其它自定义的函数时必须在前面写上声明或者定义，但是在C中却可以写在main()的后面

```
#include<stdio.h>
int main()
{
   foo(); // foo() is called before its declaration/definition
   return 0;
} 
 
int foo()
{
   printf("Hello");
   return 0; 
}

```
上面的程序在C中可以编译成功，但是在C++中就不行

***

- 在C++中，指针是不能指向一个常量的，但是在C中可以

```
#include <stdio.h>
 
int main(void)
{
    int const j = 20;
 
    /* The below assignment is invalid in C++, results in error
       In C, the compiler may throw a warning, but casting is
       implicitly allowed */
    
    int *ptr = &j;  // A normal pointer points to const
 
    printf("*ptr: %d\n", *ptr);
 
    return 0;
}
```

***

- 在C语言中，一个空指针可以直接指派给其他指针，如int*，char *。但在C中，必须指定类型

```
#include <stdio.h>
int main()
{
   void *vptr;
   int *iptr = vptr; //In C++, it must be replaced with int *iptr=(int *)vptr; 
   return 0;
}
```

***

- 下面的程序在C中可以编译，但是在C++中不行，必须为常量初始化

```
#include <stdio.h>
int main()
{
    const int a;   // LINE 4
    return 0;
}
```
> Line 4 [Error] uninitialized const 'a' [-fpermissive]

***

- 在C中可以用C++的一些特定的关键字作为变量名

*p.s. 这是自然，汗*

```
#include <stdio.h>
int main(void)
{
    int new = 5;  // new is a keyword in C++, but not in C
    printf("%d", new);
}
```

***

- C++的检查会比C更严格，如：

```
#include <stdio.h>
int main()
{
    char *c = 333;
    printf("c = %u", c);
    return 0;
}
```

> error “invalid conversion from ‘int’ to ‘char*'”.

***

**试了一些，确实是这样，感觉蛮有趣的！**

[原文链接](http://www.geeksforgeeks.org/write-c-program-wont-compiler-c/)
