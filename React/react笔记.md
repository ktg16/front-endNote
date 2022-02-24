
# [***React框架***](https://react.docschina.org/)

## React的起源和发展 

    起初facebook在建设instagram（图片分享）的时候，因为牵扯到一个东西叫数据流，那为了处理数据流并且还要考虑好性能方面的问题，Facebook开始对市场上的各种前端MVC框架去进行一个研究，然而并没有看上眼的，于是Facebook觉得，还是自己开发一个才是最棒的，那么他们决定抛开很多所谓的“最佳实践”，重新思考前端界面的构建方式，他们就自己开发了一套，果然大牛创造力还是很强大的。

React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。



## React的出发点

    基于HTML的前端界面开发正变得越来越复杂，其本质问题基本都可以归结于如何将来自于服务器端或者用户输入的动态数据高效的反映到复杂的用户界面上。而来自Facebook的React框架正是完全面向此问题的一个解决方案，按官网描述，其出发点为：用于开发数据不断变化的大型应用程序（Building large applications with data that changes over time）。相比传统型的前端开发，React开辟了一个相当另类的途径，实现了前端界面的高性能高效率开发。



## React与传统MVC的关系

轻量级的视图层库！A JavaScript library for building user interfaces

    React不是一个完整的MVC框架，最多可以认为是MVC中的V（View），甚至React并不非常认可MVC开发模式；React 构建页面 UI 的库。可以简单地理解为，React 将将界面分成了各个独立的小块，每一个块就是组件，这些组件之间可以组合、嵌套，就成了我们的页面。



react是mvc里面的view层 （轻量级的视图层框架）

vue是完整的mvvm的框架 （双向数据绑定原理：Object.defineProperty  get与set  watcher --> 虚拟dom对比 --> 渲染真实dom节点）



## React高性能的体现：虚拟DOM

### React高性能的原理：

在Web开发中我们总需要将变化的数据实时反应到UI上，这时就需要对DOM进行操作。而复杂或频繁的DOM操作通常是性能瓶颈产生的原因（如何进行高性能的复杂DOM操作通常是衡量一个前端开发人员技能的重要指标）。

React为此引入了虚拟DOM（Virtual DOM）的机制：在浏览器端用Javascript实现了一套DOM API。基于React进行开发时所有的DOM构造都是**通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新**。而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，例如你连续的先将节点内容从A-B,B-A，React会认为A变成B，然后又从B变成A  UI不发生任何变化，而如果通过手动控制，这种逻辑通常是极其复杂的。

尽管每一次都需要构造完整的虚拟DOM树，但是因为虚拟DOM是内存数据，性能是极高的，部而对实际DOM进行操作的仅仅是Diff分，因而能达到提高性能的目的。这样，在保证性能的同时，开发者将不再需要关注某个数据的变化如何更新到一个或多个具体的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的。

#### React Fiber:

在react 16之后发布的一种react 核心算法，**React Fiber是对核心算法的一次重新实现**(官网说法)。之前用的是diff算法。

**在之前React中，更新过程是同步的，这可能会导致性能问题。**

当React决定要加载或者更新组件树时，会做很多事，比如调用各个组件的生命周期函数，计算和比对Virtual DOM，最后更新DOM树，这整个过程是同步进行的，也就是说只要一个加载或者更新过程开始，中途不会中断。因为JavaScript单线程的特点，如果组件树很大的时候，每个同步任务耗时太长，就会出现卡顿。

React Fiber的方法其实很简单——分片。把一个耗时长的任务分成很多小片，每一个小片的运行时间很短，虽然总时间依然很长，但是在每个小片执行完之后，都给其他任务一个执行的机会，这样唯一的线程就不会被独占，其他任务依然有运行的机会。






## React的特点和优势

   **1.虚拟DOM  ==> 高性能**

我们以前操作dom的方式是通过document.getElementById()的方式，这样的过程实际上是先去读取html的dom结构，将结构转换成变量，再进行操作

而reactjs定义了一套变量形式的dom模型，一切操作和换算直接在变量中，这样减少了操作真实dom，性能真实相当的高，和主流MVC框架有本质的区别，并不和dom打交道

   **2.组件化  ===> 高效率**

*react最核心的思想是将页面中任何一个区域或者元素都可以看做一个组件 component*

创建拥有各自状态的组件，再由这些组件构成更加复杂的 UI。 

   **3.声明式**  

React 使创建交互式 UI 变得轻而易举。为你应用的每一个状态设计简洁的视图，当数据改变时 React 能有效地更新并正确地渲染组件。 

​    **4.JSX  语法**  

在vue中，我们使用render函数来构建组件的dom结构性能较高，因为省去了查找和编译模板的过程，但是在render中利用createElement创建结构的时候代码可读性较低，较为复杂，此时可以利用jsx语法来在render中创建dom，解决这个问题，但是前提是需要使用工具来编译jsx





## 构建React简易环境

react开发需要引入多个依赖文件：react.js、react-dom.js，分别又有开发版本和生产版本

react.js中有React对象，帮助我们创建组件等功能

react-dom.js中有ReactDOM对象，渲染组件的虚拟dom为真实dom的爆发功能

在编写react代码的时候会大量的使用到jsx代码，但是需要编译：

1. 浏览器端编译，通过引入browser、babel等对引入的script内的代码做编译 -- 浏览器  安装 babel-standalone
2. 利用webpack等开发环境进行编译，将编译好的文件引入到应用中

```
    <!--引入react的核心包-->
    <script src="./js/react.development.js"></script>
    <!--引入开发web的包-->
    <script src="./js/react-dom.development.js"></script>
    <!--引入解析jsx的包-->
    <script src="./js/babel.js"></script>
    
    <script type="text/babel">
    	ReactDOM.render(<h2>hello world</h2>,
           document.getElementById("box"))
    </script>
```

在react中创建组件的形式有三种

- 纯函数式定义的无状态组件
- React.createClass 定义的组件
- Extends React.Component 定义的组件





- react中有三种创建组件的形式
- **纯函数不会被实例化，不能访问this，没有生命周期**
- 尽可能的使用纯函数拆分复杂型组件

## 元素与组件

如果代码多了之后，不可能一直在render方法里写，所以就需要把里面的代码提出来，定义一个变量，像这样：

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
// 这里感觉又不习惯了？这是在用JSX定义一下react元素
const app = <h1>欢迎进入React的世界</h1>
ReactDOM.render(
  <div>
    { app }
  </div>
  document.getElementById('root')
)
```





## 函数式组件

这里我们定义的方法实际上也是react定义组件的第一种方式-定义函数式组件，这也是无状态组件。

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
/*
const 组件名(首字母大写)=（props）=>{
	return jsx表达式             
}
*/
const App = (props) => {
    return (
    	<h1>欢迎进入{props.name}的世界</h1>
    )
}

ReactDOM.render(
  // React组件的调用方式
  <App name={"react"} />,
  document.getElementById('root')
)
```

这样一个完整的函数式组件就定义好了。但要**注意！注意！注意！**组件名必须**大写**，否则报错。





## class组件

ES6的加入让JavaScript直接支持使用class来定义一个类，react的第二种创建组件的方式就是使用的类的继承`ES6 class`是目前官方推荐的使用方式，它使用了ES6标准语法来构建，看以下代码：

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

