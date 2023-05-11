## 1.双向绑定原理

vue2的双向绑定原理是使用  object.definproperty和发布订阅者模式构成的

vue3则是使用了 proxy



## 2.computed 与 watch区别

computed： 

1.有缓存（有依赖项  依赖项不发生改变，将不会发生变化）

2.避免使用垃圾代码处理data数据

3.性能要好于 methods实现的方法 （不会每一次都会使用）

4.只要所依赖的相应数据不是频繁变化，开销不大的时候，就是用**计算属性**，反之用**监听器**；

watch:

- 用于侦听变化较为频繁，开销较大的数据；

总结: watch适合监听频繁更新 开销较大的数据  computed反之

## Vue的父组件和子组件生命周期钩子执行顺序是什么

1.加载渲染过程

父`beforeCreate` -> 父created -> 父beforeMount -> 子beforeCreate -> 子 created ->子 beforeMount -> 子 mounted -> 父mounted

2.子组件更新过程

父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated 

3.父组件更新过程 `父beforeUpdate->父updated`

4.销毁过程 `父beforeDestroy->子beforeDestroy->子destroyed->父destroyed`

## key的作用

https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/1

key的作用是为了在diff算法执行时更快的找到对应的节点，提高diff速度

vue 和 react 都是采用 diff 算法来对比新旧虚拟节点，从而更新节点。

js call 实现原理

修改this指向，传递参数

 , foreach map 区别, vue2 , 3 , vue2 直接修改数组里的一个元素 会不会更新到页面, webpack loader plugin 区别, 优化过吗, dva 数据流向 有啥api?

## vue2 , 3 , vue2 直接修改数组里的一个元素 会不会更新到页面

这是vue设计的原因 如果给所有的元素都加上双向绑定会 降低页面性能

在 Vue2 中源码 Observer 类中对**数组进行了过滤**，不调用 walk()，就是说**不对数组进行监控**，和defineProperty无关。根据尤大在issue上面的回答过滤掉数组的原因是 性能代价和获得的用户体验收益不成正比。可能是担心如果数组长度几千上万，性能消耗太大


vue团队给了 vue.set(vm.items, indexOfItem, newValue)

vm.items.splice(indexOfItem, 1, newValue)

来修改数组里的一个元素





优化图片加载顺序



## vue3.2与vue2.X 双向绑定响应式原理区别

1.性能提升 

​	提升速度  减少内存消耗

vue2双向绑定原理:

https://juejin.cn/post/7017327623307001864

vue 通过使用双向数据绑定，来实现了 View 和 Model 的同步更新。

vue 的双向数据绑定**主要是通过使用数据劫持和发布订阅者模式来实现的**。

首先我们通过 Object.defineProperty() 方法set和get来对 Model 数据各个属性添加访问器属性，以此来实现数据的劫持。

我们 依据发布订阅者 可以实现一个**订阅者收集器Dep**收集很多订阅者 Watcher（订阅者有很多） ，将这个订阅者加入这个属性主题的订阅者列表（订阅者收集器中）中。然后再监听器和订阅者之间进行统一管理）（收集依赖）

当 Model 层数据（属性）发生改变的时候，Model 作为发布者向收集器发出通知，主题（收集器）收到通知再向它的所有订阅者推送，订阅者收到通知后更改自己的数据

数据更改时发布消息给订阅者 触发响应的监听回调

vue3双向绑定原理:

用proxy代替了 object.defineproperty()来实现对数据的劫持

通过 `track` **收集依赖**，通过 `trigger` 触发更新，本质上就是用 WeakMap，Map，Set 来实现

