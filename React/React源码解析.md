# React 组件化

开课吧课堂地址 github.com/bubucuo/kkb-reaact/tree

## Context API

**context 跨层通信**

### **React.createContext** 

创建一个Context对象  使用此组件创建Provider  被包裹组件会匹配离自己最近的的Provider读取值

### **Context.Provider**

Provider 接收一个value属性   传递给被包裹的组件  允许被包裹组件订阅context的变化  provider可以实现  一对多  多对一(里层的会覆盖外层数据)的对应关系





两种引入方式

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

const ThemeProvider = ThemeContext.Provider //供应者
theme:{
temmeColor:''
}
//使用ThemeProvider将组件包裹起来 
return(
	<ThemeProvider value={theme}>
	<Page /> 组件
	</ThemeProvider>
)


//1.类子组件
类名.contextType = ThemeContext或者 static contextType = MyContext;


render(){
const {themeColor} = this.context

//2.函数子组件
还需要引入 ThemeContext
const ctx = useContext(ThemeContext)

return(
   {{ctx.themeColor}}
)
}

3.Consumer组件 //消费者

<PriceContext.Consumer>
{
	theme=>	<div>{theme}</div>
}
</PriceContext.Consumer>


```

存在一个替换方案

https://react.docschina.org/docs/context.html

```
function Page(props) {
  const user = props.user;
  const content = <Feed user={user} />;
  const topBar = (
    <NavigationBar>
      <Link href={user.permalink}>
        <Avatar user={user} size={props.avatarSize} />
      </Link>
    </NavigationBar>
  );
  return (
    <PageLayout
      topBar={topBar}
      content={content}
    />
  );
}
```

有的时候在组件树中很多不同层级的组件需要访问同样的一批数据。Context 能让你将这些数据向组件树下所有的组件进行“广播”，所有的组件都能访问到这些数据，也能访问到后续的数据更新。使用 context 的通用的场景包括管理当前的 locale，theme，或者一些缓存数据，这比替代方案要简单的多。

