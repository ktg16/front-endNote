   React 17 学习



**注意：** 组件名称必须以大写字母开头。

React 会将以小写字母开头的组件视为原生 DOM 标签。例如，`<div />` 代表 HTML 的 div 标签，而 `<Welcome />` 则代表一个组件，并且需在作用域内使用 `Welcome`。

setState修改对象状态

## react内联样式写法

```
<div style={{backgroundColor:context.background,border:'1px solid red'}} > </div>
```



## 1.什么是纯函数？

纯函数不会改变入参

**所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。**

## 2.不熟悉的点

默认事件 例：a.preventDefault

条件渲染

```js
//1.可以使用&&与进行条件渲染
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&   
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
true && expression 总是会返回 expression, 而 false && expression 总是会返回 false。

//2.可以使用三目运算符
{isLoggedIn ? 'currently' : 'not'}
//提取组件
{isLoggedIn
  ? <LogoutButton onClick={this.handleLogoutClick} />
  : <LoginButton onClick={this.handleLoginClick} />
 }
 
```

### //3.包含关系（v-slot）

```js
//v-slot 使用方法 https://cn.vuejs.org/v2/guide/components-slots.html#%E5%8A%A8%E6%80%81%E6%8F%92%E6%A7%BD%E5%90%8D
base-layout 组件
<header>
    <slot name="header"></slot>
</header>

<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>
//缩写
<template #footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>



// react 包含关系（props.children）
https://react.docschina.org/docs/composition-vs-inheritance.html
//也可以不使用props.children 可以自行约定：所需内容传入props使用相应prop
//
<div className="SplitPane-left">
        {props.left}
 </div>

 <SplitPane
      left={
        <Contacts />
      } />
          
//不一定非要写标签体
  //父组件
    <MyNavLink to='/context/about' title='about' >About</MyNavLink>      
  //子组件  MyNavLink(把props.children放进this.props)       
  <NavLink {...this.props} />   
	//相当于
  <NavLink  children={123}/> => <NavLink>123</Navlink>        
          
```







函数式setState和对象式setState

```

this.state = {count:0}
// 函数式

this.setState({count:this.state.count+1})
// 对象式
this.setState(state=>({this.state.count+1})
修改状态
this.setState(state=>({this.state.count+1}，()=>{console.log(this.state.count)})
```



## 3.修改state中的对象

```
state={
	list:{
		objA:{
			name:'A',
			age:20
		}
		objD:'D'
	}
}


//方法一  只作用于第一层
let data  = Object.assgin({},this.state.list,{objD:'D1'})
	this.setState({
		list:data
})
//方法二  作用于对象中的深层级和第一层级
 this.setState({
     list: {
         ...this.state.list,
          objA: {
             ...this.state.list.objA,
                  name: 'A1'
                }
            }
      })
//方法三  作用于对象中的深层级和第一层级
 let data = this.state.list;
      data.objA.name = 'A1';
      data.objD = 'D1';
      this.setState({
          list: data
      })
```

4.为什么需要使用.bind绑定this

传递一个函数名给一个变量，之后通过函数名()的方式进行调用，在方法内部如果使用this则this的指向会丢失

```js
const test = {    
    name:'jack',    
    getJack:function(){        
    console.log(this.name)    
	} 
} 
//const func = test.getJack()  //this指向test
const func = test.getJack;  //  this指向window this失去指向
func();

我们没有直接调用对象的方法，而是将方法声明给一个中间变量，之后利用中间变量()调用方法，此时this则失去指向，输出undefined
```

**在react中 onClick即是中间变量 所以this指向就会丢失**



### 事件处理



\1. 通过onXxx属性指定事件处理函数(注意大小写)

​    \1) React使用的是自定义(合成)事件, 而不是使用的原生DOM事件（为了更好的兼容）

​    \2) React中的事件是通过事件委托方式处理的(委托给组件最外层的元素) （为了高效）

\2. 通过event.target得到发生事件的DOM元素对象（不要过度使用ref）



