[TOC]

# JS总结

## 严格模式（‘use strict’）
    优点：消除js语法中的不合理、不严谨之处，减少怪异行为，提高运行速度
    * 不能修改arguments变量；
    * 禁止使用with语句；
    * 禁止使用delete操作var定义的变量；
    * 对象属性名不能重复,函数的参数不能重复
    * 禁止八进制表示法
    * 增加了新的保留字
    * this不能指向全局变量

## js实现继承 
* 原型链继承  
  function Parent() {}
  function Child() {}
  Child.prototype = new Parent()  缺点：子类区别于父类的属性和方法要在Sub.prototype = new Base();这样的语句之后分别执行，无法被包装到Sub这个构造器里面去；优点：实例既是父类的实例又是子类的实例
* 原型继承
  Child.prototype = Parent.prototype
  Child.prototype.constructor = Child 缺点：在子类原型对象中拓展一些属性的话，父类原型对象也会被修改
* 实例继承
  var Base = function()  
    {  
        this.level = 1;  
        this.name = "base";  
        this.toString = function(){  
            return "base";
        };
    };
  Base.CONSTANT = "constant";
  var Sub = function()
  {  
    var instance = new Base();  
    instance.name = "sub";  
    return instance;  
  };



## promise
    promise的三个阶段：Fulfilled（成功），Rejected（失败），Pending（创建阶段）
## promise的缺点
    1.promise无法取消，一旦建立就必须执行完成
    2.必须设置回调函数，不设置回调函数内部会抛出错误
    3.pending状态，也就是执行状态中无法追踪，不能得知目前进展到哪个阶段

## call,apply,bind的异同点，不支持bind的情况下如何写polyfill    
三者都是用来改变this指向的
call和apply是对函数进行直接调用，bind方法的返回值仍然是一个函数，需要加括号才能进行调用
```
    xw.say.call(xh);   xw.say.apply(xh); xw.say.bind(xh)()
```
## Event loop

## 跨域解决方案

## jsonp实现原理
利用script的src属性来实现跨域，将前端方法作为参数传递到服务器，，然后由服务器注入参数后返回，只支持get方法

## 使用reduce实现map

## map和forEach的区别
    map不改变原数组返回新的数组
    forEach不改变原数组，无返回值
## for in for of的区别
for－in遍历的对象的属性键值，for－of遍历的对象的元素

## call 为什么比apply要快
call 方法的参数格式正是内部方法所需要的格式

## currentTarget vs target
target 是鼠标点击的目标，触发事件的某个对象；currentTarget是当前事件活动的对象，绑定事件的对象

## 
# ES6

## 箭头函数的优点
    this指针的指向问题
this的指向是由函数定义的位置决定，而不是在使用它的地方，而且this的值在整个函数生命周期内是保持不变的，也无法通过call bind apply来改变
## 箭头函数如何获取参数，什么时候不能使用箭头函数
箭头函数无法通过arguments获取参数，必须使用命名参数或者rest参数
剩余参数只包含那些没有对应形参的实参，而 arguments 对象包含了传给函数的所有实参。
## generator的返回值
返回一个指针对象。整个generator就是一个封装的异步任务，
## 那些对象或者数据类型中有iterator及其实现
## 顺序发送多个请求使用generator
## function的scope属性
任何函数定义的时候都会创建一个[[scope]]属性，这个属性对应的是一个对象的列表，列表中的对象仅能javascript内部访问，无法通过语法访问；这个列表是在函数被创建的作用域对象的集合
### javascript作用域的执行过程
- 任何执行上下文时刻的作用域，都是由作用域来实现的
- 在一个函数被定义的时候会将它定义时刻的scope chain链接到这个函数[[scope]]属性中
- 在一个函数被调用的时候，会创建一个**活动对象**（也就是一个对象），然后对于每一个函数的形参，都命名为这个**活动对象**的**命名属性**，然后将这个活动对象作为此时作用域链的最前端，并将这个活动对象的[[scope]]加入到scope chain中


## object和map的区别
二者都是按键存取一个值，都可以删除键，都可以查看某个键名是否绑定了值
区别：对象通常有自己的原型，也就是有一个prototype键
    对象的键值只能是string或者symbol，但是map的键可以是任意值
    可以通过size很容易确定map中含有键值对的个数
## cookie和session的区别
session是在服务端保存的一种数据结构，用来跟踪用户的状态，这个数据可以保存在集群、数据库，文件中
cookie是客户端保存用户信息的一种机制，用来记录一些用户信息，也是实现session的一种方式
session是依赖于session if，但是session id 是存储在cookie中的，如果浏览器禁止了cookie，那么session也会失效
## ES6中object的新方法
object.assign对象合并  object.is判断两个对象是否相等  Object.setPrototypeOf()，Object.getPrototypeOf()用于设置和读取一个对象的prototype属性
## new的时候发生了什么？函数中的this是什么时候绑定的？如果在构造函数中加入return会怎么样？

