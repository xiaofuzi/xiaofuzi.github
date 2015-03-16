---
   layout: default
   title: Developing Your Css Framework
---

# Developing Your Css Framework

##Divide&Rule
我们经常用CSS来进行布局、排版、表单以及一些常用元素列表、图片、等，确保我们的网页在所有的浏览器上都能很好的显示。当然我们还会有一些常用的组件像menu、gallery、slider等。编写CSS框架的目的即将我们经常使用的通用部分提取出来，这样就可以提高我们的开发效率。


我们可以将CSS按如下分类（并不一定需要如此划分）：

* reset.css
* base.css
* typography.css
* layout.css
* form.css
* table.css
* broser.css
* print.css

##下面列出几个可参考的资源：
不同的浏览器对原生HTML的解析样式是有所不同的，如(margin,padding,border,outline etc),为了使我们的CSS框架的展现效果在各种浏览器中都能得到一致的效果，我们需要重新定义这些样式效果。

* [Eric Meyer CSS Reset](http://meyerweb.com/eric/thoughts/2007/05/01/reset-reloaded/)
* [YUI Reset CSS](http://developer.yahoo.com/yui/reset/)
* [ Normalize.css](http://www.yyyweb.com/demo/inner-show/normalize.html)(bootstrap使用该reset)
以上是两个主流的框架的reset.css部分，可以作为参考。
* [YUI Base CSS](http://developer.yahoo.com/yui/base/)


排版和布局会因设计因素而有很大的影响，所以是否要引入这两个部分是有争议的，也可以引入多种类型的排版和布局方式。

##浏览器兼容

* [IE6 CSS Fixer: Starter Kit](http://www.onderhond.com/tools/ie6fixer/)
* [CSS Hack](http://www.webdevout.net/css-hacks)
* [Developing CSS for IE6 and 7](http://www.edgeofmyseat.com/blog/developing-css-for-ie6-and-7)
* [Explorer Exposed!](http://www.positioniseverything.net/explorer.html)



###Step1：reset.css，base.css
Normalize.css 是一个可定制的 CSS 文件，使浏览器呈现的所有元素，更一致和符合现代标准。它正是针对只需要统一的元素样式。该项目依赖于研究浏览器默认元素风格之间的差异，精确定位需要重置的样式。这是一个现代的，HTML5-ready 的 CSS 重置样式集。使用其作为我们框架的CSS重置集。

###Step2:栅格系统设计
目标：

 * 响应式
 * 流式布局
 * 移动支持
 * 支持嵌套