/*
class 组件名  extends  React.Component {
	render(){ //render是必不可少的生命周期钩子函数！
		return jsx表达式
	}
}
*/
//class组件一定要继承 React.Component
class App extends React.Component {
  render () {
    return (
      // 注意这里得用this.props.name, 必须用this.props
      <h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}
ReactDOM.render(
  <App name="react" />,
  document.getElementById('root')
)
```



> 更老的一种方法：

在15.x的版本只能这样创建组件, 但现在的项目基本上不用

```jsx
React.createClass({
  getInitialState(){ //定义组件初始化状态
      
  },
  getDefaultProps(){ //定义组件的默认属性
      
  },
  render () {
    return (
      <div>hello world</div>
  	)
  }
})
```





## 组件的组合、嵌套

将一个组件渲染到某一个节点里的时候，会将这个节点里原有内容覆盖

组件嵌套的方式就是将子组件写入到父组件的模板中去，且react没有Vue中的内容分发机制（slot），所以我们在一个组件的模板中只能看到父子关系

```jsx
// 从 react 的包当中引入了 React 和 React.js 的组件父类 Component
// 还引入了一个React.js里的一种特殊的组件 Fragment
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
      <h1>欢迎进入React的世界</h1>
  	)
  }
}
class Content extends Component {
  render () {
    return (
      <p>React.js是一个构建UI的库</p>
  	)
  }
}
/** 由于每个React组件只能有一个根节点，所以要渲染多个组件的时候，需要在最外层包一个容器，如果使用div, 会生成多余的一层dom
class App extends Component {
  render () {
    return (
    	<div>
    		<Title />
        	<Content />
      	</div>
  	)
  }
}
**/
// 如果不想生成多余的一层dom可以使用React提供的Fragment组件在最外层进行包裹
class App extends Component {
  render () {
    return (
      <Fragment>
      	<Title />
        <Content />
      </Fragment>
  	)
  }
}
ReactDOM.render(
  <App/>,
  document.getElementById('root')
)
```





## JSX语法糖

JSX是一种语法糖，全称：javascript xml

JSX语法不是必须使用的，但是因为使用了JSX语法之后会降低我们的开发难度，故而这样的语法又被成为语法糖。

看下面的DOM结构：

```html
<div class='app' id='appRoot'>
  <h1 class='title'>欢迎进入React的世界</h1>
  <p>
    React.js 是一个帮助你构建页面 UI 的库
  </p>
</div>
```

上面这个 HTML 所有的信息我们都可以用 JavaScript 对象来表示：

```js
{
  tag: 'div',
  attrs: { className: 'app', id: 'appRoot'},
  children: [
    {
      tag: 'h1',
      attrs: { className: 'title' },
      children: ['欢迎进入React的世界']
    },
    {
      tag: 'p',
      attrs: null,
      children: ['React.js 是一个构建页面 UI 的库']
    }
  ]
}
```

但是用 JavaScript 写起来太长了，结构看起来又不清晰，用 XML的方式写起来就方便很多了。

于是 React.js 就把 JavaScript 的语法扩展了一下，**让 JavaScript 语言能够支持这种直接在 JavaScript 代码里面编写类似 XML 标签结构的语法，这样写起来就方便很多了**。**编译的过程会把类似 XML 的 JSX 结构转换成 JavaScript 的对象结构**。

下面代码:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class App extends React.Component {
  render () {
    return (
      <div className='app' id='appRoot'>
        <h1 className='title'>欢迎进入React的世界</h1>
        <p>
          React.js 是一个构建页面 UI 的库
        </p>
      </div>
    )
  }
}

ReactDOM.render(
	<App />,
  document.getElementById('root')
)
```

编译之后将得到这样的代码:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class App extends React.Component {
  render () {
    return (
      React.createElement(
        "div",
        {
          className: 'app',
          id: 'appRoot'
        },
        React.createElement(
          "h1",
          { className: 'title' },
          "欢迎进入React的世界"
        ),
        React.createElement(
          "p",
          null,
          "React.js 是一个构建页面 UI 的库"
        )
      )
    )
  }
}

ReactDOM.render(
	React.createElement(App),
  document.getElementById('root')
)
```

**`React.createElement` 会构建一个 JavaScript 对象来描述你 XML 结构的信息，包括标签名、属性、还有子元素等, 语法为**

```jsx
React.createElement(
  type,
  [props],
  [...children]
)
```



在不使用JSX的时候，需要使用React.createElement来创建组件的dom结构，但是这样的写法虽然不需要编译，但是维护和开发的难度很高，且可读性很差



所谓的 JSX 其实就是 JavaScript 对象，所以使用 React 和 JSX 的时候一定要经过编译的过程:

> JSX代码 — > 使用react构造组件，bable进行编译（React.createElement方法）—> JavaScript对象（虚拟dom） — `ReactDOM.render()函数进行渲染`—>真实DOM元素 —>插入页面



另：

- JSX就是在js中使用的xml，但是，这里的xml不是真正的xml，只能借鉴了一些xml的语法，例如：


最外层必须有根节点、标签必须闭合

- jsx借鉴xml的语法而不是html的语法原因：xml要比html严谨，编译更方便
- react中jsx里的注释要写成{/*  */}的方式





## 组件dom添加样式

- 行内样式

想给虚拟dom添加行内样式，需要使用表达式传入样式对象的方式来实现：

```jsx
// 注意这里的两个括号，第一个表示我们在要JSX里插入JS了，第二个是对象的括号
 <p style={{color:'red', fontSize:'14px'}}>Hello world</p>

```

- 使用`class`

React推荐我们使用行内样式，因为React觉得每一个组件都是一个独立的整体

其实我们大多数情况下还是大量的在为元素添加类名，但是需要注意的是，**`class`需要写成`className`（因为毕竟是在写类js代码，会收到js规则的现在，而`class`是关键字）**

```jsx
<p className="hello" style = {this.style}>Hello world</p>
```





## React Event

在react中，我们想要给组件的dom添加事件的话，也是需要在行内添加的方式，事件名字需要写成小驼峰的方式，值利用表达式传入一个函数即可。（原生的事件全是小写`onclick`, React里的事件是驼峰`onClick`）

注意，在没有渲染的时候，页面中没有真实dom，所以是获取不到dom的

给虚拟dom结构中的节点添加样式。在行内添加,写成驼峰形式，值是一个函数名，需要用 { } 包裹

```
class App extends React.Component {
	handleClick(){
		alert(1)
	}
    render () {
        return (
                <div className='app' id='appRoot'>
                    <h1 className='title'>欢迎进入React的世界</h1>
                    <p onClick={this.handleClick}>
                    	React.js 是一个构建页面 UI 的库
                    </p>
                </div>
            )
        }
}
ReactDOM.render(<App/>,document.getElementById("box"))
```

## 阻止组件渲染

在极少数情况下，你可能希望能隐藏组件，即使它已经被其他组件渲染。若要完成此操作，你可以让 `render` 方法直接返回 `null`，而不进行任何渲染。

```
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}
```

## 列表&key

遍历列表 需要加上key

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>    {number}
  </li>
);

在类似TODOlist中 不建议使用index作为key 
```

## jsx中数组的遍历操作

```
//vue的模板中遍历数组 ==> <li v-for="item in arr">{{item}}</li>
//遍历数组  arr.map
//为什么加key?
//key 帮助 React 识别哪些元素改变了，比如被添加或删除。
//因此你应当给数组中的每一个元素赋予一个确定的标识。
var arr = ["aa","bb","cc"]
ReactDOM.render(
    <div>
        {
            arr.map((item,index)=>{
            	return <p key={index}>{item}</p>
            })
        }
	</div>,
document.querySelector("#box"))
```

一个好的经验法则是：在 `map()` 方法中的元素需要设置 key 属性。

