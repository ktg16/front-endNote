# uni-app

**Objct.key(obj)得到的值是[key,key] 可以用来判断值是否存在**

arr.length !==0

请求接口可以使用 页面中在 onReady()中调用

Promise.all({

this._comingSoon()

this._newMovies()

}).then(res=>{

console.log(res)//打印出的res为几个数据组成的数组

})





navigationBarTitleText    tabbar的标题

globalStyle 首页默认的样式

pages.json 控制路由 谁放在第一个谁先显示

App.js 用来配置全局样式   监听应用的生命周期

**加新页面是需要重启下**

### App.js

onLaunch

uni.scss 全局通用scss样式库   不需要引入

pages 添加路由  配置页面

components 组件 使用方法与vue一样 

#### 兄弟组件的通信

```
也可以这样写：
组件中uni.$emit()

全局事件订阅

onLoad(){

//$once 只能调用一次

uni.$on('testEmit',(rel)=>{})

}页面初始化的时候
```

分页

在微信小程序里不能使用indexOf   

二元运算符 {{false||“”||"123"}}

uniapp中只有<view> 没有<div>

##### **生命周期**

https://uniapp.dcloud.io/collocation/frame/lifecycle?id=%e5%ba%94%e7%94%a8%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f

onPullDownRefresh

1.需要在 `pages.json` 里，找到的当前页面的pages节点，并在 `style` 选项中开启 `enablePullDownRefresh`

也可以在globalStyle(全局的)开启enablePullDownRefresh

2.当处理完数据刷新后，`uni.stopPullDownRefresh` 可以停止当前页面的下拉刷新

onShareAppMessage 用户点击分享

onPageScroll 监听页面滚动

#### 路由与页面跳转

https://uniapp.dcloud.io/api/router?id=navigateto

当跳转的页面是tabbar中的页面时需要用  

**uni.switchTab**({

url:""})

路由跳转时tabbar页面比较特殊

***uni.navigateTo*** 使用其会保留老页面打开一个新的页面  打开多次就无法再次打开了  因为路由中缓存被占满了

多次打开的使用**uni.redirectTo**  redirect重定向 不会保留老页面

当需要获取路由传参是使用onLoad(option){

console.log(option)

}

#### 常用组件

直接使用就可

点击左侧  右侧列表滑到指定位置

scroll-view 滑动视图

:scroll-into-view ="clickid" 绑定一个空字符串

标题绑定字符串  :id="'po'+index"

在列表头绑定方法 setId(index){

this.clickId = 'po'+index

}	点击时滑动到 与vant card一样

uni-app字体大小适配使用upx

双联动

操作dom

@scroll 滚动事件 

scroll(e){

e.target.scrollTop

}

当最后一个标题达不到要求的top使用如下

@scrolltolower=“ ” 滚动到底部事件

当与@scroll会出现bug 可以使用setTimeout 让@scroll先执行

#### ajax使用

https://uniapp.dcloud.io/api/request/request?id=request

#### uniapp-ui

https://uniapp.dcloud.io/component/README?id=uniui

Vuex

vuex使用方法

https://uniapp.dcloud.io/vue-vuex?id=state 

调用mutations全局同步方法   this.$store.commit("xxx")

调用actions  this.$store.dispach

getters 为vue中的computed

在onReady中调用初始化接口

uni-app项目 

1.写静态页面

2.调用百度地图接口获取到当前位置信息

3.写接口

使用uni.request



#### 条件编译

布局是出现差异

//#ifdef MP-AlIPAY

xxxxx

//#endif

uni-app（h5端需要）配置跨域代理

https://www.bilibili.com/video/BV17z4y1D7Yj?p=971

![eeae19905f43753fd9c31bd641f3be2](C:\Users\ADMINI~1\AppData\Local\Temp\WeChat Files\eeae19905f43753fd9c31bd641f3be2.png)