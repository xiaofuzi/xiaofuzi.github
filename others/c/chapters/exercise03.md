---
layout: post
title: 笨方法学习C语言（中文版）
---

#练习3：格式化输出
将makefile文件保持之前例子的样子，这样在编译时可以输出错误信息，之后我们也会加入更多的信息让make做更多的事。

许多的语言都有C风格的格式输出，下面我们来尝试一下：

    #include<stdio.h>
    int main()
    {
    	int age = 10;
    	int height = 72;

    	printf("I am %d years old.\n", age);
    	printf("I am %d inches tall.\n", height);

    	return 0;
    }
当你将上述代码编写到 ex3 文件之后，使用make构建并运行它，请确保修复掉所有的警告信息。

下面将对上述代码做一些深入的解释说明：

* 首先包含一个名为 stdio.h 的头文件，该头文件告诉编译器你讲使用标准输入输出函数“ printf ”。
* 然后你使用一个名为 age 的变量并赋值为10.
* 接着你使用一个名为 height 的变量并赋值为72.
* 然后用printf 函数输出这两个变量。
* 使用printf 你可以控制输出的样式多样化。
* 在函数printf中，你格式控制部分的变量将会被变量的值替代。

在这里你使用printf函数输出一个格式化的字符串，在字符串中包含你所定义的变量的值到终端上。

#你将会看到的结果？
当你使用make构建好并运行，你将会在终端中看到如下的结果：

    $ make ex3
    cc -Wall -g  ex3.c -o ex3
    $ ./ex3
    I am 10 years old.
    I am 72 inches tall.
    $
  
在接下来我将不会在告诉你如何运行make以及得到怎样的结果，所以请确信你已经直到如何使用make并且能够得到正确的输出。

#课外学习
在每个练习我都会设有一个额外学习的环节，我会让你自己去查找相关的信息然后自学。这对于一个程序员来说是很重要的。如果你每次遇到问题都不去自己尝试解决而是总去询问别人，那么你将永远无法独立的解决问题。这会让你对你自己的技术没有自行，而且你也总是需要其他人来帮助你完成你的工作。

要想摆脱这种习惯你就要强迫你自己在遇到问题时首先自己去寻找到正确的答案，在这个过程中尝试去解决遇到的问题，去验证自己觉得的可能的答案，然后自己去研究问题的所在。

对于本次的练习，我希望你到网上查找关于 printf 函数的所有的格式控制信息，像换行、tab键的输出等。对于格式控制符，你需要去查看类似%s 或 %d（分别输出字符串和整数）的控制符，学会使用它们。最后你可以看如何去控制输出的长度以及精度。

从先在开始，类似与这样的练习都会在课外练习部分出现，希望你能够好好的完成这部分的内容。

#如何打破它？
尝试下面的做法，这可能会是使你的程序在你的电脑上崩溃：

* 去除在第一个printf函数中的 age 变量，然后重新编译，你会得到一组警告信息。
* 运行你修改后的程序，结果可能会崩溃或者是输出奇怪的年龄。
* 将printf函数复原，然后去掉age的赋值语句然后重新编译运行。


    # edit ex3.c to break printf
    $ make ex3
    cc -Wall -g    ex3.c   -o ex3
    ex3.c: In function 'main':
    ex3.c:8: warning: too few arguments for format
    ex3.c:5: warning: unused variable 'age'
    $ ./ex3
    I  am -919092456 years old.
    I am 72 inches tall.
    # edit ex3.c again to fix printf, but don't init age
    $ make ex3
    cc -Wall -g    ex3.c   -o ex3
    ex3.c: In function 'main':
    ex3.c:8: warning: 'age' is used uninitialized in this function
    $ ./ex3
    I  am 0 years old.
    I am 72 inches tall.
    $

#课外练习

* 尝试其它的打破方法。
* 尝试输出其它3个控制符%的字符串。
* 添加ex3的信息到makefile文件中，然后使用make清除中间文件并重新编译构建。
* 添加ex3的信息到makefile文件中，然后使用make clean命令清除ex3文件。

