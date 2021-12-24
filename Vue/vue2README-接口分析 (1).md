## 1. 去分析人家网站的接口是干什么的

首页轮播图数据：
GET https://mhd.zhuishushenqi.com/comic_v2/getproad?apptype=8&appversion=1.0&channel=web-app&adgroupid=123

首页漫画推荐数据：
GET https://mhd.zhuishushenqi.com/comic_v2/customerview?apptype=8&appversion=1.0&channel=web-app&viewtype=1

## 2. 去请求一下看看是否会跨域

不跨域的好说，直接用就好了。
跨域的如何处理呢？

1. jsonp  缺点，只能进行get请求
2. cors   重写 cors 协议 
3. 代理   (推荐)
4. ....

#### 代理的处理

方案一、自己做一个nodejs的中间层

A - 当前页面地址    http://localhost:8080
B - nodejs中间层   http://localhost:9090
C - 目标地址       http://movie.miguvideo.com
D - 目标地址的某个接口地址 http://movie.miguvideo.com/lovev/miguMovie/data/seeFilmData.jsp

方案二、配置 Vue 脚手架的配置文件

Vue 脚手架创建的项目，在本地开发时（npm run serve）时，启动的服务就是一个node实现的。
Vue 脚手架创建的项目，有一个配置文件叫做 vue.config.js
在这个配置文件中可以做很多的配置，其中就有代理的配置。

1. 项目根目录下创建一个 vue.config.js
2. 配置 vue.config.js 中 devServer.proxy 配置。这里的配置与方案一种的配置项是一样的
3. 重新运行项目
4. A 与 B 是同一个主机。这里就是 http://localhost:8080



## 3. 具体的实现

### 方案一：自己做一个nodejs的中间层

1. 安装nodejs插件

