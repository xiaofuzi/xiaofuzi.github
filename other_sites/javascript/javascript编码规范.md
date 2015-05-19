---
   layout: post
   title: Javascript编码规范
---

#Javascript编码规范

##目录

* 类型
* 对象
* 数组
* 字符串
* 函数
* 属性
* 变量
* 条件表达式
* 块
* 构造器
* 方法返回值(this)
* 事件
* 模块

###类型

* 原始值：按值传递
    string/number/boolean/null/undefined
    注:null和undefine是不同的.

* 复杂类型：按引用传递
    object/array/function

###对象

    使用字面值创建对象
    //bad
    var item = new Object();
    //good
    var item = {};

    不要使用保留字作为键
    //bad
    var superman = {
        class:'superhero',
        default:{ clark:'kent' },
        private: true
    }

    //good
    var superman = {
        klass: 'superhero',
        defaults:{ clark: 'kent' },
        hidden:true
    };

###数组：

    使用字面量创建数组
    //bad
    var items = new Array();

    //good
    var items = [];

    数组长度不知时，使用push添加元素
    var someStack = [];
    //bad
    someStack[someStack.length] = 'abcdefg';

    //good
    someStack.push('abcdefg');

    使用slice拷贝数组
    var len = items.length,
            itemsCopy = [],
            i;
    //bad
    for(i = 0; i < len; i++){
        itemsCopy[i] = items[i];
    }
    //good
    itemsCopy = items.slice();

###字符串

    对字符串使用单引号''
    //bad
    var name = "Bob Parr";

    //good
    var name = 'Bob Parr';

    编程时使用join而不是字符串连接来构建字符串：
    var items,
            messages,
            length, i;
    messages = [{
        state: 'success',
        message: 'This one worked.'
        },{
        state: 'success',
        message:'This one worked as well.'
        },{
        state:'error',
        message: 'This one did not work.'
        } ];
        length = messages.length;
        //bad
        function inbox(messages){
            items = '<ul>';
            for(i = 0;i < length; i++){
                items += '<li>' + messages[i].message + '</li>';
            }
        return items + '</ul>';
        }

        //good
        function inbox(messages){
            items = [];
            for(i = 0; i < length; i++){
                items[i] = messages[i].message;
            }
            return '<ul><li>' + items.join('</li><li>')+'</li></ul>';
        }

###函数表达式：

        //匿名函数表达式
        var anonymous = function(){
            return true;
        };
        //有名函数表达式
        var named = function named(){
            return true;
        };

        //立即调用函数表达式
        (function(){
            console.log('Welcome to the internet. Please follow me.');
        })();

不要在一个非函数块里面声明一个函数，应该把那个函数赋给一个变                 量。浏览器让你这么做，但是解析的情况是不同的。

        //bad
        if(currentUser){
            function test(){
                console.log('Nope.');
            }
        }

        //good
        if(currentUser){
            var test = function test(){
                console.log('Yup.');
            };
        }

请勿把参数命名为 arguments,这会对函数内的 arguments对象产生影响。

        //bad
        function nope(name, options, arguments){
            //.....stuff....
        }
        //good
        function yup(name, options, args){
            //...stuff.....
        }

###属性：

当使用变量访问属性时使用中括号。

        var luke = {
            jedi: true,
            age: 28
        };
        function getProp(prop){
            return luke[prop];
        }
        var isJedi = getProp('jedi');

###变量：
总是使用var 来声明变量，避免产生全局变量，污染全局命名空间。
       
        //bad
        superPower = new SuperPower();

        //good
        var superPower = new SuperPower();
        
使用一个var以及新行声明多个变量，缩进四个空格

        //bad
        var items = getItems();
        var goSportsTeam = true;
        var dragonball = 'z';

        //good
        var items = getItems(),
            goSportsTeam = true,
            dragonball = 'z';

最后再声明未赋值的变量
        
        //bad
        var i, len, dragonball,
            items = getItems(),
            goSportsTeam = true;
        
        //bad
        var i, items = getItems(),
            dragonball,
            goSportsTeam = true,
            len;

        //good
        var items = getItems(),
            goSportsTeam = true,
            dragonball,
            length,
            i;

###条件表达式和等号

适当使用===和！==以及==和！=。
条件表达式的强类型转换规则：
        
* 对象被计算为true
* Undefined被计算为false
* Null被计算为false
* 布尔值被计算为布尔的值
* 数字如果是+0, -0,NaN被计算为false
* 字符如果是空字符串，则被计算为false，否则为true
* 字符串如果是空字符串，则被计算为false，否则为true

###块的使用
给所有多行的块使用大括号

        //bad
        if(test)
            return false;
        //good
        if(test)   return false;

        //good
        if(test){
         return false;
        }

        //good
        function(){
            return false;
        }

###构造器
给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会是继承出现问题。

        function Jedi(){
            console.log('new jedi');
        }
        //bad
        Jedi.prototype = {
            fight: function fight() {
                console.log('fighting');
        },
        block: function block(){
            console.log('blocking');
        }
    };

    //good
    Jedi.prototype.fight = function fight(){
        console.log('fighting');
    };
    Jedi.prototype.block = function block(){
        console.log('blocking');
    };

方法可以返回this帮助方法链
    
    //bad
    Jedi.prototype.jump = function(){
        this.jumping = true;
        return true;
    };
    Jedi.prototype.setHeight = function(height){
        this.height = height;
    };

    
    var luke = new Jedi();
    luke.jump();   //true
    luke.setHeight(20)  //undefined
    
    //good
  Jedi.prototype.jump = function() {
        this.jumping = true;
        return this;
    };

    Jedi.prototype.setHeight = function(height){
        this.height = height;
        return this;
    }
    luke.jump()
        .setHeight(20);    //实现方法链调用

    自定义toString()方法，但需确保不会有副作用
    function Jedi(options){
        options || (options = {});
        this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName(){
        return this.name;
    };
    Jedi.prototype.toString = function toString(){
        return 'Jedi - ' + this.getName();
};

###事件
当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据
里而不用找出并更新那个事件的事件处理器。

    //bad
    $(this).trigger('listingUpdated', listing.id);
    $(this).on('listingUpdated', function(e,listingId){
        //do something with listingId
    });

    //good
    $(this).trigger('listingUpdated', {listingId: listing.id});

    $(this).on('listingUpdated', function(e, data){
        //do something with data.listingId
    });

###模块
模块应该以 ';' 开始，这保证了如果一个有问题的模块忘记包含最后的分号在合并后刽出现错误。
这个文件应该以驼峰命名，并在同名文件夹下，同时导出的时候名字一致。
加入一个名为noConflict()的方法来设置导出的模块为之前的版本并返回它。
总在模块顶部声明 'use strict';

     ;function(global) {
       'use strict';

       var previousFancyInput = global.FancyInput;

       function FancyInput(options) {
         this.options = options || {};
       }

       FancyInput.noConflict = function noConflict() {
         global.FancyInput = previousFancyInput;
         return FancyInput;
       };

       global.FancyInput = FancyInput;
     }(this);














         