---
layout: post
title: 笨方法学习C语言（中文版）
category: programming
---

#C中的变量类型
在接下来我们会声明并定义不同类型的变量，以让你能够更好的理解一个简单的C程序的结构。

{% highlight  c %}
     #include<stdio.h>
     int main(int argc, char *argv[])
     {
     	int distance = 100;
     	float power = 2.345f;
     	double super_power = 56789.4532;
     	char initial = 'A';
     	char first_name[] = "zed";
     	char last_name[] ="Shaw";
     	printf("You are %d miles away.\n", distance);
	printf("You have %f levels of power.\n", power);
	printf("You have %f awesome super powers.\n", super_power);
	printf("I have an initial %c.\n", initial);
	printf("I have a first name %s.\n", first_name);
	printf("I have a last name %s.\n", last_name);
	printf("My whole name is %s %c. %s.\n",first_name, initial, last_name);

    	return 0;
      }
{% endhighlight %}

在这个程序中，我们声明了不同类型的变量然后使用不同的格式将其输出出来。

#你应该看到什么？
有的输出应该和我的一样。我们已经输出字符串这么多次了，你应该会渐渐的发现C的字符串格式和Python等其它语言很相似。

{% highlight bash %}
$ make ex6
cc -Wall -g    ex6.c   -o ex6
$ ./ex6
You are 100 miles away.
You have 2.345000 levels of power.
You have 56789.453200 awesome super powers.
I have an initial A.
I have a first name Zed.
I have a last name Shaw.
My whole name is Zed A. Shaw.
$
{% endhighlight %}

你可以看到我们设置了许多类型的变量并赋予相匹配类型的变量值，变量的类型会告诉编译器它的变量类型是怎样的（存储结构是怎样的）。

##整型
整型使用" int "来声明并使用" %d "来输出。

##浮点型
浮点型分单精度和双精度类型，分别用" float"和"double"类型来声明，使用” f%“来输出。

##字符
使用" char "关键字声明，赋值的字符使用单引号扩起来，输出使用" %C"。

##字符串(字符数组)
使用 "char *name[]"的形式声明，赋值使用双引号将字符串包含起来，输出时使用"%s"格式控制符。

>注意
>当我在说明C类型的时候，我会使用 "char[]"的形式而不是" char SOMENAME[]"的形式。这只是为了方便说明和方便英文书写而已，那并不是合法的C书写格式。

#如何打破？
你可以通过传送错误的参数给" printf()"来是程序运行出错。例如，你将输出我的名字的那行的"initial"与"first_name"变量交换位置，你就会发现你的函数会产生错误。当你运行修改后的程序，你会发现编译器给出一大堆的错误信息，你也许会得到“Segmentation fault”这样的错误，就像我那样：

{% highlight bash %}
$ make ex6
cc -Wall -g    ex6.c   -o ex6
ex6.c: In function 'main':
ex6.c:19: warning: format '%s' expects type 'char *', but argument 2 has type 'int'
ex6.c:19: warning: format '%c' expects type 'int', but argument 3 has type 'char *'
$ ./ex6
You are 100 miles away.
You have 2.345000 levels of power.
You have 56789.453125 awesome super powers.
I have an initial A.
I have a first name Zed.
I have a last name Shaw.
Segmentation fault
$

{% endhighlight %}
使用Valgrind运行你的程序，看它会告诉你关于“Invalid read of size 1”的信息。

#课外练习

* 使用其它的方式去更改printf函数的代码，然后编译运行，看发生了什么，最后修复它。
* 在网上查找关于 " printf formats "的信息，然后实在去练习使用。
* 探究看你可以使用几种方式来写一个数字，尝试八进制，十六进制以及其它你找到的方法。
* 尝试打印输出一个空的字符串。