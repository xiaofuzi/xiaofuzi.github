---
   layout: post
   title: Html编写风格指南
---

# HTML

##HTML5 doctype
================
>为每个 HTML 页面的第一行添加标准模式（standard mode）的声明，这样能够确保在每个浏览器中拥有一致的展现。

```
<!DOCTYPE html>
<html>
    <head>
    </head>
</html>
```
####根据 HTML5 规范：
>强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

```
<html lang="zh-CN">   
  <!-- ... --> 
</html>
```

##IE 兼容模式
============
>IE 支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。

```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

##字符编码
=========
> 通过明确声明字符编码，能够确保浏览器快速并容易的判断页面内容的渲染方式。这样做的好处是，可以避免在 HTML 中使用字符实体标记（character entity），从而全部与文档编码一致（一般采用 UTF-8 编码）。

```
<head>   
  <meta charset="UTF-8"> 
</head>
```

##引入 CSS 和 JavaScript 文件
============================
>根据 HTML5 规范，在引入 CSS 和 JavaScript 文件时一般不需要指定 type 属性，因为 text/css 和 text/javascript 分别是它们的默认值。

```
<!-- External CSS --> 
<link rel="stylesheet" href="code-guide.css">  

<!-- In-document CSS --> 
<style>   /* ... */ </style> 
 
<!-- JavaScript --> 
<script src="code-guide.js"></script> 
```

##属性顺序
=========
> HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

* class
* id
* href

>class 用于标识高度可复用组件，因此应该排在首位。id 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。href 可排在最后一位，若有私有属性及其他标签，直接放到中间

```
<a class="..." id="..." data-modal="toggle" href=“#">
  Example link 
</a>  
<input class="form-control" type="text">  
<img src="..." alt="...">
```

##布尔（boolean）型属性
=====================
> 布尔型属性可以在声明时不赋值。XHTML 规范要求为其赋值，但是 HTML5 规范不需要。
> 元素的布尔型属性如果有值，就是 true，如果没有值，就是 false。
> 简单来说，就是不用赋值。

```
<input type="text" disabled> 

<input type="checkbox" value="1" checked>  

<select>   
  <option value="1" selected>1</option> 
</select> 
```


