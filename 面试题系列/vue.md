本文借鉴于 https://mp.weixin.qq.com/s/h2H-36iVeoyXsorZChwxyQ

### vue跟React异同点？

1.都使用虚拟化dom

2.组件化开发

3.单向数据流 

4.都支持服务端渲染

不同

1.React的jsx 以及Vue的template   react是一个ui库    vue渐进式框架

2.状态变化 react使用setState     Vue自动  

3.React单向绑定  Vue双向绑定

4.状态管理React的Redux Vue的vuex

### MVVM是什么和MVC？

MVC

- Model(模型)：负责从数据库中取数据
- View(视图)：负责展示数据的地方
- Controller(控制器)：用户交互的地方，例如点击事件等等

控制器将Model数据展示在View视图上

VM：也就是View-Model，做了两件事达到了数据的双向绑定 一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据。实现的方式是：DOM 事件监听。

也就是当 Model 的属性改变时，我们不用再自己手动操作 Dom 元素，来改变 View 的显示，而是改变属性后该属性对应 View 层显示会自动改变

###  为什么data是个函数并且返回一个对象呢？

`data`之所以只一个函数，是因为一个组件可能会多处调用，而每一次调用就会执行`data函数`并返回新的数据对象，这样，可以避免多处调用之间的`数据污染`。

### 8. 使用过哪些Vue的修饰符呢

完整地址： https://juejin.cn/post/6981628129089421326#comment



![640](.\640.webp)

一定要常用

1.sync 父子组件传值可简写代码    

2.keyCode 限制某个按键的触发

```
例如

<input type='text' @keyup.tab='shout(4)'/> 按tab键触发
```

