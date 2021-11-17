React 17 学习



**注意：** 组件名称必须以大写字母开头。

React 会将以小写字母开头的组件视为原生 DOM 标签。例如，`<div />` 代表 HTML 的 div 标签，而 `<Welcome />` 则代表一个组件，并且需在作用域内使用 `Welcome`。

setState修改对象状态

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

//3.包含关系（v-slot）

```js
//v-slot 使用方法 https://cn.vuejs.org/v2/guide/components-slots.html#%E5%8A%A8%E6%80%81%E6%8F%92%E6%A7%BD%E5%90%8D
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
// 包含关系（props.children）
https://react.docschina.org/docs/composition-vs-inheritance.html
//也可以不使用props.children 可以自行约定：所需内容传入props使用相应prop
<div className="SplitPane-left">
        {props.left}
 </div>

 <SplitPane
      left={
        <Contacts />
      } />
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

## 高阶函数

1.若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数。

 2.若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。

**事件回调不能加小括号** 加上小括号则变成立即执行

```  
this.saveFormData('username')  高阶函数 返回的依然是一个函数  这个函数是真正的onChang的回调
onChange={this.saveFormData('username')} 这里调用的是返回值 需要 return (event)=>{值}

```

**onchange接受的是个函数才能够继续回调event**

onChange={event => this.saveFormData('username',event) }

需要写高阶函数进行回调才可以

高阶函数： Promise setTimeout

函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。 

todolist案例学习

1.拆分组件  实现静态组件

2.动态初始化列表，如何确定将数据放在哪个组件的State？

某个组件使用：放在其自身的state中

某些组件的使用：放在他们共同的父组件state中 （官方称作状态提示）

3.父子通信

父子 通过props传递

子父 通过props传递 要求父提前给子传递一个函数

状态在哪 操作状态的方法就在哪

## react生命周期

挂载阶段

1.constructor()   构造函数

2.static getDerivedStateFromProps() 通过props派生state

3.render 提交

4.componentDidMount() 挂载结束

副作用是 调用api去更新状态  

更新阶段

1.static getDerivedStateFromProps(nextProps, prevState) 通过props派生state   直接通过props修改 State

2.shouldComponentUpdate() 组件更新

3.render 挂载

4.getSnapshotBeforeUpdate()  更新前

5.componentDidUpdate()更新结束



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

其实就是一个组件

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

动态传值2

## React hooks

useState 定义变量 方法

useEffect 代替常用的生命周期函数

useEffect(()=>{

xxx

return

```js
()=>{
            console.log('老弟，你走了!Index页面')
        }
```

},[str])第二参数是限制  如果str修改才触发事件

useContext 需要创建 useContex t然后调用

const use  = useContext

```js
需要其包裹<CountContext.Provider value={count}>
            </CountContext.Provider>
```

useReduce

useMemo缓存变量

useRef 直接获取dom元素和保存变量 与ref this.ref类似

useCallBack缓存方法

自定义hooks函数获取窗口大小 编写就完了

useReducer  一般有两个参数   第二个参数是默认值

`reducer`其实就是一个函数，这个函数接收两个参数，一个是状态，一个用来控制业务逻辑的判断参数。

```js
function countReducer(state, action) {
    switch(action.type) {
        case 'add':
            return state + 1;
        case 'sub':
            return state - 1;
        default: 
            return state;
    }
}
```

使用useReducer useContext代替redux

