# React 组件化

开课吧课堂地址 github.com/bubucuo/kkb-reaact/tree

## Context API

**context 跨层通信**

### **React.createContext** 

创建一个Context对象  使用此组件创建Provider  被包裹组件会匹配离自己最近的的Provider读取值

### **Context.Provider**

Provider 接收一个value属性   传递给被包裹的组件  允许被包裹组件订阅context的变化  provider可以实现  一对多  多对一(里层的会覆盖外层数据)的对应关系

### **useContext**（函数式跨层通信）

使用方法

useContext(ThemeContext)

接受一个Context对象 接受一个context对象(**React.createContext**的返回值 )并返回该context的当前值  

取决于Provider的value prop 函数组件 使用

<Usercontext.Consumer> 包裹  value值调用

### class.contextType

**类组件 需要使用  类名.contextType = Usercontext**

子组件的this.context就会有值

举例

新建两个页面

```
//创建context
const ThemeContext = React.createContext()  用于子组件
//创建Provider

const ThemeProvider = ThemeContext.Provider

//使用ThemeProvider将组件包裹起来 
return(
	<ThemeProvider value={theme}>
	<Page /> 组件
	</ThemeProvider>
)


//类子组件
类名.contextType = Usercontext


render(){
const {themeColor} = this.context

//函数子组件
还需要引入 ThemeContext
const ctx = useContext(ThemeContext)

return(
   {{ctx.themeColor}}
)
}




```

高阶组件-hoc





因为无状态组件其实就是一个函数（方法）,所以它的性能也比普通的`React`组件要好。