什么是非受控组件/受控组件？

现有现取是非受控组件 (用的时候获取值)/           受控组件（随时可取的值需要使用（this.state&&onChange））

# 高级指引

## 无状态组件

https://juejin.cn/post/6844903493816303624

```javascript
// 有状态组件
import React, { Component, PropTypes } from 'react';

export default class CusImg extends Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div className={this.props.style}>
        <img src={this.props.imgurl}/>
        <text className={this.props.textStyle}>{this.props.text}</text>
    </div>);
  }
}

CusImg.propTypes = {
};

// 转为无状态组件
const CusImg = (props)=>(
  <div className={props.style}>
    <img src={props.imgurl}/>
    <text className={props.textStyle}>{props.text}</text>
</div>
);

module.exports = CusImg
```



## React组件之间如何通信

https://github.com/febobo/web-interview/issues/189

### 兄弟组件传递信息

父组件作为中间层实现数据的互通

```react
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {count: 0}
  }
  setCount = () => {
    this.setState({count: this.state.count + 1})
  }
  render() {
    return (
      <div>
        <SiblingA
          count={this.state.count}
        />
        <SiblingB
          onClick={this.setCount}
        />
      </div>
    );
  }
}
```

### 父组件向后代组件传递

父组件向后代组件传递数据是一件最普通的事情，就像全局数据一样

使用`context`提供了组件之间通讯的一种方式，可以共享数据，其他数据都能读取对应的数据

通过使用`React.createContext`创建一个`context`

```
 const PriceContext = React.createContext('price')
```

`context`创建成功后，其下存在`Provider`组件用于创建数据源，`Consumer`组件用于接收数据，使用实例如下：

`Provider`组件通过`value`属性用于给后代组件传递数据：

```
<PriceContext.Provider value={100}>
传递的子组件
<MyClass></MyClass>
</PriceContext.Provider>
```

如果想要获取`Provider`传递的数据，可以通过`Consumer`组件或者或者使用`contextType`属性接收，对应分别如下：

```
class MyClass extends React.Component {
  static contextType = PriceContext;
  render() {
    let price = this.context;
    /* 基于这个值进行渲染工作 */
  }
}
```

`Consumer`组件：

```
<PriceContext.Consumer>
    { /*这里是一个函数*/ }
    {
        price => <div>price：{price}</div>
    }
</PriceContext.Consumer>
```

完整版

```
// context.js
import React from 'react'
const { Consumer, Provider } = React.createContext(null) //创建 context 并暴露Consumer和Provide
export { Consumer, Provider }

// 父组件
import React from 'react'
import Son from './son'
import { Provider } from './context'
class Father extends React.Component {
  constructor(props) {
    super(props)
  }
  state = {
    info: 'info from father',
  }
  render() {
    return (
      <Provider value={this.state.info}>
        <div>
          <p>{this.state.info}</p>
          <Son />
        </div>
      </Provider>
    )
  }
}
export default Father

// 子组件
import React from 'react'
import GrandSon from './grandson'
import { Consumer } from './context'
class Son extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <Consumer>
        {(info) => (
          // 通过Consumer直接获取父组件的值

          <div>
            <p>父组件的值:{info}</p>
            <GrandSon />
          </div>

​        )}
​      </Consumer>
​    )
  }
}
export default Son

// 孙子组件
import React from 'react'
import { Consumer } from './context'
class GrandSon extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <Consumer>
        {(info) => (
          // 通过 Consumer 中可以直接获取组父组件的值

          <div>
            <p>组父组件的值:{info}</p>
          </div>

​        )}
​      </Consumer>
​    )
  }
}
export default GrandSon


注意使用多个Context，则需要使每一个consumer组件的context成为一个单独的节点

const Context1 = React.createContext(null) //创建
const Context2 = React.createContext(null)
//provider
	<Context1.Provider value={this.state.info}>
		<Context2.Provider value = {this.state.theme}>
		<Son/>
		<Context2.Provider>
	<Context1.Provider>



//consumer
<Context1.Consumer>
{(info:string)=>{
	<Context2.Consumer>
	{(theme:number)=>{
		<p>{info}<p>
		<P>{theme}</p>
	}}
	<Context2.Consumer>
}}

</Context1.Consumer>


很多优秀的 React 组件的核心功能都通过 Context 来实现的，比如 react-redux 和 react-router 等，所以掌握 Context 是必须的。
```

