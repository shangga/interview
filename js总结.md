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

# ES6

## 箭头函数的优点
    this指针的指向问题
# CSS总结
## flex与传统布局的差异 
    传统的布局是基于css盒模型，依赖display＋position＋float等属性
    flex是弹性布局，为盒模型提供最大程度的灵活性
## transform
    所有的transform属性的参考位置都是元素中心点，可以通过transform-origin属性设置，默认值是50%，50%
    skew(): 相对于x轴，y轴的移动
    translate(): 从当前位置移动
    rotate(): 旋转角度
    scale(): 放大缩小
    matrix(): 所有的2D转换方法集合，包含数学函数，允许您：旋转、缩放、移动以及倾斜元素   

## 不定宽高元素的垂直水平居中
    transform：translate（－50%，－50%）；
    position：absolute；
    top：50%；
    left：50％；
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

## 上一个问题导致的问题以及如何解决

## js异步加载 async defer区别
async异步记载并执行
defer异步加载，最后执行


# React－Redux

    * connect方法实际接受四个参数，mapStateToProps和mapDispatchToProps，mergeProps，options选项。他们定义了UI组件的逻辑。mapStateToProps 负责 state 映射到 UI 组件的参数 props，mapDispatchToProps 负责用户对 UI 组件的操作映射成 Action。
    * mapStateToProps是一个函数，用于建立一个从（外部的）state 对象到（UI组件的）props对象的映射关系。mapStateToProps会订阅 Store，每当 state 更新的时候，会自动执行，重新计算 UI 组件的参数，从而触发 UI 组件的重新渲染。如果省略这个函数，UI组件就不会订阅store，store的更新也就不会引起UI组件的更新。
    * mapDispatchToProps 将 action 作为 props 绑定到组件上
    * mergeProps：，不管是 stateProps 还是 dispatchProps，都需要和 ownProps merge 之后才会被赋给组件。connect 的第三个参数就是用来做这件事。通常情况下，你可以不传这个参数，connect 就会使用 Object.assign 替代该方法。
    * provider组件：connect 方法生成容器组件后，需要容器拿到 state 对象，这样才能生成 UI 组件的参数。React-Redux 提供了 Provider 组件，可以让容器组件拿到 state。Provider 在根组件外面包一层，这样 App 的所以子组件就默认都可以拿到 state 了。
## 生命周期
    * getDefaultProps---> getInitState ----> componentWillMount ----> render ---->  componentDidMount
    * componentWillReceiveProps ---> shouldComponentUpdate ----> componentWillUpdate ----> render -----> componentDidUpdate
    * componentWillUnmount

## reactsetState的第二个参数的作用，发生在什么生命周期

## 受控组件，非受控组件

## ref的最新写法

## shouldComponentUpdate如何使用

# VUE 总结

## 生命周期
    beforecreate（初始化事件）---> created（完成数据观测，属性和方法的计算，watch／event事件回调）---> beforeMounted（render首次被调用）---> mounted (el被创建的vm.$el替换，并挂载到实例上去后调用，并不会保证所有子组件都会被挂载，如果希望整个视图都渲染完毕，可以使用vm.$nextTick替换mounted)---> beforeUpdate(数据更新时调用，发生在虚拟dom重新渲染和打补丁之前，可以在这个钩子函数中进一步更改状态，不会触发附加的重渲染过程) ---> updated（由于数据更改导致的虚拟dom重新渲染，会调用该函数，当这个函数被调用时，组件dom已经更新，所以可以执行依赖于dom的操作。在大多数情况下应该避免在此期间更改状态，可以通过计算属性和watcher取代）---> activated（keep－alive激活时调用）---> deactivate（keep－alive组件停用时调用）---> beforeDestroy（实例销毁之前调用，在这一步，实例仍然完全可用）---> destroyed（实例销毁之后调用，调用后，vue实例所指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁）
## 双向绑定实现原理
    使用数据劫持结合发布者－订阅者模式的方式，通过Object.defineProperty来劫持各个属性setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调，将需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter，这样的话，给这个对象的某个值赋值，就会触发setter，就监听到了数据变化。
## MVVM模式
    以数据为驱动，将DOM和数据进行绑定，一旦创建绑定，DOM和数据同步。view－model是vue的核心DOMListeners和DataBindings是实现双向绑定的关键。DOMListeners监听页面所有View层DOM元素的变化，当发生变化，Model层的数据随之变化；DataBindings监听Model层的数据，当数据发生变化，View层的DOM元素随之变化。
