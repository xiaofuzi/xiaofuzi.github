---
   layout: post
   title: Css编写风格指南
---

#css

##语法
============
1. 用四个空格来代替制表符（tab） – 这是唯一能保证在所有环境下获得一致展现的方法。
2. 为了获得更准确的错误报告，每条声明都应该独占一行。
3. 所有声明语句都应当以分号结尾
4. 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，box-shadow）
5. 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）。
6. 尽量使用简写形式的十六进制值，例如，用 #fff 代替 #ffffff。
7. 为选择器中的属性添加双引号，例如，input[type="text"]。只有在某些情况下是可选的，但是，为了代码的一致性，建议都加上双引号。

8. 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;。

<pre>
/* Bad CSS */ 
.selector, .selector-secondary, .selector[type=text] {   
  padding:15px;   
  margin:0px 0px 15px;   
  background-color:rgba(0, 0, 0, 0.5);   
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
} 
</pre>

<pre>
/* Good CSS */ 
.selector, 
.selector-secondary, 
.selector[type="text"] {   
  padding: 15px;   
  margin-bottom: 15px;   
  background-color: rgba(0,0,0,.5);   
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff; 
} 
</pre>


##声明顺序
============
>相关的属性声明应当归为一组，并按照下面的顺序排列：
>
>由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。
其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

1. Positioning
2. Box model
3. Typographic
4. Visual

<pre>
.declaration-order {   
  /* Positioning */   
  position: absolute;   
  top: 0;   
  right: 0;   
  bottom: 0;   
  left: 0;   
  z-index: 100;  
  
  /* Box-model */   
  display: block;   
  float: right;   
  width: 100px;   
  height: 100px;    

  /* Typography */   
  font: normal 13px "Helvetica Neue", sans-serif;   l
  ine-height: 1.5;   
  color: #333;   
  text-align: center;    

  /* Visual */   
  background-color: #f5f5f5;   
  border: 1px solid #e5e5e5;   
  border-radius: 3px;    

  /* Misc */   
  opacity: 1; 
} 
</pre>

##媒体查询（Media query）的位置
============================
>将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。下面给出一个典型的实例。

<pre>
.element { ... } 
.element-avatar { ... } 
.element-selected { ... }  
@media (min-width: 480px) {
    .element { ...}
    .element-avatar { ... }
    .element-selected { ... }
} 
</pre>

##带前缀的属性
============
>当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。

>在 Textmate 中，使用 Text → Edit Each Line in Selection (⌃⌘A)。在 Sublime Text 2 中，使用 Selection → Add Previous Line (⌃⇧↑) 和Selection → Add Next Line (⌃⇧↓)。

<pre>
/* Prefixed properties */ 
.selector {
  -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
          box-shadow: 0 1px 2px rgba(0,0,0,.15);
} 
</pre>

##单行规则声明
=============
>对于只包含一条声明的样式，为了易读性和便于快速编辑，建议将语句放在同一行。对于带有多条声明的样式，还是应当将声明分为多行。

>这样做的关键因素是为了错误检测 – 例如，CSS 校验器指出在 183 行有语法错误。如果是单行单条声明，你就不会忽略这个错误；如果是单行多条声明的话，你就要仔细分析避免漏掉错误了。

<pre>
/* Single declarations on one line */ 
.span1 { width: 60px; } 
.span2 { width: 140px; } 
.span3 { width: 220px; }  

/* Multiple declarations, one per line */ 
.sprite {   
  display: inline-block;   
  width: 16px;   
  height: 15px;   
  background-image: url(../img/sprite.png); 
} 
.icon           { background-position: 0 0; } 
.icon-home      { background-position: 0 -20px; } 
.icon-account   { background-position: 0 -40px; } 

</pre>

##简写形式的属性声明
=================
> 在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

* padding
* margin
* font
* background
* border
* border-radius

>大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

* 对于不太熟悉简写属性声明及其行为的用户很有用。

<pre>
/* Bad example */ 
.element {   
  margin: 0 0 10px;   
  background: red;   
  background: url("image.jpg");   
  border-radius: 3px 3px 0 0; 
}  

/* Good example */ 
.element {   
  margin-bottom: 10px;   
  background-color: red;   
  background-image: url("image.jpg");   
  border-top-left-radius: 3px;   
  border-top-right-radius: 3px; 
} 
</pre>

