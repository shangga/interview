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

## react setState的第二个参数的作用，发生在什么生命周期

## 受控组件，非受控组件

## ref的最新写法

## shouldComponentUpdate如何使用

## React 15 vs 16


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