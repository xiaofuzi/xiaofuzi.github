---
layout: post
title: 笨方法学习C语言（中文版）
---

#练习4：valgrind介绍
Valgrind，一个让你既爱又恨的工具，从现在开始我将带你了解它，因为在接下来的每个练习的“打破”环节中你都会用到它。Valgrind是一个运行你的程序然后报告出你的程序里的所有糟糕的错误问题的程序。在我写C代码的过程中，我一直都在使用它，它是软件中不可多得的免费的工具。

还记得在上一个练习中，我让你移除printf函数中的一个参数吗？移除后会输出一些奇怪的结果，但是我并没有告诉你为什么会输出这些结果。在这个练习中，我将使用Valgrind这个工具告诉你为什么？

####注意：
在开始的这几个练习中会使用一些很好的工具处理一些简单的代码作为示范，这些工具将在本书的余下部分中用到。因为许多阅读本书的人对静态语言和自动化编译及其它的有用的工具不熟悉，所以我会在这里说明，现在让你使用make 和 Valgrind会让你学习C更快，同时也尽早的帮助你解决你遇到的bug。
做完本次的练习之后，我会花一段时间讲解C语言的语法，也会用少量的工具让你更好的理解我们在做什么，对于遇到的错误和问题也有更好的理解。

#Valgrind安装
你可以通过你的系统的包管理程序安装valgrind，但是在这里，我想教你如何使用源代码安装程序。通过下面的这些步骤来完成：

* 下载源代码的归档文件来得到源代码。
* 解压归档文件到你的电脑上。
* 运行 ./configure 命令来设置配置信息。
* 运行make来构建程序，就如同之前做的一样。
* 运行 sudo 命令将程序安装到你的电脑上。


下面是我所做的流出，你需要按照我做的在你的机器上做一遍：
{% highlight bash %}
	# 1) Download it (use wget if you don't have curl)
     curl -O http://valgrind.org/downloads/valgrind-3.6.1.tar.bz2
     # use md5sum to make sure it matches the one on the site
    md5sum valgrind-3.6.1.tar.bz2
    # 2) Unpack it.
    tar -xjvf valgrind-3.6.1.tar.bz2
    # cd into the newly created directory
    cd valgrind-3.6.1
    # 3) configure it
    ./configure
    # 4) make it
    make
    # 5) install it (need root)
    sudo make install
{% endhighlight%}
按照以上的步骤安装新版本的Valgrind程序，如果出现问题，请自己去找到问题的所在并解决。

#Valgrind使用
Valgrind的使用是非常简单的，你只需要使用 valgrind命令加上你的程序名然后它就会运行你的程序并在运行的过程中输出关于你程序的错误信息。在这个练习中我们会将上一个练习的代码输出部分做些错误处理然后用valgrind运行它，观察得到怎样的结果，之后我们在修复我们的程序。

下面是我们对ex3.c有意做的错误处理，将其重新编写到一个名为ex4.c的文件中，作为练习，请自己编写该文件的代码。

    #include<stdio.h>
    int main()
    {
    	int age  = 10;
    	int height ;
    	printf("I am %d years old.\n");
    	printf("I am %d inches tall.\n", heght);
     
    	return 0
    }

运行上述代码，你会看到与之前得到的结果相比会多出两个我所做的错误。

* height 变量初始化失败。
* 第一个printf 函数中缺失 age 变量。