>  文档说明  [cors](https://www.npmjs.com/package/cors)  [http-proxy-middleware](https://www.npmjs.com/package/http-proxy-middleware)

```bash
$ npm install http-proxy-middleware -D
$ npm install express -D
$ npm install cors -D
```

2. server.js

```javascript
const express = require("express");
const { createProxyMiddleware } = require("http-proxy-middleware");
const cors = require("cors");
const app = express();

//处理一下跨源
app.use(cors())

// 目标地址 C 是: https://api.asilu.com/today/
// 这是我们可以访问 B 是：http://localhost:9090/today/

// A 发起请求 http://localhost:9090/migu/today/

//提供代理，处理跨源的数据
app.use('/migu', createProxyMiddleware({
  // 目标地址，只写主机
  target: 'https://api.asilu.com',
  changeOrigin: true,
  pathRewrite: {
    '^/migu': ''
  }
}))

app.get('/', (req, res) => {
  res.send("hello world")
})


app.listen(9090, () => {
  console.log("服务器启动成功");
})

//运行这个程序 npm run start  或者 npm start
//supervisor server.js
```

##### 测试用例

```javascript
// 使用fetch
//fetch('https://mhd.zhuishushenqi.com/comic_v2/getproad?apptype=8&appversion=1.0&channel=web-app&adgroupid=123')
    //   .then(res => res.json())
    //   .then(res => {
    //     console.log(res)
    //   })
是否能下载到数据 Access-Control-Allow-Origin：*
    后台允许跨域请求
    // https://api.asilu.com/today/

    // 直接请求是跨域的
    // fetch('https://api.asilu.com/today/')
    //   .then(res => res.json())
    //   .then(res => {
    //     console.log(res)
    //   })

    // fetch('http://localhost:8080/migu/today/')
    //   .then(res => res.json())
    //   .then(res => {
    //     console.log(res)
    //   })
    fetch('/migu/today/')
      .then(res => res.json())
      .then(res => {
        console.log(res)
      })
```



### 方案二：直接通过配置 vue 脚手架 工具 实现代理

> Vue 脚手架创建的项目，在本地开发的时候 (npm run serve) 时，启动的服务器就是一个node实现的服务器。
>
> Vue 脚手架创建的项目，有一个配置叫做 vue.config.js
>
> 这个配置文件可以去做很多配置 [配置](https://cli.vuejs.org/zh/config/#%E5%85%A8%E5%B1%80-cli-%E9%85%8D%E7%BD%AE)，其中就我们反向代理的配置。

具体的配置操作

1. 项目的根目录下 创建 vue.config.js

2. 配置 vue.config.js 中 devServer.proxy 配置项，这里的配置与方案一的配置项是一致的。

   ```javascript
   module.exports = {
     devServer: {
       proxy: {
         '/migu': { // 前缀自己写 遇到目标值就代替  
           target: 'https://api.asilu.com',
           changeOrigin: true,
           pathRewrite: {
             '^/migu': '' 
           }
         },
         '/api': { // 前缀自己写
           target: 'https://mhd.zhuishushenqi.com',
           changeOrigin: true,
           pathRewrite: {
             '^/api': ''
           }
         },
         '/maizuo': {
           target: 'https://m.maizuo.com',
           changeOrigin: true,//是否改变请求头中的host
           pathRewrite: {
             '^/maizuo': ''
           }
         }
       }
   
     }
   }
   
   ```

   

3. 重新运行项目

4. A 和 B 是同一个主机  这个主机都是 localhost:8080

## 4. 接口统一处理

1. 确定网络请求工具选择是什么？

> axios

2. 安装axios

```bash
$ npm install axios
```

3. 对axios 做一个二次的封装

   ```javascript
   const instance = axios.create({
   
     // options    baseurl方便你后期上线的时候，更改主机名
     // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
     baseURL: process.env.NODE_ENV === 'production' ? 'http://localhost:8080' : 'http://154.8.228.120/',
     // 设置超时时间
     timeout: 15000
   
   })
   // 添加请求拦截器
   
   instance.interceptors.request.use(function (config) {
     // 在发送请求之前做些什么
     return config
   }, function (error) {
     // 对请求错误做些什么
     return Promise.reject(error)
   })
   
   instance.interceptors.response.use(function (response) {
     // 对响应数据做点什么
     return response.data
     // 返回请求         返回 .data
   }, function (error) {
     // 对响应错误做点什么
     // 在调用.catch 之前，先需要经过这里
     Notify({ message: '网络异常，请稍后重试', duration: 1500 })
     return Promise.reject(error)
   })
   
   export default instance
   
   ```

   

4. 通过封装的函数进行数据请求

5. 新建api/cartoon处理漫画数据的接口 （获取数据需要获得相关接口）

6. 将请求的到的数据挂载到data 中的数据  bannerList 数组中

```javascript
import request from '../utils/request'
import { format } from '@/utils/apiHelp'
/**
 * 获取轮播图数据
 * 数据源  https://mhd.zhuishushenqi.com/comic_v2/getproad?apptype=8&appversion=1.0&channel=web-app&adgroupid=123
 */
export const getBanner = () => {
  return request({
    url: '/api/comic_v2/getproad',
    params: { // 参数拼接参数
      apptype: 8,
      appversion: 1.0,
      channel: 'web-app',
      adgroupid: 123
    }
  })
}

/**
 * 获取首页推荐的数据
 * https://mhd.zhuishushenqi.com/comic_v2/customerview?apptype=8&appversion=1.0&channel=web-app&viewtype=1
*/

export const getIndexRecomment = () => {
  return request({
    url: '/api/comic_v2/customerview',
    params: { // 参数拼接参数
      apptype: 8,
      appversion: 1.0,
      channel: 'web-app',
      viewtype: 1
    }
  })
}
```

之前使用this.$nextTick()  重点

> 对于swiper组件，由于数据是异步下载的，**又出现bug**   我们可以在swiper组件上添加一个 v-if = "bannerList.length > 0" 有数据才会去加载

```vue
<Swiper class = 'my-swiper' v-if = "bannerList.length > 0" :autoplay = "3000">
  <SwiperItem v-for = "item in bannerList" :key = "item.id">
    <img
      :src="item.imageurl"
      alt
    />
  </SwiperItem>
</Swiper>
```

## 五、设置iconfont图标

1. 先去阿里矢量库选择要用的图片，点击下载
2. 将下载到的图标库，拷贝到 public/目录下 
3. 在 index.html 引入 图标的 css 文件路径
4. 给 .index-nav 添加下边框下

## 六、实现首页推荐商品

> 这里发现滚动图顶上去了

滚动窗口



这里我们需要设置一个局部的滚动

1. 将整体页面上需要滚动的部分  单独放在一个 class = index-main 的div 标签中

2. 然后设置样式 垂直滚动 

   flex：1代表什么

```css
  .index-main {
    flex: 1;
    overflow-y: auto;
  }
```

六 1 继续下载数据

```
/**
 * 获取首页推荐的数据
 * https://mhd.zhuishushenqi.com/comic_v2/customerview?apptype=8&appversion=1.0&channel=web-app&viewtype=1
*/

export const getIndexRecomment = () => {
  return request({
    url: '/api/comic_v2/customerview',
    params: { // 参数拼接参数
      apptype: 8,
      appversion: 1.0,
      channel: 'web-app',
      viewtype: 1
    }
  })
}
```

下载数据

```
getIndexRecomment () {
      getIndexRecomment().then(res => {
        if (res.code === 200) {
          this.recommentList = res.info
        } else {
        // 不ok，就在页面上报错
        // 在这里我们先通过 alert 进行报错，后期 我们可以用一下 vant 组件库的组件
          alert(res.code_msg)
        }
      }
      )
        .catch(err => {
          alert('网络异常，请稍后：' + err)
        })
    }

  },
```

需要数据时  考虑哪些

1.数据放在哪些地方    data？ props？ computed？ state？ getter？

2.数据格式？string array object....



根据页面样式  自定义下载数据  很简单

###   七、自定义过滤器

1. 全局注册 

   全局注册过滤器组件可以在main里写  也可以单独写一个组件在main中引入

   最后一个过滤的参数，是靠近左边的返回值

   局部注册过滤器  多出一个filters配置项

   svn

   v-gotop指令两个知识点 自定义指令 .dispatch  vue.extend 继承组件

   有没有封装组件  封装组件流程

```javascript
Vue.filter('formatYi', (value) => {
  var Yi = Math.pow(10, 8)
  if (value > Yi) {
    return `${(value / Yi).toFixed(2)}亿`
  } else {
    return `${(value / Math.pow(10, 4)).toFixed(2)}万`
  }
})
```

> 调用

```html
 <span class="hot-hot">{{ childItem.bigbookview | formatYi }}</span>
```

全局方法

2. 局部注册

```javascript
  filters: {
    formatYi (value) {
      var Yi = Math.pow(10, 8)
      if (value > Yi) {
        return `${(value / Yi).toFixed(2)}亿`
      } else {
        return `${(value / Math.pow(10, 4)).toFixed(2)}万`
      }
    }
```



























