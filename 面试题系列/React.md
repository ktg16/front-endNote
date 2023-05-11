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

### 3.setState是异步还是同步

1.我的回答是执行过程代码同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形式了所谓的“异步”，所以表现出来有时是同步，有时是“异步”。

之所以会有异步的表现是因为react框架本身的性能机制所导致的。因为每次调用setState都会触发更新，异步操作是为了提高性能，将多个状态合并一起更新，减少re-render调用。

#### 1、react中的核心算法react Fiber作用

React.Fiber的方法很简单---分片。将用时很长的任务分成很多小片，每一个小片的用时耗时很短，虽然总任务的时间依然很长，但是在每一个小片执行完成之后，都会给其他小片执行的机会，这样唯一的线程就不会拥堵，其他任务依然有运行的机会

#### 2、jsx内部编译原理

1、编写jsx代码

2、jsx代码内部通过babel提供的核心方法react.createElement()

3、将jsx代码转成虚拟dom

4、ReactDOM.render()将虚拟dom转成真实dom

JSX代码 — > 使用react构造组件，bable进行编译（React.createElement方法）—> JavaScript对象（虚拟dom） — `ReactDOM.render()函数进行渲染`—>真实DOM元素 —>插入页面

#### 3、react中如何遍历数组，通过map迭代

key很关键！！！

key帮助React识别哪些元素改变了，比如被添加或者删除，因此应当给数组中的每一个元素赋予一个确定的标识

虚拟dom对比的时候，加key可以避免出错。如果不加key，当一个元素添加的时候，后面的元素就会经历卸载与重新加载的过程

为了避免出错，所以我们在开发过程中应该尽量避免用index作为key值，除非我知道index是不变的

key 是给每一个 vnode 的唯一 id,可以依靠 key,更准确,更快的拿到 oldVnode 中对 应的 vnode 节点

#### 4、React高性能的原理：

在改变数据变化时，React都会重构整个虚拟dom树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行真实DOM的更新。

尽管每一次都需要构造完整的虚拟DOM树，但因为虚拟DOM是存在于内存数据，性能是极高的，而对实际DOM的操作仅仅是Diff部分，因而能够达到提高性能的目的

#### 5、react中数据改变，视图层不会发生变化，应该用什么函数？

setState，通过该函数，就可以实现数据改变，视图层也发生变化，但也存在小BUG，同时运行多个setState时，不会逐个运行，就像Object.assign的浅拷贝一样，后面调用的setState会覆盖同一周期的setState

#### 6、如果后续状态取决于当前状态，我们建议使用updater函数的形式代替

```html
this.setState((prevState)=>{
                return{
                count:prevState.count+1
            }
        })
```



#### 7、setState两种写法的区别

（1）在类组件中，通过this.setState({count:this.state.count+1})

​		***内部经过Object.assign()在一个短时间内进行合并***，例如添加商品，看似多次，实际只添加一次

（2）在方法组件中，通过使用useState这个hooks去定义状态

```
const [count,setCount]=React.useState(1)
setCount(count+1)
```

相当于类组件中的写法：

```
constructor{
	super()
	this.state={
		count:1
	}
}
setCount=()=>{
	this.setState({
		count:this.state.count+1
	})
}
```

#### 8、受控组件和非受控组件

受控组件：受到数据的控制，使得React成为唯一的数据源

```
        class App extends React.Component{
            constructor(){
                super()
                this.state={
                    value:'123'
                }
            }
            submit=(e)=>{
                e.preventDefault()
                console.log(this.state.value)
            }
            handleChange = (e)=>{
                this.setState({
                    value:e.target.value
                })
            }
            render(){
                return (
                    <div>
                        <form onSubmit={this.submit}>
                            <input type="text" value={this.state.value} onChange={this.handleChange} />
                            <p>{this.state.value}</p>  
                            <input type="submit" />
                        </form>    
                    </div>
                    )
                }
        }
        ReactDOM.render(<App/>,document.getElementById("app"))
```

非受控组件：只需要在DOM元素上通过ref进行绑定取值即可

```
class App extends  React.Component{
            submit = (e)=>{
                e.preventDefault()
                console.log(this.textInput.value)
            }

            render(){
                return(
                    <div>
                        <form onSubmit={this.submit}>
                            <input type="text" name="123" ref={el=>this.textInput=el}/>
                            <input type="submit"/>    
                        </form>    
                    </div>
                )
            }
        }
ReactDOM.render(<App/>,document.getElementById("app"))
```



#### 9、jsx的特性

1、 1）标签必须要闭合 <input/>
 2) 在外层只能有一个根元素
 3) class ==> className
 4) style ==> {{backgroundColor:'red'}}
 5) onClick
    onClick={()=>{alert(1)}}
    注意： this的指向  建议采用箭头函数（因为箭头函数内部的this与定义这个函数的外部this是同一个）

6）input的value值

```
<input value={this.state.value} onChange={(e)=>{this.setState({value:e.target.value})}} />
```

如果只是简单的显示值，就用defaultvalue，

7）checkbox checked必须配合onChange事件，写成受控组件的形式，否则就采用defaultchecked

8）label的属性 for==>htmlFor

9）jsx的注释：{/* jsx代码*/}

10）jsx的原理：将编写的jsx代码通过babel的React.CreatElement方法编译成虚拟dom，进而通过ReactDOM.render方法将虚拟dom渲染成真实dom



#### 10、父子组件通信

父组件通过属性的方式将将自己的状态传递给子组件，子组件通过props接受父组件的状态

#### 11、子父组件通信

父组件可以将一个更改自身状态的方法(回调函数)传递给子组件，然后子组件通过props接收后进行调用，相当于父组件的方法被执行了，从而改变自身的状态

