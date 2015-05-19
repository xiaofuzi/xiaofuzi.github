---
   layout: post
   title: Javascript编写风格指南
---

#javascript编写风格指南

##目录

* 命名风格
* 代码格式化
* 注释

##命名风格

包括全局变量，局部变量，类变量，函数参数等的命名；

###变量命名规范
变量命名使用有意义的单词和驼峰式命名。

* 临时变量简写：str,num,bol,fun,arr。
* 循环变量简写：i , j , k。

###全局变量及常量规范
全局变量使用g作为前缀，如gUserName , gLoginTime。

常量全部字母都大写，如： PI , COPYRIGHT。注:常量可存在于函数中，也可存在于全局。

###函数命名规范
1.统一使用动词或动词加名词的形式。如getVersion() , submitForm()。

2.涉及返回逻辑值的函数可以使用is , has 等表示逻辑的词语代替动词。
内部函数前加上 '_'前缀。

3.可选参数以 'opt' 开头.

###类的命名

* 类名首字母大写。
* 属性名为具有一定意义的名词。私有属性加 "_"。
* 方法名为有意义的动词[+名词]，首字母小写。私有方法加 ‘_".

###对象方法命名
对象方法命名使用 "对象类名 + 动词[+ 名词]" 的形式。如addressGetEmail。Todo:考虑到对象名可能比较长,可以使用对象名的简写形式.

###事件响应函数
事件响应函数以 "触发事件对象名 + 事件名或者模块名 + 直接触发事件对象名 + 事件名" 的形式。如：
divClick() , addressSubmitButtonClick()。

###Getters 和 Setters
Getters 和 setters 并不是必要的. 但只要使用它们了, 就请将 getters 命名成 getFoo() 形式, 将 setters 命名成 setFoo(value) 形式. (对于布尔类型的 getters, 使用 isFoo() 也可.)
###其它

* 命名无特殊情况，请使用英语表示。切勿用汉语拼音。
* 变量名应该明确必要，避免容易混淆的缩写。
* 应该避免双重否定意义的变量，例如：bIsNotError, bIsNotFound，不可取。
* 变量的生命周期保持可用范围最小。
* 循环变量在循环中定义。
* 避免在条件中执行语句。
* 重复使用的具有相同意义的数字，用变量代替。

注：window对象中只可以定义全局变量，常量，类。

###文件名
文件名应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式. 文件名以.js结尾, 不要包含除 - 和 _ 外的标点符号(使用 - 优于 _).

###命名空间
为避免全局命名的冲突,在全局作用域上使用一个与项目或文件相关的名字来划分作用域空间.

如:
  
     var sloth = {};
     sloth.sleep = function() {
       ...
     };

###对于名字很长的变量可使用别名,仅限于函数块作用域中.

     /**
      * @constructor
      */
     some.long.namespace.MyClass = function() {
     };

     /**
      * @param {some.long.namespace.MyClass} a
      */
     some.long.namespace.MyClass.staticHelper = function(a) {
       ...
     };

     myapp.main = function() {
       var MyClass = some.long.namespace.MyClass;
       var staticHelper = some.long.namespace.MyClass.staticHelper;
       staticHelper(new MyClass());
     };


##代码格式化

###大括号

     //good way
     if (something) {
       // ...
     } else {
       // ...
     }
     //bad
     if(something)
     {
         //...
     }
     else
     {
         //...
     }

###数组和对象的初始化
如果初始值不是很长,写在一行.

var arr = [1, 2, 3];  		//'['之后无空格,']'之前无空格. 

var obj = {a: 1, b: 2, c: 3};  	//'{'之后无空格,'}'之前无空格. 

数组和对象多行初始化以及字符串跨越多行的情况.被拆分的行需要按统一的缩进对齐.

###空行
使用空行来划分一组逻辑上相关联的代码片段.

     doSomethingTo(x);
     doSomethingElseTo(x);
     andThen(x);

     nowDoSomethingWith(y);

     andNowWith(z);

###符号

* 单引号优先于双引号.
* 标点符号前后使用空格.

##注释
###顶层/文件注释

顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西. 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息. 如下:

     
     /**
      * @fileoverview Description of file, its uses and information
      * about its dependencies.
      * @author user@xxx.com
      */

###类注释

每个类的定义都要附带一份注释, 描述类的功能和用法. 也需要说明构造器参数. 如果该类继承自其它类, 应该使用 @extends 标记. 如果该类是对接口的实现, 应该使用 @implements 标记.

     /**
      * Class making something fun and easy.
      * @param {string} arg1 An argument that makes this more interesting.
      * @param {Array.<number>} arg2 List of numbers to be processed.
      * @constructor
      * @extends {goog.Disposable}
      */
     project.MyClass = function(arg1, arg2) {
       // ...
     };
     goog.inherits(project.MyClass, goog.Disposable);



