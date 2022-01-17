SPA： single page web application  （react,vue）单一页面导致首屏加载过慢（使用cdn加速）不能seo

Nuxt.js  (vue)

Next.js ssr(服务端渲染)

优点

1.搭建轻松 

2.自带数据同步

3.丰富插件   自己形成生态

```
//需要全局安装 
npm isntall -g create-next-app

//创建项目

npx create-next-app next-create
```

## 跳转时用query传递和接受参数

```
<Link href="/xiaojiejie?name=苍井空"><a>选苍井空</a></Link>

//另一种形式
Router.push({
      pathname:'/xiaojiejie',
      query:{
        name:'井空'
      }
    })
```

react-next 存在路由钩子函数

routerChangeStart 路由发生变化时

routerChangeComplete 路由结束变化时

beforeHistoryChange 浏览器history触发前

routeChangeError路由跳转发生错误时

hashChangeStart hansChangeComplete

## next利用axios请求远端数据

在`Next.js`框架中**提供了`getInitialProps`静态方法用来获取远端数据**，这个是框架的**约定**，所以你也只能在这个方法里获取远端数据。不要再试图在声明周期里获得，虽然也可以在`ComponentDidMount`中获得，但是用了别人的框架，就要遵守别人的约定。

```js
yarn add axios

import axios from 'axios'

import { withRouter} from 'next/router'
import Link from 'next/link'
import axios from 'axios'

const Xiaojiejie = ({router,list})=>{
    return (
        <>
            <div>{router.query.name},来为我们服务了 .<br/>{list}</div>
            <Link href="/"><a>返回首页</a></Link>
        </>
    )
}

//  获取远端数据
Xiaojiejie.getInitialProps = async ()=>{
    const promise =new Promise((resolve)=>{
            axios('https://www.easy-mock.com/mock/5cfcce489dc7c36bd6da2c99/xiaojiejie/getList').then(
                (res)=>{
                    console.log('远程数据结果：',res)
                    resolve(res.data.data)
                }
            )
    })
    return await promise
}

export default withRouter(Xiaojiejie)
```

## style 编写 jsx

```
import React, {useState} from 'react'

function Jspang(){
    //关键代码----------start-------
    const [color,setColor] = useState('blue')

    const changeColor=()=>{

        setColor(color=='blue'?'red':'blue')
    }
     //关键代码----------end-------

    return (
        <>
            <div>技术胖免费前端教程</div>
            <div><button onClick={changeColor}>改变颜色</button></div>
           <style jsx>
           {`
           		<div>
           		{color:${color}}
           		</div>
           `}
           </style>
        </>
    )
}
export default Jspang
```

## Lazy loading实现模块懒加载

当我们作的应用存在首页打开过慢和某个页面加载过慢时，就可以采用`Lazy Loading`的形式，用懒加载解决这些问题。

## 自定义Head 更友好Seo

为了更好的进行SEO优化，可以自己定制`<Head>`标签

1. 定义header组件完成一个简单hooks组件，引入next/head

   ```
   import Head from 'next/head'
   function Header(){ 
       return (
           <>
               <Head>
                   <title>技术胖是最胖的！</title>
                   <meta charSet='utf-8' />
               </Head>
               <div>JSPang.com</div>
   
           </> 
       )
   }
   export default Header
   ```

   写完如上代码就完成了，在各个组件中引入使用即可



## 使next支持css文件（next 使用antd）

```
// 让next.js 可以加载css文件 
yarn add @zeit/next-css
//建立一个next.config.js(next.js)的总配置文件

const withCss = require('@zeit/next-css')

if(typeof require !== 'undefined'){
    require.extensions['.css']=file=>{}
}

module.exports = withCss({})
```

babel-plugin-import 是一款 babel 插件（按需加载），它会在编译过程中将 import 的写法自动转换为按需引入的方式。

```
//写法  新建.babelrc配置文件。
{
    "presets":["next/babel"],  //Next.js的总配置文件，相当于继承了它本身的所有配置
    "plugins":[     //增加新的插件，这个插件就是让antd可以按需引入，包括CSS
        [
            "import",
            {
                "libraryName":"antd",
                "style":"css"
            }
        ]
    ]

```