#### 12、兄弟组件通信

如果是兄弟组件之间的传递，则父组件作为中间层来实现数据的互通，通过使用父组件传递

在父组件设置状态及修改状态的函数，传递给子组件



#### 12.2 父组件向后代组件传递 

使用`context`提供了组件之间通讯的一种方式，可以共享数据，其他数据都能读取对应的数据

通过使用`React.createContext`创建一个`context`

#### 13、 mock数据工具 - json-server (可以将本地的一个json文件启动起来，做成一个接口服务)

​    https://gitee.com/rh_hg/json-server?_from=gitee_search
​        npm i json-server -g
​        json-server --version
​        json-server .\data.json --port 4000 -w

#### 14、很多事件方法内，通过bind绑定数据来传值

#### 15、react中代理的配置

如果后端没有帮助我们配置跨域处理，需要我们前端手动的进行代理配置
    

```
node_modules>react-scripts>config>devServer.js
    proxy:{
        "/api":{
            target:"http://47.96.0.211:9000",
            changeOrigin:true,
            pathRewrite:{
            "^/api":""
            }
        }
    }
```

​    但是有问题？ 后续安装新的模块的时候，内部yarn.lock文件实时的检测node_modules下面的文件是否手动的
​    更改过，如果更改的话，重新变成初始状态。


    解决方案一：
        可以通过 yarn eject 进行react-scripts相关配置文件的抽离操作。 
        报错？
          .git删掉
    
          git init
          git add *
          git commit -m "first commit"
          git push  
          再去进行 yarn eject  Y  
    
    解决方案二：
        yarn add http-proxy-middleware
        安装之前创建
        src/setupProxy.js
        const { createProxyMiddleware } = require('http-proxy-middleware');
    
        module.exports = function(app){
            app.use("/api",
                createProxyMiddleware({ target: 'http://47.96.0.211:9000', changeOrigin: true , pathRewrite:{ "^/api":"" } })
            )
        }


#### 16、React挂载阶段的钩子函数：

##### 1、constructor

***只在初始化的时候执行一次***

**作用：**

**1、可以用来初始化组件状态。2可以给一些事件函数绑定this **

##### 2、getDerivedStateFromProps

在这个钩子函数里面，钩子函数属于类，前面需要加static修饰，所以不能访问this

这个方法返回会什么，状态里的属性就会变成什么

如果你的组件的某个状态就想由外部传入的属性进行关联控制，希望属性变化了，组件内部的状态也发生变化，那么就把这个状态变成派生状态，使用此钩子函数即可，这样，组件内部不能改变该属性。

##### 3、render

render什么时候被执行？

1初始化的时候被执行。2当组件内部调用setState时。3当外部调用props改变时。4forceUpdate（强制更新）时

##### 4、componentDidMount

只在初始化的过程中执行一次

#### 17、React挂载阶段废弃掉的钩子函数

17.x版本中不推荐使用的钩子函数

前面加UNSAFE

##### 1、componentWillMount

##### 内部为什么不进行异步请求？

这个钩子函数受到React16.x Fiber协调算法影响，异步渲染   导致这个钩子函数可能会执行多次，如果异步请求放在这里，执行多次显然是不科学的

##### 2、componentWillReceiveProps #####

##### 3、componentWillUpdate

#### 18.React更新阶段的钩子函数

**1、getDerivedStateFromProps**

在这个钩子函数里面，钩子函数属于类，前面需要加static修饰，所以不能访问this

这个方法返回会什么，状态里的属性就会变成什么

如果你的组件的某个状态就想由外部传入的属性进行关联控制，希望属性变化了，组件内部的状态也发生变化，那么就把这个状态变成派生状态，使用此钩子函数即可，这样，组件内部不能改变该属性。

**2、shouldComponentUpdate**（相当于一个过滤网，只将发生改变的数据进行render更新）（麻烦，建议下面 但要注意引用类型）

默认shouldComponentUpdate返回ture 因为每次都要使用咱们可以写PureComponent

询问是否进行更新操作，false，不进

行render重新渲染操作，通过减少render的执行次数来提升react的性能 默认钩子函数 

运行阶段钩子函数

在类组件中：

***Component+shouldComponentUpdate***===***PureComponent***

可以用PureComponent来实现，不过纯组件用的是浅拷贝，会判断地址是否一样：

​				基本类型：根据外部传入的数据，新的数据与旧的数据是否一致？如果一致，render就不会执行

  			  如果是纯组件 使用arr:[...this.state.arr,3]  创建一个地址 深拷贝 

引用类型：根据外部传入的数据，新的数据与旧的数据地址是否一致，render也不会执行

再去进行更新操作

在方法组件中

可以用***React.memo(functional Component)***

**3、render**

**4、getSnapshotBeforeUpdate**

必须配合componentDidUpdate一起使用，并且可以返回一个更新之前的值；一般用于聊天室的滚动

**5、componentDidUpdate**

轮播图的实例化在此函数当中，

##### 轮播图的实例化不能在componentDidMount的原因：

在该钩子函数当中请求数据后，在进行虚拟DOM的对比，对比成功后才会有真实DOM元素。如果将实例化放在componentDidMount中，name虚拟DOM对比的时候就会进行实例化，这样是不对的

#### 19、卸载阶段的钩子函数

1、componentWillUnmount

在删除组件前进行善后处理

需要调用ReactDOM

div中使用React.DOM.unmountComponentAtNode()

处理内存泄漏 还有关闭定时器与事件解绑 clearInterval(this.timer)

如果被<keep-alive>包裹

#### Context