OnRef



### 非关系组件传递

如果组件之间关系类型比较复杂的情况，建议将数据进行一个全局资源管理，从而实现通信，例如`redux`。关于`redux`的使用后续再详细介绍

**总结**

由于`React`是单向数据流，主要思想是子组件不会改变接收的数据，只会监听数据的变化，当数据发生变化时它们会使用接收到的新值，而不是去修改已有的值

因此，可以看到通信过程中，数据的存储位置都是存放在上级位置中

https://github.com/febobo/web-interview/issues/189

## 高阶函数

1.若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数。

 2.若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。 //可以使代码更简便

**事件回调不能加小括号** 加上小括号则变成立即执行

```  
this.saveFormData('username')  高阶函数 返回的依然是一个函数  这个函数是真正的onChang的回调
onChange={this.saveFormData('username')} 这里调用的是返回值 需要 return (event)=>{值}

```

**onchange接受的是个函数才能够继续回调event**

onChange={event => this.saveFormData('username',event) }

需要写高阶函数进行回调才可以

高阶函数： Promise setTimeout

### 函数的柯里化

函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。 （就是闭包写法）

数组的 reduce（(item,ss),0）

```
function add(a){
	return (b)=>{
		return (c)=>{
			return a+b+c
		}
	}
}
const result = add(1)(2)(3)
```



## 高阶组件

https://vue3js.cn/interview/React/High%20order%20components.html#%E4%BA%8C%E3%80%81%E5%A6%82%E4%BD%95%E7%BC%96%E5%86%99   查看

高阶组件（HOC）是 React 中用于**复用组件逻辑的一种高级技巧**。HOC 自身不是 React API 的一部分，它是一种基于 React 的组合特性而形成的设计模式。

一个函数内部返回一个新的函数，内部采用闭包的写法

具体而言，**高阶组件是参数为组件，返回值为新组件的函数**

需要满足以下**条件**之一

- 接受一个或多个函数作为输入
- 输出一个函数

使用约定：

- props 保持一致

- 你不能在函数式（无状态）组件上使用 ref 属性，因为它没有实例

- 不要以任何方式改变原始组件 WrappedComponent

- 透传不相关 props 属性给被包裹的组件 WrappedComponent

- 不要再 render() 方法中使用高阶组件

- 使用 compose 组合高阶组件

- 包装显示名字以便于调试

  获取存储的data并渲染

```react
import React, { Component } from 'react'

function  withPersistentData (wrappedComponent){
    return class extends Component{
        componentDidMounet(){
            let data = localStorage.getItem('data')
            this.setState({data})
        }
        render(){
            return <WrappedCompontent data={this.state.data} {this.props}></WrappedCompontent>
        }
    }
    
}

class MyComponent2 extends Component{
    render(){
        return <div>{this.props.data}</div>
    }
}
const MyComponentWithPersistentData = withPersistentData(MyComponent2)
//调用 MyComponentWithPersistentData 就可以了
```



## refs使用

```
// 不能用了过时了 this.refs被删除
consturctor(props){
	this.myRef  =  react.createRef()//创建
}

componentDidMount(){
	this.refs.myRef.focus() // 获取焦点
}

render (){

	return (
		<input refs='myRef'/>
	)
}
//官网版本
consturctor(props){
	this.myRef = React.createRef()
}
componentDidMount(){
	this.myRef.current.focus() //通过current执行
}
render (){
	return(
		<input ref = {this.myRef}/>
	) 
}

ref属性用于原生HTML元素上，如果ref设置的组件为一个类组件的时候，ref对象接收到的是组件的挂载实例
在函数组件中可以使用useRef
注意的是，不能在函数组件上使用ref属性，因为他们并没有实例
主要用于：
对Dom元素的焦点控制、内容选择、控制
对Dom元素的内容设置及媒体播放
对Dom元素的操作和对组件实例的操作
```