```
如果被提取出来 应该这样定义key
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 正确！key 应该在数组的上下文中被指定    <ListItem key={number.toString()}       id={post.id} //组件需要key属性值时      value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

## 




## React中的数据承载-Props/State

任意的视图变化都应该由数据来控制

React也是基于数据驱动(声明式)的框架，组件中必然需要承载一些数据，在react中起到这个作用的是属性和状态（props & state）

1. 属性（props）  在组件外部传入，或者内部设置，组件内部通过this.props获得
2. 状态（state）   在组件内部设置或者更改，组件内部通过this.state获得

父子通信 父元素给子元素一个方法 子元素 this.props.xxx()调用传递给父亲

### 属性(props)

**属性一般是外部传入的，组件内部也可以通过一些方式来初始化的设置，属性不能被组件自己更改**

属性是描述性质、特点的，**组件自己不能随意更改**

使组件拥有属性的方式：

1. 在装载（mount）组件的时候给组件传入

传入数据的时候，除了字符串类型，其他的都应该包上表达式，但是为了规整，所有的数据传递，最好都包上{}

```
var Gouzi = React.createClass({
    render(){
        console.log(this)
        return (
            <div>
                <p>我的名字：{this.props.name}</p>
                <p>我的性别：{this.props.sex}</p>
                <p>我的年龄：{this.props.age}</p>  
                <p>我的父亲是：{this.props.father}</p>                                       
            </div>
        )
    }
})

let info = {
    sex:'male',
    father:'狗爸'
}

ReactDOM.render(<Gouzi {...info} name={"大狗子"} age={26}/>,app)

ReactDOM.render(<Gouzi info={info} name={"大狗子"} age={26}/>,app)
```

2. 父组件给子组件传入

父组件在嵌套子组件的时候为子组件传入，传入的方式和上面的方式一样

```
//父组件的render函数
render(){
    return (
        <div>
            <p>父组件：</p>
            <hr/>
            <Son name={'大狗子'}/>
            <Son name={'二狗子'}/>
        </div>
    )
}
```
3. 根据属性或状态，我们可以在render中的表达式里做一些逻辑判断，可以使用||、三元表达式、子执行函数等等

```
getName(){
    return this.props.name || '野狗子'
},
render:function () {
    let {name} = this.props
    return (
    <div>
        <p>我是子组件-{this.props.name || '野狗子'}</p>
        <p>我是子组件-{this.props.name?this.props.name:'野狗子'}</p>
        <p>我是子组件-{this.getName()}</p>
    </div>
    )
}
```



### 状态(state)

状态就是组件描述某种显示情况的数据，由组件自己设置和更改，也就是说由组件自己维护，使用状态的目的就是为了在不同的状态下使组件的显示不同(自己管理)

在组件中可以通过constructor构造函数来给组件挂载初始状态,在组件内部通过this.state获取

**this.props和this.state是纯js对象,在vue中，$data属性是利用Object.defineProperty处理过的，更改$data的数据的时候会触发数据的getter和setter，但是react中没有做这样的处理，如果直接更改的话，react是无法得知的，所以，需要使用特殊的更改状态的方法：**

**setState(params)**

**在setState中传入一个对象，就会将组件的状态中键值对的部分更改，还可以传入一个函数，这个回调函数必须返回像上面方式一样的一个对象，函数可以接收prevState和props**

```
//1.
let doing = this.state.doing=='学习'?'玩游戏':'学习'
this.setState({doing})

//2.
this.setState((prevState,props)=>{
    return {
        doing:prevState.doing=='学习'?'玩游戏':'学习'
    }
})
```

#### `setState`有两个参数

第一个参数可以是对象，也可以是方法return一个对象，我们把这个参数叫做`updater`

- 参数是对象

  ```jsx
  let dos = this.state.doing==="学英语"?"玩游戏":"学英语";
  this.setState({
      doing:dos
  });
  ```

- 参数是方法  

  ```jsx
  this.setState((prevSate,props)=>{
      return {
          doing:prevSate.doing==="学英语"?"玩游戏":"学英语"
      }
  });
  ```

  注意的是这个方法接收两个参数，第一个是上一次的state, 第二个是props
  
  如果想对更新过的数据 再进行更新 使用下面方法

**`setState`是异步的，所以想要获取到最新的state，没有办法获取，就有了第二个参数，这是一个可选的回调函数**

```jsx
this.setState((prevSate,props)=>{
    return {
        doing:prevSate.doing==="学英语"?"玩游戏":"学英语"
    }
}, () => {
  console.log('回调里的',this.state.doing)  //获取更新后的值
})
console.log('setState外部的',this.state.doing) //还是之前没有更新的值
```





#### 两种setState的比较：

另外setState(stateChange[, callback])这种形式的更改状态，会将传入的对象浅层合并到新的 state 中，例如，调整购物车商品数：

```
this.setState({quantity: 2})
```

这种形式的 `setState()` 是异步的，并且在同一周期内会对多个 `setState` 进行批处理。例如，如果在同一周期内多次设置商品数量增加，则相当于：

```
Object.assign(
  previousState,
  {quantity: state.quantity + 1},
  {quantity: state.quantity + 1},
  ...
)
```

后调用的 `setState()` 将覆盖同一周期内先调用 `setState` 的值，因此商品数仅增加一次。如果后续状态取决于当前状态，我们建议使用 updater 函数的形式代替：

```
this.setState((prevState,props) => {
  return {quantity: prevState.quantity + 1}; //连续执行多次获放入队列中一次执行
}[, callback]);
```

//定义函数式组件（无状态组件）

​    //16.8推出了useState这个hooks，可以在函数式组件中定义状态了。

​    //const [状态,更改状态的方法] = React.useState(0)

​    function App(props){

​      // 声明一个新的叫做 “count” 的 状态

​      const [count, setCount] = React.useState(0);

​      const [title,setTitle] = React.useState("hello")

​      return (

                <div>

                    <p>count === {count} === {title}</p>

                    <p onClick={()=>{setCount(count+1)}}>更改count</p>

                    <p onClick={()=>{setTitle("你好")}}>更改title</p>

                    <p>这是App组件...</p>    

​        </div>

​      )

​    }



### 实现下拉菜单的方式

1. 通过数据来控制元素的行内样式中display的值，或者去控制类名

```
<ul style={{display:isMenuShow?'block':'none'}}><li>国内新闻</li></ul>
...
<ul className={isMenuShow?'show':'hide'}><li>国内新闻</li></ul>
```

2. 根据数据控制是否渲染改节点、组件
```
{
    isMenuShow?<ul><li>国内新闻</li></ul>:''
}
```
3. 通过ref对dom、组件进行标记，在组件内部通过this.refs获取到之后，进行操作
```
<ul ref='content'><li>国内新闻</li></ul>
...
this.refs.content.style.display = this.state.isMenuShow?'block':'none'
```



### 属性和状态的对比

相似点：都是纯js对象，都会触发render更新，都具有确定性（状态/属性相同，结果相同）

不同点： 

1. 属性能从父组件获取，状态不能
2. 属性可以由父组件修改，状态不能
3. 属性能在内部设置默认值，状态也可以
4. 属性不在组件内部修改，状态要改
5. 属性能设置子组件初始值，状态不可以
6. 属性可以修改子组件的值，状态不可以

`state` 的主要作用是用于组件保存、控制、修改自己的可变状态。**`state` 在组件内部初始化，可以被组件自身修改，而外部不能访问也不能修改**。你可以认为 `state` 是一个局部的、只能被组件自身控制的数据源。**`state` 中状态可以通过 `this.setState`方法进行更新，`setState` 会导致组件的重新渲染。**

`props` 的主要作用是让使用该组件的父组件可以传入参数来配置该组件。**它是外部传进来的配置参数，组件内部无法控制也无法修改**。除非外部组件主动传入新的 `props`，否则组件的 `props` 永远保持不变。



没有 `state` 的组件叫无状态组件（stateless component），设置了 state 的叫做有状态组件（stateful component）。因为状态会带来管理的复杂性，我们尽量多写无状态组件，尽量少写有状态的组件。这样会降低代码维护的难度，也会在一定程度上增强组件的可复用性。





## 表单

## [受控组件与非受控组件](https://react.docschina.org/docs/forms.html)

表单元素它的值来自于state 这个组件就是受控组件，否则就是非受控组件



> 受控组件：在HTML中，表单元素通常自己维护 state，并根据用户输入进行更新。而在 React 中，可变状态通常保存在组件的 state 属性中，并且只能通过使用 [`setState()`](https://react.docschina.org/docs/react-component.html#setstate)来更新。
>
> 我们可以把两者结合起来，使 React 的 state 成为“唯一数据源”。渲染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”。

```
class App extends React.Component{
    constructor(props){
        super(props);
        this.state={
        	n:1
        }
    }
    change=(e)=>{
        this.setState({
        	n: e.target.value
        })
    }
    handeleSubmuit(e){
    alert('提交的名字'+ this.state.value)
    event.preventDefault
    }
    render(){
        return (
        <form onSubmit={this.handleSubmit}>
            <div>
            	<input value={this.state.n} onChange={this.change} />									{this.state.n}
            	<input type="submit" value="提交" />
            </div>
            </form>
           )
     }
 }
 ReactDOM.render(<App />,document.getElementById("box"));