#你将会看到的结果？
将上述代码重新构建后，分别直接运行和使用Valgrind运行该程序。

    $ make ex4
	cc -Wall -g    ex4.c   -o ex4
	ex4.c: In function 'main':
	ex4.c:10: warning: too few arguments for format
	ex4.c:7: warning: unused variable 'age'
	ex4.c:11: warning: 'height' is used uninitialized in this function
	$ valgrind ./ex4
	==3082== Memcheck, a memory error detector
	==3082== Copyright (C) 2002-2010, and GNU GPL'd, by Julian Seward et al.
	==3082== Using Valgrind-3.6.0.SVN-Debian and LibVEX; rerun with -h for copyright info
	==3082== Command: ./ex4
	==3082== 
	I am -16775432 years old.
	==3082== Use of uninitialised value of size 8
	==3082==    at 0x4E730EB: _itoa_word (_itoa.c:195)
	==3082==    by 0x4E743D8: vfprintf (vfprintf.c:1613)
	==3082==    by 0x4E7E6F9: printf (printf.c:35)
	==3082==    by 0x40052B: main (ex4.c:11)
	==3082== 
	==3082== Conditional jump or move depends on uninitialised value(s)
	==3082==    at 0x4E730F5: _itoa_word (_itoa.c:195)
	==3082==    by 0x4E743D8: vfprintf (vfprintf.c:1613)
	==3082==    by 0x4E7E6F9: printf (printf.c:35)
	==3082==    by 0x40052B: main (ex4.c:11)
	==3082== 
	==3082== Conditional jump or move depends on uninitialised value(s)
	==3082==    at 0x4E7633B: vfprintf (vfprintf.c:1613)
	==3082==    by 0x4E7E6F9: printf (printf.c:35)
	==3082==    by 0x40052B: main (ex4.c:11)
	==3082== 
	==3082== Conditional jump or move depends on uninitialised value(s)
	==3082==    at 0x4E744C6: vfprintf (vfprintf.c:1613)
	==3082==    by 0x4E7E6F9: printf (printf.c:35)
	==3082==    by 0x40052B: main (ex4.c:11)
	==3082== 
	I am 0 inches tall.
	==3082== 
	==3082== HEAP SUMMARY:
	==3082==     in use at exit: 0 bytes in 0 blocks
	==3082==   total heap usage: 0 allocs, 0 frees, 0 bytes allocated
	==3082== 
	==3082== All heap blocks were freed -- no leaks are possible
	==3082== 
	==3082== For counts of detected and suppressed errors, rerun with: -v
	==3082== Use --track-origins=yes to see where uninitialised values come from
	==3082== ERROR SUMMARY: 4 errors from 4 contexts (suppressed: 4 from 4)
	$


####注意
If you run valgrind and it says something like by 0x4052112: (below main) (libc-start.c:226) instead of a line number in main.c then add run your valgrind command like this valgrind --track-origins=yes ./ex4 to make it work. For some reason the Debian or Ubuntu version of valgrind does this but not other versions.

因为Valgrind将每个问题的细节都输出出来，所以会有很多的信息。下面我会为你一行一行的讲解输出的内容（左边会有行号说明）。

####1
make 命令构建 ex4 程序，请确保你的 CC 编译命令正确（如果没有 -g属性，Valgrind的输出将没有行号）。

####2-6
可以注意到，编译器对你的源文件也输出了许多的信息并出现“缺少参数”的警告信息。
这是因为你没有包含 age 变量的原因。

####7
使用 valgrind ./ex4命令运行你的程序。

####8
Valgrind会给你输出一大串的信息：

* ####14-18
错误信息中有：在ex4.c文件的第十一行main函数中，你使用了8 bit 的为初始化的内存。然后你会在该行的下面出现栈溢出的提示信息。
On line main (ex4.c:11) (read as "in the main function in file ex4.c at line 11) you have "Use of uninitialised value of size 8". You find this by looking at the error, then you see what's called a "stack trace" right under that. The line to look at first (ex4.c:11) is the bottom one, and if you don't see what's going wrong then you go up, so you'd try printf.c:35. Typically it's the bottom most line that matters (in this case, on line 18).
* ####20-24
下一个错误还是出现在了第十一行代码中，这个错误显示的是某中控制语句使用了未实例化的变量。
* ####25-35
接下来给出的错误信息和前面的差不多，因为出错的原因是因为同样的变量被重复使用了而已。


####37-46
最后Valgrind给出一个总结信息说明你的程序有多么的糟糕然后退出程序。


这次的练习有很多的知识需要消化，但你只要做到下面的几点就可以了：

*  每次运行C程序的时候，使用 Valgrind 运行一遍。
*  对应于每个错误，定位带源代码中去，找出错误的原因并修复该错误，如果你不清楚问题的所在的话，可以到网上查找解决方法。
*  如果你的程序使用Valgrind运行没有给出错误信息，说明你的代码已经写得很正确了（你之前可能已经学习过编程）。

我并不想通过本次练习让你完全的掌握Valgrind的使用，而是希望你学会安装并会使用它，在之后的练习中都会用到它。

#课外练习

* 借助于Valgrind和编译器，修复该程序。
* 在网上查找关于 Valgrind 的资料，并阅读了解。
* 下载其它的软件然后手动构建它，可以尝试一些你使用过的但是之前重来没有构建过的软件。
* 浏览下Valgrind的源码和它的makefile文件。不用担心，即使使我也无法完全看懂。