---
layout: post
title: 使用yeoman开发web应用
category: programm
tags: [web, node, '前端']
---

##认识[yeoman](http://yeoman.io)
Yeoman是一个可以帮助我们高效的开发Webapp的工具，它内置了yo,bower,grunt三个工具，这三者都是对web开发十分便利的开发利器（如果你觉得Yeoman过于臃肿，可以单独使用以上的工具）。

![yeoman](http://ww3.sinaimg.cn/mw690/7cc829d3gw1ehy6vblvjsj20gj0net9v.jpg)

* yo是一个生成器，用于构建特定框架的生态系统的代码工具。
* [Grunt](http://gruntjs.com/)或者[Gulp](http://gulpjs.com/),项目的创建，预览以及测试工具。
* [bower](http://bower.io/)，一个包管理工具。

##yeoman安装
首先需要安装如下的依赖项：

* Node.js
* npm

然后使用如下命令安装yeoman

     $ npm install --global yo
     $ yo --version && bower --version && grunt --version //查看是否安装成功
     $ yo      //进入yo菜单

##生成器安装
    npm install -g generator-angular

##一个简单的例子[参考实现Todos](http://blog.jobbole.com/65399/#comment-147241)
新建一个目录并进入到该目录中，运行生成器

     $yo angular

yo会询问你是否要加载一些共同开发的类库以及选择你需要使用的Angular模块。

安装完成后，就可以在浏览器中查看你的应用

     grunt serve  //该命令会启动一个基于Node的http服务

这里会通过一系列的Grunt任务来监视你的文件更改情况，一旦发现文件发生修改就会自动刷新应用。

####[我的示例代码](https://github.com/xiaofuzi/yeoman-todos)