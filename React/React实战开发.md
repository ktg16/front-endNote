## 前言

> React起源于 Facebook 的内部项目，是一个用于构建用户界面的JS库；核心专注于视图，目的实现组件化开发 。那什么是组件化开发呢？我们可以很直观的将一个复杂的页面分割成若干个独立的组件，每个组件包含自己的逻辑和样式，再将这些独立组件组合成完成一个复杂的页面，这样既减少了逻辑复杂度，又实现了代码的重用。在昨天，我偶然发现蜜雪冰城小程序的界面非常适合用来锻炼React初学者的能力，于是我花了一天多的时间写出来了一个大概的界面（后续功能会继续进行完善，大家如果觉得写的不错，可以点个赞或者收藏一下，谢谢大家）。

### 界面展示

![图片](https://mmbiz.qpic.cn/sz_mmbiz/H8M5QJDxMHpHR9icnImdZqHHP6Yfib1VLiar0ns7XSxLlJtTBvMD0iaNSRIEc1Aibjy8sWSJ9OpIUnukAic2836E9ljQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)

WPS图片拼图.png

> 因为时间的原因，目前只做出了三个界面，但都可以实现跳转，接下来就让我为大家介绍一下组件的制作过程把。

## 项目准备

首先为大家介绍一下我开发一个React组件所用到的一些技术栈

### 技术栈

> -   Html，CSS，JavaScript全家桶
>     
> -   antd-mobile
>     
> -   axios
>     
> -   classnames
>     
> -   prop-types
>     
> -   react/react-dom/react-router/react-router-dom
>     
> -   styled-components
>     
> -   swiper
>     

### 创建React项目

想要写好一个React项目，一个脚手架是必不可少的。常用的创建脚手架方式有两种

```
npm init vitejs/app
npm i -g create-react-app复制代码
```

我个人比较推荐使用第一种，对于第二种创建方式，他的优点很明显：

1.  项目就是工具，更加的简单和直接
    
2.  不需要安装额外的CLI工具，减少了使用成本
    
3.  更新方便，无需同时维护模板和CLI工具，也是目前最快的脚手架 但第二种方法使用的时间较久，目前还是很多人在使用的。所以大家选择用哪个都是可以的。
    

### 安装依赖

创建完脚手架，就要安装我们的依赖了，没有这些，我们的项目是运行不起来的哦。

```
npm i  //用来安装模块到node_module目录中npm i antd-mobile antd-mobile-icons // React开发时比较常用的一个组件库和图标库npm i axios // 一个HTTP请求库,用来做数据请求npm i classnames // 一个简单的JavaScript工具库，可以将不同的的classname联合在一起npm i prop-types // 可以用来校验父组件传递过来值的类型npm i react-dom react-router react-router-dom // 引入路由组件npm i styled-components //是一种通过JavaScript来编写CSS样式的解决方案npm i swiper // 一款轻量级的轮播图插件，以移动端为主，可以快速做出一个轮播图复制代码
```

### 项目文件夹创建

一个大型的项目，里面的文件往往非常之多，因此，合理的对每个文件进行分类就显得尤为重要。我的项目文件分类如下

![图片](https://mmbiz.qpic.cn/sz_mmbiz/H8M5QJDxMHpHR9icnImdZqHHP6Yfib1VLiaPLOun8S8DTQ7JctQ57GhCt8S6iaMDRI0klo4Jr5ysnafdqKMJJnjOww/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)多个文件夹各司其职，分工明确：

> 1.  api文件夹：主要存放我们需要的外界接口，通过这些接口，我们可以拿到外面的数据。
>     
> 2.  assets文件夹：主要存放一些静态资源，如图片，字体，以及默认的一些样式。
>     
> 3.  components文件夹：放置一些主要的组件，比如Header，Footer等。
>     
> 4.  config文件夹：主要负责页面标题的配置。
>     
> 5.  pages文件夹：放置一些次要的组件，大组件内部的一些小组件。
>     
> 6.  Routes文件夹：存放路由的一些配置，按照路由划分。
>     

## 功能展示

### 底部导航栏切换

当鼠标点击不同的按钮的时候，将被点击的按钮施加一个高亮的效果，同时切换上面的内容显示效果。实现代码如下：

```
import React from "react";import { Link, useLocation } from "react-router-dom";import { FooterWrapper } from "./style";import classnames from "classnames";const Footer = () => {  const { pathname } = useLocation();  return (    <FooterWrapper>      <Link        to="/home"        className={classnames({          active: pathname == "/home" || pathname == "/",        })}      >        <i className="iconfont icon-shouye"></i>        <span>首页</span>      </Link>      <Link to="/food" className={classnames({ active: pathname == "/food" || pathname == "/food/nearby" || pathname == "/food/often"})}>        <i className="iconfont icon-faxian"></i>        <span>点餐</span>      </Link>      <Link        to="/order"        className={classnames({ active: pathname == "/order" || pathname == "/order/ing" || pathname == "/order/back" || pathname == "/order/history"})}      >        <i className="iconfont icon-shouye1"></i>        <span>订单</span>      </Link>      <Link to="/mine" className={classnames({ active: pathname == "/mine" })}>        <i className="iconfont icon-wode"></i>        <span>我的</span>      </Link>    </FooterWrapper>  );};export default Footer;复制代码
```

主要实现原理是通过**Link**组件的**to**属性，在点击后将地址进行改变，达到切换不同页面的效果，此处还使用了**classnames**，在每个组件上添加一个动态的类，当地址与设置的值相同时，将**active**效果施加给对应的**Link**。但我在写**二级路由**的时候出现了一个问题：当_切换_二级路由的时候，对应底部的导航栏的_高亮效果消失了_。我思考了很久，发现是**pathname**匹配的问题，当切换二级路由的时候，地址数据改变，导致未匹配成功，所有我在后面加了二级路由的匹配，解决了这个bug，但代码的_阅读性_差了许多，后续我准备使用_正则表达式_进行优化。

### 二级路由跳转

```
<Routes>    <Route path="/" element={<Home />} />    <Route path="/home" element={<Home />} />    <Route path="/order" element={<Order />}>          <Route path="/order/ing" element={<Conduct />}/>          <Route path="/order/history" element={<History />}/>          <Route path="/order/back" element={<Back />}/>    </Route>    <Route path="/food" element={<Food />}>          <Route path="/food/nearby" element={<Nearby />} />          <Route path="/food/often" element={<Often />} />    </Route>    <Route path="/mine" element={<Mine />} /></Routes>复制代码
```

页面跳转部分的代码。注意：二级路由需要**嵌套**在一级路由中写，否则会跳转到新页面，不是在原来的页面上进行切换了。效果如图所示：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

erjiluyou.gif

跟一级路由一样，二级路由添加的样式为底部红线。由于数据拉取以及渲染总是需要一些时间，这时候屏幕一直白屏，_用户体验感_非常不好，于是在数据请求的时候设置了一个`showloading` 变量，来实现加载中的状态。

### weiper轮播图

> swiper 是一款轻量级的轮播图插件，可以支持pc端和移动端的使用，他可以快速的做出一个轮播图,十分方便快捷

```
useEffect(() => {    new Swiper(".home_info_banners", {      loop: true,      autoplay: {        delay: 2000,      },    });  }, []);复制代码
```

```
<Wrapper>      <div className="home_info_img">        <div className="home_info_banners swiper-container">          <div className="swiper-wrapper">            <div className="swiper-slide">              <p>                <img width="100%" src={LemonWater} alt="" />              </p>            </div>            <div className="swiper-slide">              <p>                <img width="100%" src={putao} alt="" />              </p>            </div>          </div>        </div>      </div>    </Wrapper>复制代码
```

这里给出部分代码，需要注意的是，在**useEffect**中，一定要在第二个参数位置放一个_空数组_，否则轮播效果会跟很鬼畜。主要是防止多次进行请求，也可以采用下面的方法解决：

```
let swiper = null;  useEffect(() => {    console.log("Swiper 不能多次实例化");    if (swiper) {      // 如果实例化了，就不new Swiper了      return;    }    new Swiper(".btn-banner", {      loop: true,      pagination: {        el: ".swiper-pagination",      },    })  })复制代码
```

通过定义一个**swiper**变量初始值为_null_，当**第一次**实例化的时候改变**swiper**的值，后面对**swiper**进行一个判定，如果已经请求过就退出，同样可以达到目的。

### 图标、表单、按钮

本项目多个地方采用了**antd-mobile**和**anto-mobile-icons**组件库的图标，表单以及按钮

![图片](https://mmbiz.qpic.cn/sz_mmbiz/H8M5QJDxMHpHR9icnImdZqHHP6Yfib1VLiaYAiagmaKxS1kfFiajSyzjOuAuWoUfaa9LwuEeg9JCfKGZ3sfia9VVTSqg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)

_6F~@3}R)S3W){@G`}_JZ2U.png

![图片](https://mmbiz.qpic.cn/sz_mmbiz/H8M5QJDxMHpHR9icnImdZqHHP6Yfib1VLiaI0hInkHyoIiaica8NDj7TnMu7Bs4h8EXwnDR5RicT7icJ3WOdeibAicLtIcA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)

sousuo.png

**antd-mobile**官网封装好了很多组件，可以很方便的利用，达到减轻工作量的目的，下面给出使用组件的部分代码

```
import { Wrapper } from "./style";import { EnvironmentOutline } from "antd-mobile-icons";import { Space } from "antd-mobile";<div className="header">      <Space wrap style={{ fontSize: 16 }}>        <EnvironmentOutline />      </Space>  <span>南昌市910724店</span></div>复制代码
```

效果如图：

![图片](https://mmbiz.qpic.cn/sz_mmbiz/H8M5QJDxMHpHR9icnImdZqHHP6Yfib1VLiakoTHxwpJqgKxR9cibibl1pSmedzBlKJWxic0Gvu1SN1wumhK1DBMaHwCA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)

nanc.png

### 数据请求

在做项目的时候，前端往往负责页面的构建，后端负责数据处理，并将处理好的数据返回给前端，前端在将数据渲染到页面上，前后端交流的通道就是接口，通过接口，前端就可以拿到后端返回的数据，但一个人做项目的时候，哪来的后端给我们接口呢，这就不得不提_**在线接口Mock工具fastmock**_了，使用这个工具，可以很方便的模拟出后端给我们的数据接口，下面将展示如何使用这个工具来请求数据：

1.  ```
    在数据请求_api文件夹_下的**request.js** 进行`axios 数据请求`
    ```
    

```
import axios from 'axios'export const getIce = () =>   axios.get(`https://www.fastmock.site/mock/041a1d09b8d07742f2a97acd41a35c2a/beers/ice`)复制代码
```

2.  ```
    在主页面的UseEffect中使用` async + await` 实现同步使用数据,数据拉取成功后，将数据作为变量传入对应组件.
    ```
    

```
const [title, setTitle] = useState(true) const openMap = () => {   setTitle(!title) }; const [message, setMessage] = useState([]) useEffect(() => {   (async () => {     let { data } = await getIce()     setMessage(data)     // console.log(data)   })() }, [])复制代码
```

3.  ```
    拿到了数据，再将数据传给子组件，由子组件进行渲染。
    ```
    

```
<IceBanner message={message}/>复制代码
```

4.  ```
    子组件通过父组件传过来的对象使用**map**方法将每一个对象分别解构出来，渲染到不同的界面
    ```
    

```
const IceBanner = ({ message }) => { const renderInfo = () => {   return message.map((item) => (     <div key={item.id} className="sale-box">       <div className="left">         <div className="name">{item.name}</div>         <div className="address">{item.address}</div>         <div className="time">{item.time}</div>         <span>营业中</span>       </div>       <div className="right">         <div className="distance">{item.distance}</div>         <span className="icon1">           <Space wrap style={{ fontSize: 36 }}>             <TravelOutline color="var(--adm-color-danger)" />           </Space>         </span>         <span className="icon2">           <Space wrap style={{ fontSize: 36 }}>             <PhoneFill color="var(--adm-color-danger)" />           </Space>         </span>       </div>     </div>   )); };复制代码
```

页面效果：

### 页面布局

本项目的css部分都采用了styled-components的方式，它是一个常用的 css in js 类库。和所有同类型的类库一样，通过js赋能解决了原生css所不具备的能力，比如变量、循环、函数等。优点有：

-   className 的写法会让原本写css的写法十分难以接受
    
-   如果通过导入css的方式 会导致变量泄露成为全局 需要配置webpack让其模块化
    
-   以及上面提到的解决了原生 css 所不具备的能力，能够加速项目的快速开发 部分代码如下：
    

```
import styled from "styled-components";export const FooterWrapper = styled.div`  width: 100%;  height: 50px;  background: #e9d8d8;  position: fixed;  bottom: 0;  left: 0;  display: flex;  a {    font-weight: 700;    flex: 1;    display: flex;    flex-direction: column;    align-items: center;    justify-content: space-around;    &.active {      color: red;    }    i {      font-size: 2em;    }  }`;复制代码
```

## 项目架构

```
├─ react-ice-City│  │  ├─ index.html│  │  ├─ src│  │  │  ├─ api│  │  │  │  └─ request.js│  │  │  ├─ App.css│  │  │  ├─ App.jsx│  │  │  ├─ assets│  │  │  │  ├─ fonts│  │  │  │  ├─ images│  │  │  │  └─ styles│  │  │  │     └─ reset.css│  │  │  ├─ components│  │  │  │  ├─ Footer│  │  │  │  ├─ Header│  │  │  │  ├─ OrderList│  │  │  │  └─ ShopList│  │  │  ├─ config│  │  │  ├─ index.css│  │  │  ├─ main.jsx│  │  │  └─ pages│  │  │     ├─ Food│  │  │     │  ├─ Nearby│  │  │     │  │  ├─ IceBanner│  │  │     │  ├─ Often│  │  │     │  └─ style.js│  │  │     ├─ Home│  │  │     │  ├─ OrderList│  │  │     │  ├─ SetMeal│  │  │     │  └─ Vip│  │  │     ├─ Mine│  │  │     └─ Order│  │  │        ├─ Back│  │  │        ├─ Conduct│  │  │        ├─ History│  │  └─ vite.config.js复制代码
```

以上就是本项目的架构，基本实现了组件化开发的思想，大组件用来渲染整个页面，小组件用来实现单个功能，达到了一个协调的标准。

## 最后

> 以上就是我设想和封装全部组件的过程，作为一个刚入行的小白，刚开始写的很艰难，但好在写出来了一部分，后面我还会继续完善。希望本篇文章对你有所帮助，如果有写的不会的地方，也欢迎指正。你的点赞是我继续创作的动力。感谢大家！

源码地址：gitee.com/yan-chen092…[2] （gitee.com）

关于本文

作者：严辰

https://juejin.cn/post/7113544665575456804