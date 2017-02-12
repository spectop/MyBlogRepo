title: "Linux下如何实现C语言的system(\"pause\")"
date: 2015-04-15 09:23:57
categories: "C/C++"
tags:
  - Linux
  - C/C++
---

- **getch()** ?
	+ 不是标准库中的函数，在Linux中一般情况无法使用

- **getchar() + printf("\b")** ?
	+ 貌似使用getchar()读入，再输出一个退格符将原来回显的字符删除应该是可以的，但是在实际试了一下发现根本不行。。。

	+ **原因**：终端驱动器确实会读一个字符，但是他的输入只有到'\n' 或 EOF 才会结束，所以如果不输入回车就不会实际执行getchar().	当然，如果上一次输入的字符并没有全部读完是可以getchar()把没有读完的字符读掉。

-  ***解决办法***
```c
void system_pause(void)
{
	getchar();
 	puts("Press any key to continue...");
 	system("stty raw");
 	getchar();
	system("stty cooked");
	printf("\b");
}
```
这段代码也是我在网上找到的，我的理解是：
+ getchar()读掉上面多余的'\n'，按程序的实际情况添加
+ 输出"Press any key to continue..."
+ system("stty raw");：将终端驱动器改为一次一个字符的模式，即输入一个字符就结束输入
+ getchar(); 读一个字符
+ system("stty cooked"); 将终端驱动器改回一次一行的模式
+ printf('\b'); 退格，将回显的字符删除

***
p.s. 以上仅仅是个人理解，欢迎大家指出其中的错误