## 实现简单的jquery链式调用

# HTML 
## cookie,seesionStorage,LocalStorage区别
    cookie：默认是关闭浏览器后失效，由服务器生成，可设置失效时间（_cookie的清除：手动设置cookie的键值对后面的expires为当前时间_）
    localStorage：只能手动删除数据，数据大小为5M
    sessionStroage：只在当前页面有效，关闭页面或者浏览器时失效

# 浏览器
## 304实现原理
    浏览器跟服务器之间过了一次确认资源时效的请求，协商缓存

## http缓存机制
    当用户发起一个静态资源的请求时，浏览器会通过一下几步来获取资源，
    * 本地缓存：现在本地查找该资源，如果发现该资源还没过期就使用该资源
    * 协商缓存：如果在本地缓存中找到对应的资源，但是不知道该资源是否已经过期，发送一个http 请求，让服务器来判断这个请求，如果这个请求的资源没有改动过，返回304，让浏览器使用本地找到的那个资源
    * 缓存失败：当服务器发现请求的资源已经修改过，或者这是一个新的请求，服务器则返回该资源的数据，并且返回200

## 网络安全
    * XSS：跨站脚本攻击
    * CSRF：跨站请求伪造

## http请求数量限制，同域及不同域

## http请求资源放在不同域下的好处
1.CDN缓存更方便
2.突破浏览器的并发限制
3.cookieless节省带宽，同时产生安全隔离，防止窃取cookie
4.
## 上一个问题导致的问题以及如何解决

## js异步加载 async defer区别
async异步记载并执行
defer异步加载，最后执行

## 异步组件
    resolve
## webpack配置

## 浏览器渲染
1. 浏览器把获取到的HTML代码解析成1个DOM树，HTML中的每个tag都是DOM树中的1个节点，根节点就是我们常用的document对象。DOM树里包含了所有HTML标签，包括display:none隐藏，还有用JS动态添加的元素等。
2. 浏览器把所有样式(用户定义的CSS和用户代理)解析成样式结构体，在解析的过程中会去掉浏览器不能识别的样式，比如IE会去掉-moz开头的样式，而FF会去掉_开头的样式。
3. DOM Tree 和样式结构体组合后构建render tree, render tree类似于DOM tree，但区别很大，render tree能识别样式，render tree中每个NODE都有自己的style，而且 render tree不包含隐藏的节点 (比如display:none的节点，还有head节点)，因为这些节点不会用于呈现，而且不会影响呈现的，所以就不会包含到 render tree中。注意 visibility:hidden隐藏的元素还是会包含到 render tree中的，因为visibility:hidden 会影响布局(layout)，会占有空间。根据CSS2的标准，render tree中的每个节点都称为Box (Box dimensions)，理解页面元素为一个具有填充、边距、边框和位置的盒子。
4. 一旦render tree构建完毕后，浏览器就可以根据render tree来绘制页面了。
## 回流(reflow)和重绘(repaint)：
    当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候。在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘（repaint）。浏览器为了减少重绘和回流会维护一个队列，将重绘和回流合并，但是某些属性会强制浏览器flush队列，1. offsetTop, offsetLeft, offsetWidth, offsetHeight2. scrollTop/Left/Width/Height3. clientTop/Left/Width/Height4. width,height5. 请求了getComputedStyle(), 或者 IE的 currentStyle
## 提高渲染效率的方法：
    1.减少访问会引起浏览器flush队列的属性，如果你确实要访问，利用缓存，就是存储为一个变量；
    2.直接改变className，如果动态改变样式，则使用cssText


# js编程题目
## 数组随机顺序排序
## 深拷贝
## 对象继承

## 数组加逗号间隔符

## 有序数组合并

# 面向对象编程思想
## 重载和多态


# 前端开发工具
## 对webpack grunt gulp工作原理的理解


# HTTP 

## 网络状态码

## http请求头组成



# jQuery
## 原生实现Ajax请求

## jQuery自定义拓展



# 情境题

## 获取页面的所有标签，并判断有多少种标签

## 给页面中插入100行li，如何插入比较好

# 模块化

## cmd amd es6 node模块化比较

# js

## 垃圾回收机制

## c和js数组存储的不同
    js数组是在内存中存放引用，也就是数组的在堆中的内存地址
    c语言数组是在内存中一块连续的地址中存放，大小固定，在内存中是连续的


# node
## node 新建子进程的方式
1.exec新建子进程，接受一个命令字符串：var exec = require('child_process').exec;
2.execSync新建子进程，第一个参数是所要执行的命令，第二个参数用来配置执行环境 var execSync = require("child_process").execSync;
3.execFile新建子进程，方法直接执行特定的程序，参数作为数组传入，不会被bash解释，因此具有较高的安全性
4.spawn新建一个子进程来执行特定命令，用法与execFile方法类似
5.fork直接创建一个子进程，执行node脚本。fork会在父进程与子进程之间建立一个通讯管道，用于进程间通信