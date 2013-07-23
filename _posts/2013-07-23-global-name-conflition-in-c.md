---
layout: post
title: C语言的全局名字冲突的陷阱
description: ""
category: 其他技术
tags: [C, C语言, 全局变量, 链接, global name, global variable, linkage in C, nm, symbol]
date: Tue Jul 23 09:13:34 +0800 2013
---
{% include JB/setup %}

C语言中全局变量和函数都是在链接期才根据需要来链接到可执行文件的，关于链接，还有一些有趣的话题，比如weak symbol等，这次的话题去全局名字冲突的陷阱。

## C语言全局变量冲突

在C语言的签名中，全局变量和函数是一样的，只是类型不一样，一个是Common symbol，一个是Text(code)，具体参考nm的手册：http://sourceware.org/binutils/docs-2.16/binutils/nm.html

所以如果在一个C语言文件里面，如果同时写了一个名字相同的函数指针变量以及一个函数，那么会造成编译期的错误提示：

    agspc98:tmp fluke$ gcc testconflict.c -o testconflict
    testconflict.c:6:6: error: redefinition of 'fglobal' as different kind of symbol
    void fglobal(){}
         ^
    testconflict.c:4:7: note: previous definition is here
    fun_t fglobal;
          ^
    1 error generated.

上面测试对应的源文件为：

{% highlight c %}
// testconflict.c
#include <stdio.h>

typedef void (*fun_t)();
fun_t fglobal;

void fglobal(){}

int main()
{
	return 0;
}
{% endhighlight %}

## C语言全局变量陷阱

冲突的问题还小，在编译期就可以发现，而如果刚好两个符号在编译阶段没发现冲突的话，到链接期，只能牺牲一个了，后果就是到运行期才发现问题，下面看testglobalname.c和testglobalname2.c两个文件，后者包含了重名的函数，当和前者一起链接的时候，产生了可能是意料之外的后果。

{% highlight c %}
// testglobalname.c
#include <stdio.h>

// also see testglobalname2.c

void foo()
{
	printf("foo\n");
}

typedef void (*fun_t)();
typedef void (*fun2_t)();


fun2_t f2global;

int main()
{
	fun_t f = foo;
	f();

	fun2_t f2local = foo;
	f2local();

	f2global = foo;
	f2global();

	return 0;
}
{% endhighlight %}

{% highlight c %}
// testglobalname2.c
#include <stdio.h>

void f2global()
{
	printf("f2global as function name\n");
}

void f2local()
{
	printf("f2local as function name\n");
}
{% endhighlight %}

单独第一个文件编译运行的结果如下（正常）:

	agspc98:tmp fluke$ gcc testglobalname.c -o testglobalname
	agspc98:tmp fluke$ ./testglobalname 
	foo
	foo
	foo

两个文件一起编译、链接、运行的结果如下（非法访问）：

	agspc98:tmp fluke$ gcc testglobalname.c -c
	agspc98:tmp fluke$ gcc testglobalname2.c -c
	agspc98:tmp fluke$ gcc testglobalname*.o -o testglobalname
	agspc98:tmp fluke$ ./testglobalname 
	foo
	foo
	agspc98:tmp fluke$ gcc testglobalname2.c -c
	agspc98:tmp fluke$ gcc testglobalname.c -c
	agspc98:tmp fluke$ gcc testglobalname*.o -o testglobalname
	agspc98:tmp fluke$ ./testglobalname 
	foo
	foo
	Bus error: 10

用nm看下两个文件编译出来的符号表:

	agspc98:tmp fluke$ nm testglobalname.o
	00000000000000c0 s EH_frame0
	000000000000007b s L_.str
	0000000000000008 C _f2global
	0000000000000000 T _foo
	00000000000000d8 S _foo.eh
	0000000000000020 T _main
	0000000000000100 S _main.eh
	                 U _printf
	agspc98:tmp fluke$ nm testglobalname2.o
	00000000000000b8 s EH_frame0
	000000000000003f s L_.str
	000000000000005a s L_.str1
	0000000000000000 T _f2global
	00000000000000d0 S _f2global.eh
	0000000000000020 T _f2local
	00000000000000f8 S _f2local.eh
	                 U _printf

## C++中的情况

因为c++的符号还带上了更多的类型信息，所以在这里没有产生冲突：

	agspc98:tmp fluke$ g++ testglobalname.c -c
	clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
	agspc98:tmp fluke$ g++ testglobalname2.c -c
	clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
	agspc98:tmp fluke$ g++ testglobalname*.o -o testglobalname
	agspc98:tmp fluke$ ./testglobalname 
	foo
	foo
	foo
	agspc98:tmp fluke$ nm testglobalname.o
	00000000000000b8 s EH_frame0
	000000000000006e s L_.str
	0000000000000000 T __Z3foov
	00000000000000d0 S __Z3foov.eh
	0000000000000120 S _f2global
	0000000000000020 T _main
	00000000000000f8 S _main.eh
	                 U _printf
	agspc98:tmp fluke$ nm testglobalname2.o
	00000000000000b8 s EH_frame0
	000000000000003f s L_.str
	000000000000005a s L_.str1
	0000000000000020 T __Z7f2localv
	00000000000000f8 S __Z7f2localv.eh
	0000000000000000 T __Z8f2globalv
	00000000000000d0 S __Z8f2globalv.eh
	                 U _printf


