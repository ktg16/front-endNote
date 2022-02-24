# React面试题

rcc快速创建代码

## 什么是虚拟dom？

js对象

重新渲染js对象结构

为什么会用到虚拟对象 

 ![image-20210608160111584](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210608160111584.png)

## diff算法

（需要哪些dom，书写js对象对dom节点描述 用到哪些属性就对js对象上进行属性进行操作）是对js对象进行处理的 2.还解决跨平台dom问题

3.利用jsx语法来在render中创建dom 

react16 通过babel-loader转译后 变为React.createElement

react17

![image-20210608161322447](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210608161322447.png)

1.说一下对React的理解  及特性？

React是用于构建用户的JavaScript库 主要作用于ui层

开发者不再需要关心界面时如何渲染的，只要关心数据的生成和传递，这大大提高的开发者的开发效率，节省了开发时间

# React进阶

组件本质上就是类和函数，但是与常规的类和函数不同的是，**组件承载了渲染视图的 UI 和更新视图的 setState 、 useState 等方法**。React 在底层逻辑上会像正常实例化类和正常执行函数那样处理的组件。

## **调用 super(props) 的目的是什么**

Super（）调用父类的构造方法，有 super，组件才有自己的 this，在组件全局中都可 

以使用 this，如果只是 constructor 而不执行 super，之后的 this 都是错的，super 

继承父组件的 this