https://github.com/febobo/web-interview/issues/189

## react生命周期

卸载组件

```
ReactDom.unmountComponentAtNode(document.getElementById('test'))//卸载  
```



### 新的生命周期

![image-20211126081130712](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211126081130712.png)

挂载阶段

1.constructor()   构造函数

2.static getDerivedStateFromProps() 通过props派生state

static getDerivedStateFromProps() 

1. 静态方法  不能给实例用 （不能使用.调用）

2. 返回状态对象/null（返回的状态就无法改变了）

3. 能收到props return props（直接改变state,状态都听props）  **state值取决于props**

   

4.  ```js
      //使用方法
    static getDerivedStateFromProps(nextProps, prevState) {
        const {type} = nextProps;
        // 当传入的type发生变化的时候，更新state
        if (type !== prevState.type) {
            return {
                type,
            };
        }
        // 否则，对于state不进行任何操作
        return null;
    }
    ```

3.render 提交

4.componentDidMount() 挂载结束

如果想使用componentWillMount (不需要使用) 

UNSAFE_componentWillMount

UNSAFE_componentWillReceiveProps 

副作用是 调用api去更新状态  

更新阶段

1.static getDerivedStateFromProps(nextProps, prevState) 通过props派生state   直接通过props修改 State

2.shouldComponentUpdate() 组件更新（return false就停止了）

这个方法用来判断是否需要调用 render 方法重新描绘 

dom。因为 dom 的描绘非常消耗性能，如果我们能在 shouldComponentUpdate 

方法中能够写出更优化的 dom diff 算法（判断这个是否必要更新），可以极大的提高性能。

作用:（进行性能优化）检查props和state中所有字段，以此来决定组件是否需要更新

3.render 挂载

4.getSnapshotBeforeUpdate()  更新前 获取Snapshot(获取更新前的数据 return出来 传给componentDidUpdate)    更新之前把数据保留下来传给**componentDidUpdate()**

5.componentDidUpdate(preprops，preState,SnapshotValue)更新结束



componentDidUpdate()使用方法

可以通过参数显示之前的props、state、snapshot

同时可以使用this获取当前的props 和 state

这个函数经常会被用来触发副作用，例如说当状态从未登录改为登录时，就可以在 componentDidUpdate 中去调用其他的 API：如获取用户信息、获取登陆用户才能够访问的信息

```
class Input extends Component {
  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log('prevProps', prevProps, 'curr props', this.props);
    console.log('prevState', prevState, 'curr state', this.state);
  }
}
```



当props或者state修改完 触发componentDidUpdate 注意判断否则会产生无限更新

卸载阶段

componentWillUnmount()

错误处理

当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：

1. static getDerivedStateFromError()
2. componentDidCatch()

### 旧的生命周期

![image-20211126081115251](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211126081115251.png)

挂载

1.constructor()

2.componentWillMount

3.render

4.componentDidMount

更新时

1.componentWillReceiveProps  <=父组件

2.shouldComponentUpdate  setState() 控制组件阀门

3.componentWillUpdate  this.forceUpdate()(与setState一样的方法) // 强制更新 不更setState时

4.render

5.componentDidUpdate

卸载时

componentWillUnmount







react-next项目搭建

全局注册npm install -g create-next-app

npm install -g npx

```
1.npx create-next-app blog
```

 创建next.js react框架

2.`yarn`命令来安装`@zeit/next-css`包

```
yarn add @zeit/next-css
```

新建一个`next.config.js`文件。这个就是`Next.js`的总配置文件。写入下面的代码:

```js
const withCss = require('@zeit/next-css')

if(typeof require !== 'undefined'){
    require.extensions['.css']=file=>{}
}

module.exports = withCss({})
```

3.接下来按需加载antd Design

## react-router 

```
// 安装
npm install --save react-router-dom
```





BOM中的history（hashhistory(类似锚点跳转)  bowerhistory）

为什么路由跳转的不是xxx.html 因为history（历史记录）机制

history.push({

pathname:'xxx',

query:{},

state"{},

search:""

})

react-router其实就是一个组件

Switch 当匹配到第一个组件的时候 后面的 组件就不应该继续匹配了

NavLink 存在一个 activeClassName 高亮属性 点击触发

### 动态传值

1.设置路由

```js
<Route path="/list/:id" component={List} />
```

2.传参

```js
 <li><Link to="/list/123">列表</Link> </li>
```

3.接受参数

```js
componentDidMount(){
        console.log(this.props.match)
    }
```

4.打印对象

- patch:自己定义的路由规则，可以清楚的看到是可以产地id参数的。
- url: 真实的访问路径，这上面可以清楚的看到传递过来的参数是什么。
- params：传递过来的参数，`key`和`value`值。

### 路由跳转会发生样式丢失

1.将引入css路径修改为绝对路径（把'./'修改为'/'）

2.修改为%PUBLIC_URL%/

3.改为HashRouter（#/认为前端资源 不看后面的东西，所以就不会带入的请求）

路由的模糊匹配与严格匹配



```js
//模糊匹配  默认模糊匹配
<MyNavLink to='/context/a' title='about' >About</MyNavLink>


<Route  path="/context" component={setting}/>
//严格匹配    
<Route exact path="/context" component={setting}/>
```

向路由传递params参数需要声明接接收  通过props.match.p

```js
//接受
 <Route path="/context/about/:id" component={about}/>
```



## React hooks

  [a,usea]  =useState() 定义变量 方法

usea(a+1) 异步操作

如果想查看的话

useEffect(()=>{

console.log(a)

})

### useEffect

`useEffect` 就是一个 Effect Hook，给函数组件增加了操作副作用(**数据获取、订阅或者手动修改过 DOM**称为**副作用**)的能力。

它跟 class 组件中的 `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 具有相同的用途，只不过被合并成了一个 API。

useEffect 代替常用的生命周期函数  `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount`

useEffect(()=>{

xxx //用来设置操作

return

```js
()=>{
            console.log('老弟，你走了!Index页面') //用来取消操作
        }
```

},[str])第二参数是限制  如果str修改才触发事件（相当于componentDidUpdate）

*大多数情况下，effect 不需要同步地执行。在个别情况下（例如测量布局），有单独的 [`useLayoutEffect`](https://zh-hans.reactjs.org/docs/hooks-reference.html#uselayouteffect) Hook 供你使用，其 API 与 `useEffect` 相同。*









### useContext 

const CountContext = React.creatContext(theme.light)

```js
需要其包裹<CountContext.Provider value={theme.light}>
    <Tool>    
    </CountContext.Provider>
```

Tool需要创建 useContext然后调用

```
const use  = useContext(CountContext)

return use
```

### 额外Hook





useRef 直接获取dom元素和保存变量 与ref this.ref类似

useCallBack缓存方法

自定义hooks函数获取窗口大小 编写就完了

#### useRef

useRef 与  React.createrefs()类似

```
//使用方法

const inputEl = useRef(null)
//打印ref
console(inputEL)
inputEl.current.value = 'helo Ref' 设置input的值
   const [text, setText] = useState('jspang')
    const textRef = useRef()
  useEffect(()=>{
 		 // 使用useEffect函数实现每次状态变化都进行变量修改，并打印
        textRef.current = text;
        console.log('textRef.current:', textRef.current)
    })