## v-show和v－if的区别
    v－show是修改元素的display属性控制元素显示或隐藏
    v－if是直接销毁或者重建DOM达到显示或隐藏的效果

## keep-alive作用
    缓存不活动的组件实例，主要用于缓存组件状态或者避免重新渲染

## vue引入组件的步骤
    1.采用ES6 import方法引入组件，或者使用commomjs的方法require
    2.注册组件；
    3.使用组件

## method computed watcher
    method无论何时都会执行，computed只在依赖的数据发生变化时才会执行，watcher类似
    当需要定义一个依赖于其他属性的属性时，可以使用computed，watcher适用于一个属性改变引起其他操作

## 事件
    vm.$on(): 监听当前实例上的自定义事件，事件可以由vm.$emit触发，回调函数会接收所有传入事件触发函数的额外参数
    vm.$once(): 监听一个自定义事件，但是只触发一次，在第一次触发以后移除监听器
    vm.$off(): 移除自定义监听事件，如果没有参数，则移除全部事件监听器
    vm.$emit(): 触发当前实例上的事件。
    vm.$nextTick(): 将回调延迟到下次don更新循环之后执行。在修改数据之后立即使用然后等待dom更新。
## vuex
    vuex可以看作是项目所有组件的数据中心，我们将组件中共享的state抽离出来，任何组建都可以访问和操作我们的数据中心
    state中保存数据，
    改变state中的数据有且只有通过mutation中方法，且mutation中的方法必须是同步的
    如果要写异步方法，需要写在actions中，并通过commit到mutations中进行state数据的更改
    getter：有时候我们需要从store中派生出一些状态，如果多个组件需要用到这个属性，要么复制这个函数，要么抽取到一个共享函数中然后再多处导入，但是这两种方式都不太理想，vuex允许我们在store中定义getters，可以认为是store的计算属性，getters的返回值会根据它的依赖被缓存起来，只有当它的依赖值发生了改变才会被重新计算。
    mutations：更改store中状态的唯一方法就是提交mutations， mutations 非常类似于事件，每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。不能直接调用mutation handler，更像是事件注册，当触发一个类型为特定type的mutation时触发一个函数。
    actions：actions类似与mutations，与之不同的是action提交的是mutations，而不是直接变更状态，action可以包含任意异步操作；action通过dispatch触发；action支持同样的载荷方式和对象方式进行分发
    modules：由于使用单一状态树，应用的所有状态会集中到一个比较大的对象，当应用变的非常复杂时，store对象就有可能变得相当臃肿，所以vuex允许我们将store分割成模块（module），每个模块拥有自己的state，mutation，action，getter，甚至是嵌套子模块；
## vue－router
    动态路由，
    获取路由参数：参数值会设置到this.$route.params,使用冒号作为标记
    嵌套路由：
    route.push:想要导航到不同的URL可以使用router.push方法，这个方法会向history中添加一个新的记录，<router-link :to="..."> 等同于调用 router.push(...)
    编程式导航：router.push router.replace router.go
    命名视图：router－view 添加name属性
    导航钩子函数：router.beforeEach（to，from，next） 确保要调用 next 方法，否则钩子就不会被 resolved。
    路由独享的钩子函数：beforeEnter，beforeLeave
    如何监听路由变化：通过监听hashchange事件，在router.init中调用的。router是在注入vue的过程如下：
                    new Vue()
                    执行 vue-router 注入的 beforeCreate 钩子函数
                    执行 router.init(vm)
                    执行 history.setupListeners()，注册事件监听
    地址变更影响到视图更新：当视图更新进一步调用到 <router-view> 的 render() 时，即进入了 <router-view> 的处理
    <router-view> 作为根组件下的子组件，从根组件那里可以获取到当前的路由对象，进而根据路由对象的组件配置，取出组件并用其替换当前位置的内容。这样，也就完成整个路由变更到视图变更的过程。
    路由模式：hash模式，history模式。 通过设置mode参数指定。hash是监听的hashchange方法，history是监听的history变化，利用pushState(), replaceState()方法，浏览器是否支持是通过变量supportsPushState来检查的。
## 插槽
    slot插槽：单个插槽，具名插槽，作用域插槽
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
4.spawn新建一个子进程来执行特定命令，用法与xecFile方法类似
5.fork直接创建一个子进程，执行node脚本。fork会在父进程与子进程之间建立一个通讯管道，用于进程间通信