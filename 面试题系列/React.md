1.super() 和 constructor()的含义

### 1.redux包含哪几部分? 有什么作用

action  通过dispatch传递数据

store是把 action和reducer联系在一起的一个对象 维持应用的 state；

提供 getState() 方法获取 state；
 提供 dispatch(action) 方法更新 state；
 通过 subscribe(listener) 注册监听器;
 通过 subscribe(listener) 返回的函数注销监听器。
 通过replaceReducer(nextReducer)可以替换掉当前的reducer

reducer  通过传递过来的action 修改state 但是不能直接修改 需要声明newState return 给store重新createStore

### 2.展示组件和容器组件区别

展示组件

1. 1.包含展示组件和容器组件  
2. 2.常包含this.props.children   仅仅通过props接收数据和回调
3. 3.除了包括状态更新、有生命周期的hook、或者性能优化，通常只是一个纯函数（无状态的组件） 

容器组件

建议开始写app的时候只写 展示组件（莫非这个叫做view?） 最终你会发现你在组件之间传递了太多的props，你会发现很多组件接收到组件，他们不用只是转发，当孩子需要更多数据时，你必须重新连接所有这些中间组件。

这是一个持续优化的过程，你慢慢会从中直观的提取一些容器组件出来。就像你知道什么时候提取一个函数一样。



不用把 展示组件和容器组件分割当做一个教条。有时候很难划分界限，如果你不确定一个组件是展示还是容器组件，就别分了。

1.注重逻辑，关注事物工作

2.通常没有html标签，几乎不会出现style

*提供数据和行为给展示组件或者其他的容器组件*