##Less 和 Sass 中的嵌套
======================
>避免非必要的嵌套。这是因为虽然你可以使用嵌套，但是并不意味着应该使用嵌套。只有在必须将样式限制在父元素内（也就是后代选择器），并且存在多个需要嵌套的元素时才使用嵌套

<pre>
// Without nesting 
.table > thead > tr > th { … } 
.table > thead > tr > td { … }  

// With nesting 
.table > thead > tr {   
  > th { … }   
  > td { … } 
} 
</pre>

##注释
======
>代码是由人编写并维护的。请确保你的代码能够自描述、注释良好并且易于他人理解。好的代码注释能够传达上下文关系和代码目的。不要简单地重申组件或 class 名称。

* 对于较长的注释，务必书写完整的句子；对于一般性注解，可以书写简洁的短语。

<pre>
/* Bad example */ 
/* Modal header */ 
.modal-header {   
  ... 
}  

/* Good example */ 
/* Wrapping element for .modal-title and .modal-close */ 
.modal-header {   
  ... 
} 
</pre>

##class id  命名
============
* class id 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class id 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
* class id 名称应当尽可能短，并且意义明确。
* 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
* 基于最近的父 class 或基本（base） class 作为新 class 的前缀。
* 使用 驼峰命名法 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。

在为 Sass 和 Less 变量命名是也可以参考上面列出的各项规范。

<pre>
/* Bad example */ 
.t { ... } 
.red { ... } 
.header { ... }  

/* Good example */ 
.tweet { ... } 
.important { ... } 
.tweet-header { ... }
</pre>

###常用id的命名：
(1)页面结构
* 容器: container
* 页头：header
* 内容：content/container
* 页面主体：main
* 页尾：footer
* 导航：nav
* 侧栏：sidebar
* 栏目：column
* 页面外围控制整体布局宽度：wrapper
* 左右中：left right center

(2)导航

* 导航：nav
* 主导航：mainbav
* 子导航：subnav
* 顶导航：topnav
* 边导航：sidebar
* 左导航：leftsidebar
* 右导航：rightsidebar
* 菜单：menu
* 子菜单：submenu
* 标题: title
* 摘要: summary

(3)功能

* 标志：logo
* 广告：banner
* 登陆：login
* 登录条：loginbar
* 注册：regsiter
* 搜索：search
* 功能区：shop
* 标题：title
* 加入：joinus
* 状态：status
* 按钮：btn
* 滚动：scroll
* 标签页：tab
* 文章列表：list
* 提示信息：msg
* 当前的: current
* 小技巧：tips
* 图标: icon
* 注释：note
* 指南：guild
* 服务：service
* 热点：hot
* 新闻：news
* 下载：download
* 投票：vote
* 合作伙伴：partner
* 友情链接：link
* 版权：copyright

###常用class的命名：
(1)颜色:使用颜色的名称或者16进制代码,如
* .red { color: red; }
* .f60 { color: #f60; }
* .ff8600 { color: #ff8600; }

(2)字体大小,直接使用”font+字体大小”作为名称,如

* .font12px { font-size: 12px; }
* .font9pt {font-size: 9pt; }

(3)对齐样式,使用对齐目标的英文名称,如

* .left { float:left; }
* .bottom { float:bottom; }

(4)标题栏样式,使用”类别+功能”的方式命名,如

* .barnews { }
* .barproduct { }


##选择器
========
* 对于通用元素使用 class ，这样利于渲染性能的优化。
* 对于经常出现的组件，避免使用属性选择器（例如，[class^="..."]）。浏览器的性能会受到这些因素的影响。
* 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 。
* 只有在必要的时候才将 class 限制在最近的父元素内（也就是后代选择器）（例如，不使用带前缀的 class 时 – 前缀类似于命名空间）。

<pre>
/* Bad example */ 
span { ... } 
.page-container #stream .stream-item .tweet .tweet-header .username { ... } 
.avatar { ... }  

/* Good example */ 
.avatar { ... } 
.tweet-header 
.username { ... } 
.tweet 
.avatar { ... } 
</pre>

##代码组织
=========
* 以组件为单位组织代码段。
* 制定一致的注释规范。
* 使用一致的空白符将代码分隔成块，这样利于扫描较大的文档。
* 如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动。

<pre>
/*
 * Component section heading
 */
.element { ... }   
/*  
 * Component section heading  
 *  
 * Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.  
 */  

.element { ... }  

/* Contextual sub-component or modifer */ 
.element-heading { ... }
</pre>