```





> 非受控组件：这时表单数据将交由 DOM 节点来处理。
>
> 要编写一个非受控组件，而不是为每个状态更新都编写数据处理函数，你可以 使用 ref 来从 DOM 节点中获取表单数据自己控制节点。

```
class App extends React.Component{
    constructor(props){
    	super(props);
    }
    handleSubmit = e=>{
    	e.preventDefault();
    }
    render(){
        return (
            <form onSubmit={this.handleSubmit}>
                <label>
                	<input type="text" ref={el=>this.input=el} />
                </label>
                <input type="submit" value="Submit" />
            </form>
         )
      }
 }
 ReactDOM.render(<App />,document.getElementById("box"));
```

### select 标签

由于 `selected` 属性的缘故，椰子选项默认被选中

**你可以将数组传递到 `value` 属性中，以支持在 `select` 标签中选择多个选项：**

```
<select   value={this.state.value} onChange={this.handleChange}> /同样使用 onChange
  <option value="grapefruit">葡萄柚</option>
  <option value="lime">酸橙</option>
  <option selected value="coconut">椰子</option>
  <option value="mango">芒果</option>
</select>
```

处理多个输入时  使用三目运算符进行运算

```
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.name === 'isGoing' ? target.checked : target.value;
    const name = target.name;
    this.setState({
      [name]: value    });// ES6 计算属性名称的语法更新给定输入名称对应的 state 值
  }

  render() {
    return (
      <form>
        <label>
          参与:
          <input
            name="isGoing"            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          来宾人数:
          <input
            name="numberOfGuests"            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

## 组合vs继承  无虚继承  组合可直接引入

```
 
相当于 vue中的slot
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
也可以使用children

```

## ref属性

React提供的这个`ref`属性，表示为对组件真正实例的引用，其实就是`ReactDOM.render()`返回的组件实例。`ref`可以挂载到组件上也可以是dom元素上。

- 挂到组件(`class`声明的组件)上的ref表示对组件实例的引用。
- **不能**在函数式组件上使用 ref 属性，因为它们没有实例：
- 挂载到dom元素上时表示具体的dom元素节点。

在React 最新的版本中，要使用`ref`, 需要使用`React.createRef`方法先生成一个`ref`。

```jsx
import React, { Component, createRef } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()  //必须要写！目的就是为了调用父类构造函数
    // 创建inputRef
    this.inputRef=createRef()
  }
  componentDidMount () {
    console.log(this.inputRef.current) // <input type="text">
  }
  render () {
    return (
  		<div>
        {/* 关联ref和dom */}
        <input type="text" ref={this.inputRef} />
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```





callback回调函数形式

```js
import React, { Component, createRef } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  componentDidMount () {
    console.log(this.input) // <input type="text">
  }
  render () {
    return (
  		<div>
        {/* 关联ref和dom */}
        <input type="text" ref={(el)=>{this.input=el}} />
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```



[函数式组件里面通过React 16.8推出的新特性 Hooks实现（useRef）](https://react.docschina.org/docs/hooks-reference.html)

函数式组件内部无this/无生命周期钩子函数

```js
function App(){
    const input = React.useRef()
    return (
        <div>
            <input type="text" ref={input}/>    
        	<button onClick={()=>{input.current.focus()}}>Focus</button>
        </div>
	)
}
ReactDOM.render(<App/>,document.getElementById("box"))
```









## React生命周期

<img src="https://s1.ax1x.com/2020/06/19/NuCy1f.png"  />

React中组件也有生命周期，也就是说也有很多钩子函数供我们使用, 组件的生命周期，我们会分为四个阶段，挂载、更新、卸载、错误处理

### 挂载阶段

当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：

1. constructor() 

2. static getDerivedStateFromProps()

3. render() 

4. componentDidMount()

   ```
   注意:
   下述生命周期方法即将过时，在新代码中应该避免使用它们：
   UNSAFE_componentWillMount()
   
   ```

   

### 更新阶段

当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下： 

1. static getDerivedStateFromProps()
2. shouldComponentUpdate() 
3. render() 
4. getSnapshotBeforeUpdate() 
5. componentDidUpdate()

```
注意:
下述方法即将过时，在新代码中应该避免使用它们：
UNSAFE_componentWillUpdate()
UNSAFE_componentWillReceiveProps()

```



### 卸载阶段

当组件从 DOM 中移除时会调用如下方法：

​	componentWillUnmount()



### 错误处理

当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：

1. static getDerivedStateFromError()
2. componentDidCatch()



### 各生命周期详解

#### 1.constructor(props)

**如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。**

在 React 组件挂载之前，会调用它的构造函数。在为 React.Component 子类实现构造函数时，应在其他语句之前前调用 `super(props)`。否则，`this.props` 在构造函数中可能会出现未定义的 bug。

通常，在 React 中，构造函数仅用于以下两种情况：

- 通过给 `this.state` 赋值对象来初始化[内部 state](https://react.docschina.org/docs/state-and-lifecycle.html)。
- 为[事件处理函数](https://react.docschina.org/docs/handling-events.html)绑定实例

在 `constructor()` 函数中**不要调用 `setState()` 方法**。如果你的组件需要使用内部 state，请直接在构造函数中为 **`this.state` 赋值初始 state**：

```
constructor(props) {
  super(props);
  // 不要在这里调用 this.setState()
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);绑定this
}

```

只能在构造函数中直接为 `this.state` 赋值。如需在其他方法中赋值，你应使用 `this.setState()` 替代。



#### 2.static getDerivedStateFromProps(nextProps, prevState)

`getDerivedStateFromProps` 会在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。它应返回一个对象来更新 state，如果返回 null 则不更新任何内容。

如果是由于父组件的`props`更改，所带来的重新渲染，也会触发此方法。

当状态发生变化的时候，this.setState()的时候，此钩子函数同样也会执行。

之前这里都是使用`constructor`+`componentWillRecieveProps`完成相同的功能的



#### 3.render()

render()方法是必需的。当他被调用时，他将计算`this.props`和`this.state`，并返回以下一种类型： 

1. React元素。通过jsx创建，既可以是dom元素，也可以是用户自定义的组件。 
2. 字符串或数字。他们将会以文本节点形式渲染到dom中。 
3. null，什么也不渲染 
4. 布尔值。也是什么都不渲染。

如需与浏览器进行交互，请在 `componentDidMount()` 或其他生命周期方法中执行你的操作。保持 `render()` 为纯函数，可以使组件更容易思考。

```
注意:
如果 shouldComponentUpdate() 返回 false，则不会调用 render()。

```



#### 4. componentDidMount

`componentDidMount`在组件被装配后立即调用。初始化使得DOM节点应该进行到这里。

**通常在这里进行ajax请求**

如果要初始化第三方的dom库，也在这里进行初始化。只有到这里才能获取到真实的dom.



#### 5.shouldComponentUpdate(nextProps, nextState)

调用`shouldComponentUpdate`使React知道，组件的输出是否受`state`和`props`的影响。默认每个状态的更改都会重新渲染，大多数情况下应该保持这个默认行为。

在渲染新的`props`或`state`前，`shouldComponentUpdate`会被调用。**默认为`true`**。这个方法不会在初始化时被调用，也不会在`forceUpdate()`时被调用。返回`false`不会阻止子组件在`state`更改时重新渲染。

如果`shouldComponentUpdate()`返回`false`，`componentWillUpdate`,`render`和`componentDidUpdate`不会被调用。

```
此方法仅作为性能优化的方式而存在。不要企图依靠此方法来“阻止”渲染，因为这可能会产生 bug。你应该考虑使用内置的 PureComponent 组件，而不是手动编写 shouldComponentUpdate()。PureComponent 会对 props 和 state 进行浅层比较，并减少了跳过必要更新的可能性。
如果你一定要手动编写此函数，可以将 this.props 与 nextProps 以及 this.state 与nextState 进行比较，并返回 false 以告知 React 可以跳过更新。

```



#### 6.getSnapshotBeforeUpdate(prevProps, prevState)

在react `render()`后的输出被渲染到DOM之前被调用。它使您的组件能够在它们被潜在更改之前捕获当前值（如滚动位置）。这个生命周期返回的任何值都将作为参数传递给componentDidUpdate（）。



#### 7.componentDidUpdate(prevProps, prevState, snapshot)

`componentDidUpdate()` 会在更新后会被立即调用。首次渲染不会执行此方法。

当组件更新后，可以在此处对 DOM 进行操作。如果你对更新前后的 props 进行了比较，也可以选择在此处进行网络请求。（例如，当 props 未发生变化时，则不会执行网络请求）。

```
componentDidUpdate(prevProps) {
  // 典型用法（不要忘记比较 props）：
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}

```

如果组件实现`getSnapshotBeforeUpdate()`生命周期，则它返回的值将作为第三个“快照”参数传递给`componentDidUpdate()`。否则，这个参数是`undefined`。

```
注意:
如果 shouldComponentUpdate() 返回值为 false，则不会调用 componentDidUpdate()。

```



#### 8.componentWillUnmount()

`componentWillUnmount()` 会在组件卸载及销毁之前直接调用。在此方法中执行必要的清理操作，例如，清除 timer，取消网络请求或清除在 `componentDidMount()` 中创建的订阅等。

`componentWillUnmount()` 中**不应调用 `setState()`**，因为该组件将永远不会重新渲染。组件实例卸载后，将永远不会再挂载它。

## react事件处理

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写。

```react
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

**在 React 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。你必须显式的使用 `preventDefault`**

```react
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```



## [Props属性验证](https://react.docschina.org/docs/typechecking-with-proptypes.html )



```
import One from "./components/one"
class App extends Component{
  render(){
    let userArr = [
      {id:1,sex:"男"},
      {id:2,sex:"女"}
    ]
    return (
      <div>
        <One num={true} userArr={userArr}/>
      </div>
    )
  }
}

```



One组件：

```
//定义组件的默认属性
//优先级比较低 如果外部传入同名属性，就会将其覆盖掉
static defaultProps = {
	num:100
}

static propTypes = {  
    //限定外部传入的num属性可以是number/string/boolean类型的
    num: PropTypes.oneOfType([PropTypes.number,PropTypes.string,PropTypes.bool]),
    //规定了外部必须传入一个userArr的数组，结构是一个对象，
    //对象里面包含两个字段分别是id:number.isRequired,sex:string.isRequired
    userArr:PropTypes.arrayOf(PropTypes.shape({
        id:PropTypes.number.isRequired,
        sex:PropTypes.string.isRequired   
    })).isRequired
}

```





## [Context](https://react.docschina.org/docs/context.html)

> Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。

使用 context 的通用的场景包括管理当前的 locale，theme，或者一些缓存数据，这比替代方案要简单的多

props单向数据流动：

![图片描述](https://segmentfault.com/img/bVblBU2?w=1564&h=808)





如果觉得Props传递数据很繁琐，可以采用context,进行跨组件传递数据

![图片描述](https://segmentfault.com/img/bVblB1c?w=1560&h=792)



moneyContext:

```
import {createContext} from 'react';
let moneyContext = createContext()
let {
  Provider,
  Consumer  
} = moneyContext

export default {
    Provider,
    Consumer
}
```



App.js

父子传值

```
import React,{Component} from 'react';
import ContextParent from "./ContextParent"
import moneyContext from "./moneyContext"

class App extends Component{
  state = {
    money:100
  }
  render(){
    return (
      <moneyContext.Provider value={{  //提供者的value属性可以给所有的后代元素提供数据
        money:this.state.money
      }}>
        <ContextParent />
      </moneyContext.Provider>
    )
  }
}

export default App;

```



ContextParent

```
import React, { Component,createContext } from 'react'
import GrandChild from "./GrandChild"

import moneyContext from "./moneyContext"
export default class ContextParent extends Component {
    render() {
        return (
               //通过公共实例的Context的Consumer，内部子元素写成一个函数，参数就可以获取value值了
                <moneyContext.Consumer>
                    {
                        (value)=>{
                            return (
                                <div>
                                    ContextParent组件获取App传递来的money === {value.money} //传递的值有
                                    <GrandChild />
                                </div>
                            )
                        }
                    }
                </moneyContext.Consumer>
        )
    }
}

```



GrandChlid

```
import React, { Component } from 'react'
import moneyContext from "./moneyContext"
export default class GrandChild extends Component {
    render() {
        return (
            <moneyContext.Consumer>
                {
                    value=>{
                        return (
                            <div>
                                我是GrandChild组件---{value.money}
                            </div>
                        )
                    }
                }
            </moneyContext.Consumer>
        )
    }
}

```



## [redux](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)

管理数据

React 只是 DOM 的一个抽象层，并不是 Web 应用的完整解决方案。有两个方面，它没涉及。

- 代码结构 
- 组件之间的通信

2014年 Facebook 提出了 Flux 架构的概念，引发了很多的实现。2015年，Redux 出现，将 Flux 与函数式编程结合一起，很短时间内就成为了最热门的前端架构。

如果你不知道是否需要 Redux，那就是不需要它

只有遇到 React 实在解决不了的问题，你才需要 Redux

简单说，如果你的UI层非常简单，没有很多互动，Redux 就是不必要的，用了反而增加复杂性。

- 用户的使用方式非常简单
- 用户之间没有协作
- 不需要与服务器大量交互，也没有使用 WebSocket
- 视图层（View）只从单一来源获取数据

需要使用redux的项目:

- 用户的使用方式复杂
- 不同身份的用户有不同的使用方式（比如普通用户和管理员）
- 多个用户之间可以协作
- 与服务器大量交互，或者使用了WebSocket
- View要从多个来源获取数据

从组件层面考虑，什么样子的需要redux：

- 某个组件的状态，需要共享

- 某个状态需要在任何地方都可以拿到

- 一个组件需要改变全局状态

- 一个组件需要改变另一个组件的状态

  

### redux的设计思想

1. Web 应用是一个状态机，视图与状态是一一对应的。

2. 所有的状态，保存在一个对象里面（唯一数据源）。

     

### redux的流程

1.store通过reducer创建了初始状态
2.view通过store.getState()获取到了store中保存的state挂载在了自己的状态上
3.用户产生了操作，调用了actions 的方法
4.actions的方法被调用，创建了带有标示性信息的action
5.actions内部通过调用**store.dispatch**方法将标志性的action发送到了reducer中
6.reducer接收到action并根据标识信息判断之后返回了新的**state**
7.store的state被reducer更改为新state的时候，store.subscribe方法里的回调函数会执行，此时就可以通知view去重新获取state

> 注意：flux、redux都不是必须和react搭配使用的，因为flux和redux是完整的架构，在学习react的时候，只是将react的组件作为redux中的视图层去使用了。



### reducer是纯函数

reducer是state最终格式的确定。它是一个纯函数，也就是说，只要传入参数相同，返回计算得到的下一个 state 就一定相同。

没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。
reducer对传入的action进行判断，然后返回一个通过判断后的state，这就是reducer的全部职责



**Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出。**

**纯函数是函数式编程的概念，必须遵守以下一些约束。**

**不得改写参数**

**不能调用异步的API**

**不能调用Date.now()或者Math.random()等不纯的方法，因为每次会得到不一样的结果**

由于 Reducer 是纯函数，就可以保证同样的State，必定得到同样的 View。但也正因为这一点，Reducer 函数里面不能改变 State，必须返回一个全新的对象，请参考下面的写法。

```
// State 是一个对象
function reducer(state, action) {
  return Object.assign({}, state, { thingToChange });
  // 或者
  return { ...state, ...newState };
}

// State 是一个数组
function reducer(state, action) {
  return [...state, newItem];
}

```

最好把 State 对象设成只读。你没法改变它，要得到新的 State，唯一办法就是生成一个新对象。这样的好处是，任何时候，与某个 View 对应的 State 总是一个不变的对象。





### redux有四个组成部分

**store：用来存储数据** 
**reducer：真正的来管理数据**
**actionCreators：创建action，交由reducer处理**

**view： 用来使用数据，在这里，一般用react组件来充当**

### ![](https://s1.ax1x.com/2020/09/05/wEkeeK.jpg)



1. 创建store

   从redux工具中取出createStore去生成一个store

2. 创建一个reducer，然后将其传入到createStore中辅助store的创建

   reducer是一个纯函数，接收当前状态和action，返回一个状态，返回什么，store的状态就是什么，需要注意的是，不能直接操作当前状态，而是需要返回一个新的状态

   想要给store创建默认状态其实就是给reducer一个参数创建默认值

3. 组件通过调用store.getState方法来使用store中的数据

4. 组件产生用户操作，**调用actionCreator的方法创建一个action**，利用store.dispatch方法传递给reducer

   store只是一个仓库，并没有管理能力，会把接受到的action转发给reducer

   ```react
   changeValue(e){
       const action ={
           type:'changevalue',
           value:'e.target.value'
       }
       store.dispatch(action)
   }
   ```

   

5. reducer**对action上的标示性信息做出判断后对新状态进行处理**，然后返回新状态，这个时候store的数据就会发生改变    reducer返回什么状态，store.getState就可以获取什么状态

   ```react
   export default (state = defaultState,action)=>{  
   if(action.type === 'changeInput'){
       let newState = JSON.parse(JSON.stringify(state)); //需要使用深拷贝 
       newState.inputValue = action.value;
       return newState;
       return state //返回给store
       }
   }
   
   ```

   

6. 我们可以在组件中，**利用store.subscribe方法去订阅数据的变化**，也就是可以传入一个函数，当数据变化的时候，传入的函数会执行，在这个函数中让组件去获取最新的状态

```react
constructor(props){
    this.state = store.getState()
    store.subscribe(this.storeChange) //订阅Redux的状态 发生改变触发
}

this.storeChange=()=>{  //注意使用箭头函数 this转向
    this.setState(store.getState())
}

```

步骤(不看即可)

	1. src/store/index.js

```
import { createStore } from 'redux';
import reducer from "./reducer"
//创建了store仓库，借助外部传入的reducer纯函数
const store = createStore(reducer)  
export default store
```

2. src/store/reducer.js

   ```
   
   let state = {  //规定了redux的一些初始化的共享状态
       list:[
           {id:1,title:"今天星期一，新的一天背代码"},
           {id:2,title:"明天星期二，新的一天背代码"}
       ]
   }
   
   //Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。
   //Reducer是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出
   //注意：不能对之前的状态进行任何的更改，内部只能是同步的操作！ 不能有 Math.random()  new Date()
   //内部要求 状态与视图是一一对应的，只要外部传入的状态不变，所对应的的视图也不应该发生改变！
   const reducer = (prevState = state,action)=>{
       let newState = {...prevState}  //newState={list:[]}
       return newState;
   }
   
   export default reducer;
   ```

   

3. index.js

   ```
   import React from 'react';
   import ReactDOM from 'react-dom';
   import App from './App';
   
   import store from "./store"
   //reducer函数返回什么内容，store.getState()就可以获取什么内容
   // console.log("store===>",store.getState())
   ReactDOM.render(
     <App />,
     document.getElementById('root')
   ```

   

4. src/todolist/TodoContent

   ```
   import React, { Component } from 'react'
   import store from "../../store"
   export default class TodoContent extends Component {
       constructor(){
           super()
           this.state = {
               list:[]
           }
       }
       componentDidMount(){
           //如何获取reducer的返回结果
           this.setState({
               list:store.getState().list
           })
       }
       render() {
           let {list} = this.state;
           return (
               <ul>
                   {
                       list.map(item=>{
                           return <li key={item.id}>{item.title}</li>
                       })
                   }
               </ul>
           )
       }
   }
   
   ```

   

5. todolist/TodoInput

   ```
   import React, { Component } from 'react'
   import actionCreators from "../../store/actionCreators"
   export default class TodoInput extends Component {
       
       handleKeyUp = e=>{
           if(e.keyCode === 13){
               //目标：需要将redux的list再去添加一项。更改redux状态，必须通过派发action才可以
               actionCreators.addNewTodo(e.target.value)
               e.target.value = ""
           }
       }
       render() {
           return (
               <input onKeyUp={this.handleKeyUp} placeholder="请输入内容..."/>
           )
       }
   }
   
   ```

   

6. 定义了actionCreators

   ```
   import store from "./index"
   const actionCreators = {
       addNewTodo(title){  //actionCretors or action区别？
           //需要定义一个具有特殊标识的action对象
           let action = {
               type:"addNewTodo",
               title
           }
           //需要将action对象派发给reducer
           store.dispatch(action)
       }
   }
   
   export default actionCreators
   ```

   

7. reducer进行处理

   ```
   
   let state = {
       list:[
           {id:1,title:"今天星期一，新的一天背代码"},
           {id:2,title:"明天星期二，新的一天背代码"}
       ]
   }
   
   //Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。
   //Reducer是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出
   //注意：不能对之前的状态进行任何的更改，内部只能是同步的操作！ 不能有 Math.random()  new Date()
   //内部要求 状态与视图是一一对应的，只要外部传入的状态不变，所对应的的视图也不应该发生改变！
   const reducer = (prevState = state,action)=>{
       let newState = {...prevState}  //newState={list:[]}
       switch (action.type) {
           case "addNewTodo":
               newState.list.push({id:handler.getId(newState.list),title:action.title})
               break;
           default:
               break;
       }
       return newState;
   }
   
   
   const handler = {
       getId(list){
           list = list.slice()
           if(list.length ===0) return 1;
           return list.sort((a,b)=>{ //list=[{id:3},{id:2}]
               return b.id - a.id
           })[0].id+1
       }
   }
   
   
   export default reducer;
   ```

   

8. TodoInput里面调用actionCreator方法

   ```
   import React, { Component } from 'react'
   import actionCreators from "../../store/actionCreators"
   export default class TodoInput extends Component {
       
       handleKeyUp = e=>{
           if(e.keyCode === 13){
               //目标：需要将redux的list再去添加一项。
               //内部通过store.dispatch(action) ==> reducer(switch(action.type))
               actionCreators.addNewTodo(e.target.value)
               e.target.value = ""
           }
       }
       render() {
           return (
               <input onKeyUp={this.handleKeyUp} placeholder="请输入内容..."/>
           )
       }
   }
   
   ```

   

9. TodoContent

   因为redux状态改变了，但是视图仍然还是之前的。所以需要store.subscribe方法订阅redux状态的变化。

   ```
   componentDidMount(){
           //如何获取reducer的返回结果
           this.setState({
               list:store.getState().list
           })
           
           //当redux的状态发生改变了，组件默认是监听不到的
           //订阅状态改变，当redux状态发生改变了，内部回调仍然执行
           store.subscribe(()=>{
               this.setState({
                   list:store.getState().list
               })
           })
       }
   ```






### 划分Reducer

在一个复杂的尤其是单页面的应用中，为了提高开发效率，我们都会采取协同开发的模式，因为系统的模块较多，各个大的功能板块都较为独立，而redux有一个思想：单一数据源，也就是store只能有一个。

所以，我们多会使用划分reducer的方法，将每个大板块所需维护的状态划分在不同的reducer中去管理，分别有自己的一套结构，**再通过combineReducers合并在一起**

**需要注意的是，划分reducer之后，store会将数据也去根据划分之后的reducer来进行分开管理**



src/store/todolist  ----> 放置todolist相关的actionCreators/actionType/reducer



src/store/reducer.js

```
import {combineReducers} from "redux"
//引入todolist自己的reducer文件
import todolist from "./todolist/reducer"
const reducer = combineReducers({
    todolist   //后续组件获取redux管理的list数据： store.getState().todolist.list
})
export default reducer

```

合并完成之后，更改了一下引入的路径。



在组件里面TodoInfo里面获取redux管理的状态，本来是可以通过 store.getState().todos就可以获取。但是划分模块之后，再想要获取redux状态的话，需要通过store.getState().模块名.todos才可以。

```
	constructor(){
        super()
        this.state = {
            todos:store.getState().todolist.todos
        }
    }

    componentDidMount(){
        //redux状态了，需要组件订阅
        store.subscribe(()=>{
            this.setState({
                todos:store.getState().todolist.todos
            })
        })
    }

```









### [react-redux](https://react-redux.js.org/)

为啥要使用react-redux桥梁 将 redux 与 react进行连接？

1. 每个组件如果需要使用redux状态，都需要引入store,store.getState()
2. 当redux状态发生改变的时候，对于react组件不知道，需要通过手动订阅才可以（store.subscribe）
3. actionCreators这些方法都不纯粹，因为不仅创建action还得派发action给reducer(store.dispatch)



cnpm install react-redux -S

> 核心组件：
>  **Provider  提供者  属性上通过store将数据派给容器组件**
>  **connect    用于连接容器组件与UI组件**

​	  `connect() 返回一个函数，函数参数接收UI组件，返回容器组件`  

​     

> connect(mapStateToProps,mapDispatchToProps)(ui组件)

> ​    容器组件内部帮你做了 store.subscribe() 的方法订阅
> ​    状态变化 ==> 容器组件监听状态改变了 ==> 通过属性的方式传给UI组件
>
> ​    把`store.getState()`的状态转化为展示组件的`props`使用

​    

  转化为展示组件`props`上的属性

```
const mapStateToProps = state=>{
	return state.todolist
}

```



​    转化为展示组件`props`上的方法 

```
const mapDispatchToProps = dispatch=>{
	return {
		a(){
			let action = actionCreators.xxx()
			dispatch(action)
		}
	}
}

or

const mapDispatchToProps = actionCreators //将所有的方法全都绑定props并且进行派发了

```







### [redux中间件](https://www.jianshu.com/p/a27ab19d3657)

   

通常情况下，action只是一个对象，不能包含异步操作，这导致了很多创建action的逻辑只能写在组件中，代码量较多也不便于复用，同时对该部分代码测试的时候也比较困难，组件的业务逻辑也不清晰，使用中间件了之后，可以通过actionCreator异步编写action，这样代码就会拆分到actionCreator中，可维护性大大提高，可以方便于测试、复用，同时actionCreator还集成了异步操作中不同的action派发机制，减少编码过程中的代码量



> **做异步的操作在action里面去实现！需要安装redux中间件**
> **redux-thunk**   redux-saga   redux-promise



**redux-thunk原理：**

可以看出来redux-thunk最重要的思想，就是可以接受一个返回函数的action creator。如果这个action creator 返回的是一个函数，就执行它，如果不是，就按照原来的next(action)执行。
正因为这个action creator可以返回一个函数，那么就可以在这个函数中执行一些异步的操作。**换言之，redux的中间件都是对store.dispatch()的增强** 



**dispatch一个action之后，到达reducer之前，进行一些额外的操作，就需要用到middleware**。你可以利用 Redux middleware 来进行日志记录、创建崩溃报告、调用异步接口或者路由等等。





### 高阶组件

高阶函数：一个函数内部返回一个新的函数，内部采用闭包的写法。

```
var add = x => {
  return y => {
  	return x+y
  }
}
//调用add
add(3)(1)

```



> 高阶组件：（HOC） Higher-Order-Component
>
> 高阶组件本质上就是一个函数，内部可以接收一个组件，然后返回新的组件。
>
> 例如： React.memo()    connect()

组件类型？ 

​          类组件 （生命周期钩子、状态）     

​         函数式组件（无状态组件） hooks useRef  useState 

​          form: 受控组件 vs  非受控组件

​	  HOC: 高阶组件  connect()     React.memo(函数式组件)  / 类组件+shouldComponent/PureComponent

HOC不要改变原始组件。使用组合

封装一个具有版权信息的高阶组件WithCopy,内部接收一个组件，最终返回一个新的组件。

```
import React, { Component } from 'react'

//定义一个高阶组件WithCopy 本质上是一个函数，接受一个组件，返回一个全新的组件。
//connect()(UIComponent)  只需要通过this.props.xxx可以获取到传递来的属性了
//类组件 函数式组件（无状态组件）
//表单元素而言  受控、非受控
//HOC高阶组件 ：redux中connect()  React.memeo(functional component)  Purecomment的使用
const WithCopy = Comp=>{
    return class WithCopyComp extends Component{
        render(){
            return (
                <div>
                    <Comp name={this.props.name}/>
                    版权信息&copy;
                </div>
            )
        }
    }
}
export default WithCopy
//HOC
function logProps(WrappedComponent) {
  return class extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('Current props: ', this.props);
      console.log('Previous props: ', prevProps);
    }
    render() {
      // 将 input 组件包装在容器中，而不对其进行修改。Good!
      return <WrappedComponent {...this.props} />;
    }
  }
}
```

注意

可能已经注意到HOC与**容器组件模式**之间有相似之处。容器组件担任分离将高层和低层关注的责任，由容器管理订阅和状态，并将丙传递给处理渲染UI.HOC使用容器作为其实现的部件，你可以将 HOC 变成参数化容器组件。











### 对于CRA的定制

​	因为我们发现，调用高阶组件的时候采用withCopy(About)代码，但是不够简洁优雅。

使用vant进行定制

​	那么我们可以采用装饰器的写法实现调用高阶组件

​	

```
@WithCopy
class About extends Component {
    render() {
        return (
            <div>
                about -- {this.props.a}
            </div>
        )
    }
}


```

很不幸，目前的cra是不支持这种写法，我们需要单独进行定制，让其支持这种写法。



[Antd中提供了社区解决方案](https://ant.design/docs/react/use-with-create-react-app-cn)

1. yarn add @craco/craco

2. 对脚手架进行轻微的调整

   ```
   "scripts": {
   -   "start": "react-scripts start",
   -   "build": "react-scripts build",
   -   "test": "react-scripts test",
   +   "start": "craco start",
   +   "build": "craco build",
   +   "test": "craco test",
   }
   
   ```

   

3. yarn start启动项目发现报错了，原因是因为根路径下面缺少 craco.config.js文件

```
/* craco.config.js */
module.exports = {
  // ...
};

```

   

1. 自定义主题

   index.js文件中：

```
import 'antd/dist/antd.less';

```

​	

然后安装 `craco-less` 并修改 `craco.config.js` 文件如下。

yarn add craco-less

```
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': 'yellow' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};

```





[后续CRA支持装饰器需要这样配置](https://blog.csdn.net/lucky569/article/details/107253310/)：

yarn add @babel/plugin-proposal-decorators

在craco.config.js文件中新增以下代码即可:

```
babel: {
   plugins: [["@babel/plugin-proposal-decorators", { legacy: true }]]
},

```



区别

1.mvvm  view



2.v-xxx      js实现map     react的思路是all in js，通过js来生成html，所以设计了jsx，还有通过js来操作css，社区的styled-component、jss等，

3.双向数据绑定  数据驱动图   react单向数据流   setState更新

4.

其实就会发现 react面向社区化的。它把一些常用到的包都放在社区，用到的话单独去查找去进行相应的配置。

vue的话面向官方化，很多东西内部都帮助我们去实现了。 vue.config.js文件  标准









## [React-Router](https://reacttraining.com/react-router/)

最新的路由的版本是5.2的版本。里面的话提供了一些包

所在在做web端开发的时候只需要安装react-router-dom就可以了，因为内部已经包含了最核心的内容了。

react-router | react-router-native | react-router-config

外面套用Switch作路由匹配，当路由组件检测到地址栏与Route的path匹配时，就会自动加载响应的页面。

### 路由的简单使用

​    安装路由： yarn  add react-router-dom

​    需要在最外层的节点上面：（hash vs history）

```
import {HashRouter as Router} from "react-router-dom"
ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);


```

​    

​	使用Route实现路由

```
import React,{Component} from 'react';
import {Route,Redirect,Switch} from "react-router-dom"
import Home from "./views/Home"
import Article from "./views/Article"
//文章列表
import NotFound from "./views/NotFound"

//Route指代路由对象，path匹配路径，component代表路由组件  exact就是将地址栏与path必须完全一致
//Redirect重定向 to跳到指明的路径
//Switch 内部的路由只要匹配一个就结束了
class App extends Component{
  render(){
    return (
      <Switch>
        <Route path="/home" component={Home}/>
        <Route path="/article" component={Article}/>
        <Route path="/404" component={NotFound}/>
        <Redirect to="/home" from="/" exact/>   
        <Redirect to="/404"/>
      </Switch>
    )
  }
}
export default App;

```



声明式导航 （vue中router-link实现的）

可以通过NavLink实现a标签的切换效果，渲染成a标签，并且带有active的class样式

```
import {Route,Redirect,Switch,NavLink as Link} from "react-router-dom"

<Link to="/home" activeStyle={{color:'red'}}>首页</Link>
<Link to="/article" activeStyle={{color:'red'}}>文章</Link> 
```









### 二级路由与动态跳转



二级路由：

Article文件：

```
import React, { Component } from 'react'
import {Route,NavLink as Link} from "react-router-dom"
import ArticleDetail from './ArticleDetail';
export default class Article extends Component {
    render() {
        return (
            <div>
                <Link to="/article/1">文章一</Link>
                <Link to="/article/2">文章二</Link>
                <Route path="/article/:id" component={ArticleDetail}/>
            </div>
        )
    }
}
```



ArticleDetail中如何获取动态参数？

因为ArticleDetail被Route进行包裹，就是路由组件了。它的属性上面就会有路由相关的api

```
import React, { Component } from 'react'

export default class ArticleDetail extends Component {
    render() {
        //history/location/match的路由api了。
        return (
            <div>
                文章详情 -- {this.props.match.params.id}
            </div>
        )
    }
}
```





### 路由常用的api方法

#### Route中的render函数

​	一旦通过Route组件的component属性指明的组件，那么这个路由组件上面就会有路由相关的api

​    (location / history / match)

​	如果必须要传入额外属性的话，单纯使用component是解决不了的。

 

```
<Route path="/home" render={(routeProps)=>{
	return this.state.isLogin ? <Home {...routeProps} a={1}/> : "未登录"
}}/>
```





#### link的参数传递

​	1.可以通过动态路由的方式进行参数传递

​			path="/detail/:id"

​			Detail组件内部可以通过 **this.props.match.params.id**可以获取到动态参数



​	2.可以通过query进行传参

​			path="/detail?title=文章一"

​			Detail组件内部可以通过  **this.props.location.search**可以获取到 “?title=文章一”



​	3.可以通过state进行隐式传参

​		   to={{pathname:'/detail/2',state:{title:'文章2'}}}

​		   Detail组件内部可以通过  **this.props.location.state.title**可以获取到 





#### withRouter （HOC：React.memo()   connect()   withRouter）



> 我们可以通过引入高阶组件withRouter,将普通组件进行包裹，那么BackHome就变成了伪路由组件，它本身不能实现跳转，但是仍然可以通过属性去访问到路由相关的api了。

```
import React, { Component } from 'react'
import {withRouter} from "react-router-dom"

//withRouter(BackHome) 本来BackHome是一个普通组件，属性上面啥也没有。但是通过HOC withRouter包裹之后，这个BackHome就变成了一个伪路由组件，本身是不会跳转进来，只不过属性上面却有了路由相关的api。
@withRouter
class BackHome extends Component {

    back = ()=>{
        //通过编程式导航方式返回首页
        this.props.history.push("/home")
    }

    render() {
        return (
            <div>
                <button onClick={this.back}>返回home</button>
            </div>
        )
    }
}
export default BackHome

```





