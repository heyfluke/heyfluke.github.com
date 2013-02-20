---
layout: post
title: "用51c对8051MCU的SFR寄存器进行按位存取"
description: ""
category: 其他技术
tags: [8051, 51c, SFR, bit access]
date: 2013-02-20 23:36:27 +0800
---
{% include JB/setup %}

陈同学今天问我为什么在51c中写下面这句是错误的:

	sbit P2 = 0x02;

得到的错误信息大概是（编译错误）：

	C146: invalid absolute bit address

我印象中他之前问过我的程序中的寄存器位地址定义都是形如这样的：

	sbit myport = P1 ^ 2;

看似比较奇怪的语法，查了一下[Cx51的手册][1]得到了答案：

	The sbit type defines a bit within a special function register (SFR). It is used in one of the following ways:

	sbit name = sfr-name ^ bit-position;
	sbit name = sfr-address ^ bit-position;
	sbit name = sbit-address;

对于三种方式也都做了解释和例子：

Variant 1

	sbit name = sfr-name ^ bit-position;
	The previously declared SFR (sfr-name) is the base address for the sbit. It must be evenly divisible by 8. The bit-position (which must be a number from 0-7) follows the carat symbol ('^') and specifies the bit position to access. For example:

	sfr  PSW = 0xD0;
	sfr  IE = 0xA8;

	sbit OV = PSW^2;
	sbit CY = PSW^7;
	sbit EA = IE^7;

Variant 2

	sbit name = sfr-address ^ bit-position;
	A character constant (sfr-address) specifies the base address for the sbit. It must be evenly divisible by 8. The bit-position (which must be a number from 0-7) follows the carat symbol ('^') and specifies the bit position to access. For example:

	sbit OV = 0xD0^2;
	sbit CY = 0xD0^7;
	sbit EA = 0xA8^7;

Variant 3

	sbit name = sbit-address;
	A character constant (sbit-address) specifies the address of the sbit. It must be a value from 0x80-0xFF. For example:

	sbit OV = 0xD2;
	sbit CY = 0xD7;
	sbit EA = 0xAF;

注意到寄存器的定义都是8对齐的（可以参考头文件，我见过，但手上没有就懒得翻了），并且bit-position必须是0-7，可见用异或（^）不过是在达到效果的同时使得这看起来是一个漂亮的语法罢了。

从根本上来说，特殊功能寄存器（SFR）地址就被放在0x80-0xff这个范围内，每个寄存器大小都是8位。取位置的时候也可以用绝对值或者别的运算表达式来获取，例如：

	sbit P1 = 0x90;
	sbit myport1 = P1 + 1;
	sbit myport2 = P2 ^ 2;
	sbit myport3 = 0x93;

异或和加相等是因为最后3个二进制位是0，刚好容纳0-7。

[1]: http://www.keil.com/support/man/docs/c51/c51_le_sbit.htm