<input ref={inputEl} type='text'/>
<div ref></div>
<input value={text} onChange={(e)=>{setText(e.target.value)}} />
```



#### useReducer  （Reducer）

与useState最大区别

```
const [color, dispatch] = useReducer(reducer,'blue')
```

useReducer  一般有两个参数   第二个参数是默认值

`reducer`其实就是一个函数，这个函数接收两个参数，一个是状态，一个用来控制业务逻辑的判断参数。

```js
//Reducer基本语法
const [count,dispatch] =useReducer((state,action)=>{
    switch(action.type) {
        case 'add':
            return state + 1;
        case 'sub':
            return state - 1;
        default: 
            return state;
    }
},0)
```

使用useReducer useContext代替redux

```react
// 使用Context 实现了redux状态共享 添加Reducer 
function ShowArea() {
  const {color} = useContext(ColorContext)
  return (<div style={{ color: color }}>字体颜色为blue</div>)

}
//引入useContext
function Buttons() {
    const {dispatch} = useContext(ColorContext)
  return (
    <div>
          // 通过dispatch修改状态
      <button onClick={()=>{dispatch({{type:UPDATE_COLOR,color:"red"}})}>红色</button>
      <button onClick={()=>{dispatch({{type:UPDATE_COLOR,color:"yellow"}})}>黄色</button>
    </div>
  )
}


function Example() {
  return (
    <div>
      <Color>
        <ShowArea />
        <Buttons />
      </Color>
    </div>
  )
}
//Reducer 函数  在color函数中有了  处理业务逻辑和共享状态 就和redux一样了
const ColorContext  = React.createContext({})//使用Context实现状态共享
const UPDATE_COLOR = "UPDATE_COLOR"  //action.type类型
const reducer = (state,action)=>{
    switch(action.type){
        case UPDATE_COLOR:
            return action.color
        default:
            return state
    }
}

const Color =(props)=>{ 
	const [color,dispatch] = useReducer(reducer,'blue')
  <ColorContext.Provider value={{ color,dispatch}}>
    {props.children}
  </ColorContext.Provider>
}




```

#### useMemo缓存变量 useCallback缓存函数

**useMemo 优化ReactHooks程序性能，可以减少不必要的渲染类似（pureComponent，sholudComponentUpdate）**

useMemo有什么用  函数式组件失去了shouldComponentUpdate(更新之前)也类似computed把变量缓存起来

**每一次修改state都会调用所有的逻辑**，带来巨大性能问题（使用**useMemo，useCallBac**k解决）

![1639733222(1)](.\1639733222(1).png)

```react
//使用方法
function ChildComponent({name,children}){
    function changeXiaohong(name){
        console.log('她来了，她来了。小红向我们走来了')
    }

    const actionXiaohong = useMemo(()=>changeXiaohong(name),[name])  //第二个参数是依赖项  只有依赖项发生变化才会重新渲染
    // 根据依赖项name来判断是否调用changeXiaohong方法
    //如果没有提供依赖项数组，useMemo 在每次渲染时都会计算新的值。
    return (
        <>
            <div>{actionXiaohong}</div>
            <div>{children}</div>
        </>
    )
}
```

```
官方文档 useCallback(fn, deps)` 相当于 `useMemo(() => fn, deps)
```

```js

const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

useCallback必须配合 react.memo pureComponent，否则不但不会提升性能，还有可能降低性能。

把**内联回调函数**及**依赖项数组**作为参数传入 useCallback，它将返回**该回调函数**的 **memoized 版本**，该回调函数仅在**某个依赖项改变**时才会更新。当你把回调函数传递给经过优化的并使用引用相等性去避免非必要渲染（例如 shouldComponentUpdate）的子组件时，它将非常有用。

#### useLayoutEffect 

空数组作为第二个参数  仅在安装组件时执行一次提供的回调

其函数签名与 useEffect 相同，但它会在所有的 DOM 变更之后同步调用 effect。可以使用它来读取 DOM 布局并同步触发重渲染。在浏览器执行绘制之前，useLayoutEffect 内部的更新计划将被同步刷新





### Hook使用规则

优势: 代码简洁、组件简单

Hook 就是 JavaScript 函数，但是使用它们会有两个额外的规则：

- 只能在**函数最外层**调用 Hook。不要在循环、条件判断或者子函数中调用。

  （这让 React 能够在多次的 `useState` 和 `useEffect` 调用之间保持 hook 状态的正确）

  **Hook 的调用顺序在每次渲染中都是相同的，所以它能够正常工作**

  ```react
  // ------------
  // 首次渲染
  // ------------
  useState('Mary')           // 1. 使用 'Mary' 初始化变量名为 name 的 state
  useEffect(persistForm)     // 2. 添加 effect 以保存 form 操作
  useState('Poppins')        // 3. 使用 'Poppins' 初始化变量名为 surname 的 state
  useEffect(updateTitle)     // 4. 添加 effect 以更新标题
  //详情查看 https://zh-hans.reactjs.org/docs/hooks-rules.html
  ```

- 只能在 **React 的函数组件**中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中，我们稍后会学习到。）

### 自定义hook(解决class组件复用状态逻辑问题)

主要使用情景  想在两个函数之间**共享逻辑**，可以将代码提取至第三函数。

**自定义 Hook 是一个函数，其名称以 “`use`” 开头，函数内部可以调用其他的 Hook。** 例如，下面的 `useFriendStatus` 是我们第一个自定义的 Hook:

```react
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}

//使用自定义hooks
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}

自定义useHook规范
1.自定义hook必须以“use”开头
2.两个组件中使用相同hook 不会共享state?（想要共享可以使用useReducer，redux）

```



## React解决跨域

配置代理

第一种方法 在package.json文件中 

```
"proxy":"http://localhost:5000" 把端口转发给xx
```

有个bug 请求3000端口没有的URl才访问5000

第二种方法

1. 第一步：创建代理配置文件

   ```
   在src下创建配置文件：src/setupProxy.js
   ```

2. 编写setupProxy.js配置具体代理规则：

   ```js
   const proxy = require('http-proxy-middleware')
   //内置插件
   module.exports = function(app) {
     app.use(
       proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值（服务器是否能字段host）
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
   ```

说明：

1. 优点：可以配置多个代理，可以灵活的控制请求是否走代理。
2. 缺点：配置繁琐，前端请求资源时必须加前缀。

## React - redux 使用

简化react与redux流程（映射）

1.方便react 与redux的沟通不需要再使用   getState()以及dispatch

2.

```react 
//react-redux提供了两个方法
//App.tsx 包裹 TodoList
import  TodoList from './TodoList'
//提供器  只要是被包裹的组件都可以获得store中的state
import { Provider } from 'react-redux'

export default class Ceshi extends Component {
    render() {
        return (
            <Provider store={store}>
            <TodoList/>
        </Provider>
        )
    }
}
//TodoList.tsx
//connect 连接器 （其实它就是一个方法），有了这个连接器就可以很容易的获得数据了。
import { connect } from 'react-redux'

class TodoList extends React.Component<TodoListProps, TodoListState> {
    constructor(props: TodoListProps) {
        super(props);
        this.state = store.getState();
        console.log(this.props)
    }
    render() { 
        return (<div>dwxPang

            <p>{this.props.inputValue}</p>
            <input value={this.props.inputValue} onChange={this.props.changeState}></input>       
        </div>  );
    }
}
 
const stateToProps = (state)=>{
    return {
        inputValue: state.inputValue
        state
    }
}
//使用content 将dispatch通过porps传递给参数 代码清晰
const dispatchToProps = (dispatch)=>{
    return {
        let changeState = (e)=>{
            let action = {
                type:'change_input',
                value:e.target.value
            }
            dispatch(changeState)
        }
    }
}
export default connect(stateToProps,dispatchToProps)(TodoList)
//connect 有两个参数第一个参数是获取state，第二个是(dispatch修改store)
```

状态管理工具 redux mobx
