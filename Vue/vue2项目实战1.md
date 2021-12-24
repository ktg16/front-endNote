### 项目实战1

#### Vue 实战 - 仿写漫画岛 H5

### 一、创建项目，并且关联远程仓库

### 二、需求分析与评估

> **业务流程**
>
> 1、产品去收集需求（需求文档）
>
> 2、绘制PRD 讲解需求 需求评审（小版本迭代，一个版本一个月左右）
>
> 3、程序员去消化，然后进行二次需求评审，大的话分几个版本去做。
>
> 4、 技术评审，画一下process on 绘制大体的思维导图
>
> 5、前端、后台、数据库都看一下怎么做，在技术评审的会议上。
>
> 6、UI开始设计 设计完产品过一遍
>
> 7、其他人员开始估算工时
>
> 8、估完工时以后，pmo（管理项目进度）排期工时
>
> 9、立项开始做
>
> 11、测试用例评审 评审测试点（看实际实现和需求是否符合要求） 看测试用例是否符合需求。
>
> 12、测试用例评审完毕以后。
>
> 13、开发完以后，提测，测试进行中，提Bug，改Bug
>
> 14、改完了以后，发测试报告，然后上线。
>
> 15、上线当天测试线上bug，现场改bug。
>
> 16、改完bug，再进行上线，上线15天后，结项。结项完成以后，下个月发项目奖金。根据工时和系数（参与度，职级）

#### 需求分析

页面有哪些

1. 首页各种漫画推荐
2. 分类页面
3. 排行榜页面
4. vip专区
5. 历史页面
6. 收藏页面
7. 个人中心页面
8. 关于页面
9. 反馈页面
10. 登陆和注册
11. 搜索页面
12. 搜索详情页面
13. 列表页面

时间点评估

1. 最终时间：一周时间
2. 现做静态页面  （1天写五个）
3. 实现业务逻辑   （1-2天）
4. 与后段联调

### 三、实现路由

1.建立页面 编写初始化页面

```
<template>
  <div class = 'page-history'>
    <h1>历史页面</h1>
  </div>
</template>

<script>
export default {
  name: 'Favorite'
}
</script>

<style>

</style>
```

2.配置router信息 router/index.js

```
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
import City from '../views/City'
import Classify from '../views/Classify'
import My from '../views/My'
import Ranking from '../views/Ranking'


Vue.use(VueRouter)



const router = new VueRouter({
  routes:[
    { path: '/home', component: Home },
    { path: '/classify', component: Classify},
    { path: '/city', component: City },
    { path: '/my', component: My },
    { path: '/ranking', component: Ranking },
    { path: '/', redirect: '/home' }
    
  ]
})

export default router

```

3.拷入css样式

在assests/style写底层base.scss

```
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
html,
body,
#app{
	// 如果你在这里想使用px单位，不希望转换成rem 
	// 只需要将 px  PX
	max-width: 540PX;
  height: 100%;
  margin: auto;
}
a:active,
a:hover,
a:link,
a:visited {
  outline: none;
  text-decoration: none;
  color: #333;
}
.font-20 {
  font-size: 10px;
}
.font-24 {
  font-size: 12px;
}
.font-26 {
  font-size: 13px;
}
.font-28 {
  font-size: 14px;
}
.font-30 {
  font-size: 15px;
}
.font-32 {
  font-size: 16px;
}
.font-36 {
  font-size: 18px;
}

```

4.首页引入图片 ~@/路径  css样式下

5.自己写  css样式

### 四、实现首页头部

> 没有办法进行rem布局，没有办法进行适配
>
> ```
> 可以使用框架开发
> ```
>
> 

### 五、使用 postcss-pxtorem  来自动将代码中的带px单位的转成对应rem

>  postcss-pxtorem是 postcss 的一个插件

##### postcss 是什么？[是一个用Javascript工具和插件转换css代码的插件](https://www.postcss.com.cn/)

> @vue/cli 脚手架工具在创建vue项目的时候，默认就继承了 postcss 在里面。
>
> 现在使用 postcss 来用上两个插件  postcss-pxtorem autoprefixer
>
> 1. 项目根目录下创建  postcss.config.js 文件
> 2. 下载一些插件
>
> ```bash
> $ npm install  postcss-pxtorem autoprefixer --save-dev 开发者模式下
> ```
>
> -dev 保存在开发模式的配置项中。
>
> 3. 配置 postcss.config.js 中 plugins 选项

```javascript
module.exports = {
    plugins: {
      // 将这个插件进行一个降级操作  ^9.0.0  重新下载该插件
      autoprefixer: {
        // 不需要设置这个选项，它会自动去使用 .browserslistrc 这个文件的配置项
        // browsers: ['Android >= 4.0', 'iOS >= 8'],
        // 这里会有一个小问题 autoprefixer 最近新更新了10.x系列版本，需要降级成9.x系列
      },
      'postcss-pxtorem': {
        // 转换的基准值  1rem = 37.5px
        // x rem = 44px
        rootValue: 37.5,
        propList: ['*']
      }
    }
  }
```

> 4. 重启项目
>
> 5. ```
>    "autoprefixer": "^9.8.6", 需要降级 如何降级 "^9.0.0"降级 重新下载 autoprefixe
>    ```
>
> 
>
> 6.  不能随窗口大小改变而改变     使用一段js代码来给html设置fontSize，并且能够**尺寸发生变化的时候去动态修改html元素的fontSize值。**
>
>    使用 [lib-flexible](https://github.com/amfe/lib-flexible) 阿里的同学携带一套代码。(放在/public/lib/flexible.js)
>
>    ```javascript
>    (function flexible (window, document) {
>      var docEl = document.documentElement
>      var dpr = window.devicePixelRatio || 1
>
>      // adjust body font size
>      function setBodyFontSize () {
>        if (document.body) {
>          document.body.style.fontSize = (12 * dpr) + 'px'
>        }
>        else {
>          document.addEventListener('DOMContentLoaded', setBodyFontSize)
>        }
>      }
>      setBodyFontSize();
>
>      // set 1rem = viewWidth / 10
>      function setRemUnit () {
>        //在这里限制一下最大的宽度 540
>        var clientWidth = docEl.clientWidth;
>        var rem = clientWidth > 540 ? 540 / 10 : clientWidth / 10
>        docEl.style.fontSize = rem + 'px'
>      }
>
>      setRemUnit()
>
>      // reset rem unit on page resize
>      window.addEventListener('resize', setRemUnit)
>      window.addEventListener('pageshow', function (e) {
>        if (e.persisted) {
>          setRemUnit()
>        }
>      })
>
>      // detect 0.5px supports
>      if (dpr >= 2) {
>        var fakeBody = document.createElement('body')
>        var testElement = document.createElement('div')
>        testElement.style.border = '.5px solid transparent'
>        fakeBody.appendChild(testElement)
>        docEl.appendChild(fakeBody)
>        if (testElement.offsetHeight === 1) {
>          docEl.classList.add('hairlines')
>        }
>        docEl.removeChild(fakeBody)
>      }
>    }(window, document))
>    ```
>
> 
>
> 7. 关于 .browserslistrc 文件中的内容，可以参考这里 [这里](https://www.jianshu.com/p/d45a31c50711)



### 七、限制一些首页内容的宽度

不然平铺的话不好看 给两边留点距离

> 修改 /base.scss 中的css样式 

```css
html,
body,
#app{
	// 如果你在这里想使用px单位，不希望转换成rem 
	// 只需要将 px  PX
	max-width: 540PX;  设置rem中最大的宽
  height: 100%;
  margin: auto;
}
```

> 在/public/lib/flexible.js 中做最大的限制

```javascript
  // set 1rem = viewWidth / 10 设置1rem
  function setRemUnit () {
    //在这里限制一下最大的宽度 540 组件节点会随之变化
    var clientWidth = docEl.clientWidth;
    var rem = clientWidth > 540 ? 540 / 10 : clientWidth / 10//设置1rem最大为多少
    docEl.style.fontSize = rem + 'px'
  }
```



### 八、添加swiper插件

1. 下载swiper插件swiper

```bash
$ npm install swiper -D
```

2. 引入核心文件

```javascript
// 引入 Swiper 核心js文件 和  Swiper样式 注意
import Swiper from 'swiper/swiper-bundle.js'
import 'swiper/swiper-bundle.css'
```

3. 在 钩子函数mounted 中实例化就行了

   ```javascript
   mounted () {
       var that = this
       /* eslint-disable */
       new Swiper(this.$refs.swiper, {
         loop: this.loop, //是否进行循环轮播
         autoplay: this.autoplay ? {
           delay: this.autoplay,
           stopOnLastSlide: false,
           disableOnInteraction: true
         } : false,
         pagination: {
           el: ".swiper-pagination"
         },
   ```

   

4. [**设置轮播图样式  修改第三方样式的时候，发现修改不了]**(有问题)，原因是scoped引起的。scoped(局部样式)无法直接覆盖

   > 解决办法：在编写一个style标签，将scoped去掉就行了。

### 九、抽离组件（重点）

使用插槽<slot></slot>   <Swiper></Swiper>上就可以使用组件内的属性了     

```javascript
<Swiper class="my-swiper" v-if="bannerList.length > 0" :autoplay="3000">
        <!-- Swiper里是组件swiper里的全部代码 只不过上面的属性是给swiper的   当组件挂载上来是slot的位置 就是上面一行代码Swiper的位置 放在那里面 -->
        <SwiperItem v-for="item in bannerList" :key="item.id">
          <!-- 因为需要带内容所以使用slot   将Swiperitem组件插入这里 swiperitem上就可以设置属性了 这里面的属性了-->
          <img v-lazy="item.imageurl" alt />
        </SwiperItem>
      </Swiper>
```

在src中新建componts组件文件夹 新建Swiper/Swiper和SwiperItem.vue

Swiper

```
<template>
  <div class="swiper-container" ref = 'swiper'>
    <div class="swiper-wrapper">
      <slot></slot>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
  </div>
</template>

<script>
// 引入 Swiper 核心js文件 和  Swiper样式
import Swiper from 'swiper/swiper-bundle.js'
import 'swiper/swiper-bundle.css'
export default {
  name: 'Swiper',
  // 属性
  props: {
    autoplay: {
      type: Number,
      default: 0
    },
    loop: {
      type: Boolean,
      default: true
    }
  },
  mounted () {
    var that = this
    /* eslint-disable */
    new Swiper(this.$refs.swiper, {
      loop: this.loop, //是否进行循环轮播
     
      pagination: {
        el: ".swiper-pagination"
      },
      on : {
        slideChangeTransitionEnd: function () {
          // console.log(this.activeIndex)
          // console.log(this.realIndex)
          // 触发一个自定义事件
          that.$emit('change', this.realIndex)
        }
      }
    });
    /* eslint-enable */
  }
}
</script>
```



swiperitem

```
<template>
  <div class="swiper-slide">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: 'SwiperItem'
}
</script>
```

在Swiper文件下新建一个index.js用于组件的使用（因为方便引入）

使用Swiper，SwiperItem的解构赋值

```
// 引入抽离出来的 Swiper 插件
import Swiper from './Swiper.vue'
import SwiperItem from './SwiperItem.vue'

// 暴露
/*
  export default {}  => import xxx from ""
  export {} =>   import {} from ''

  如果上述两个都写了
  import xxx, {} from ""
*/
export {
  Swiper,
  SwiperItem
}
```

加上属性自动轮播

```
mounted () {
    var that = this
    /* eslint-disable */
    new Swiper(this.$refs.swiper, {
      loop: this.loop, //是否进行循环轮播
      autoplay: this.autoplay ? {   //判断是否为真 如果未设置写   										false  判断
        delay: this.autoplay,
        stopOnLastSlide: false,
        disableOnInteraction: true
      } : false,
      pagination: {
        el: ".swiper-pagination"
      },
      on : {            //设置了监听事件
        slideChangeTransitionEnd: function () {
          // console.log(this.activeIndex)
          // console.log(this.realIndex)
          // 触发一个自定义事件
          that.$emit('change', this.realIndex)
        }
      }
    });
    /* eslint-enable */
  }
}
```

**实现点击跳转**（有问题）

这里需要子(下标)传入父亲组件  需要使用this.$emit又产生了问题  this指向的问题 解决方案设置一个全局this中间件that用于代替组件swiper this  

重点记住  如果使用箭头函数的话 下面  this.realIndex中的this又不能使用了

```
mounted () {
    var that = this
    /* eslint-disable */
    new Swiper(this.$refs.swiper, {
      loop: this.loop, //是否进行循环轮播
      autoplay: this.autoplay ? {   //判断是否为真 如果未设置写   										false  判断
        delay: this.autoplay,
        stopOnLastSlide: false,
        disableOnInteraction: true
      } : false,
      pagination: {
        el: ".swiper-pagination"
      },
      on : {            //设置了监听事件
        slideChangeTransitionEnd: function () {
          // console.log(this.activeIndex)
          // console.log(this.realIndex)
          // 触发一个自定义事件
          that.$emit('change', this.realIndex)
        }
      }
    });
    /* eslint-enable */
  }
}
```

以上是根据vant组件实现的  我们需要实现一部分东西

### 十、组件复用的问题，Swiper 复用的时候，小圆点不能动了。（bug （重点））

>  问题的原因： new Swiper 使用的是一个css类选择器，当Swiper复用多次的时候，后面的 new Swiper 操作会将之前的实例化过的组件进行覆盖。
>
>  创建了两个同名的class类
>
>  解决办法：
>
>  1. 方案一：new Swiper 不要使用 类选择器，批量选择的选择器不能使用，使用 id 选择器 （不好）给组件  （id是唯一的）
>
>  2. 方案二：使用 ref 标记 （推荐）
>       1. 首先先使用 ref 去标记元素
>       2. 然后通过 this.$refs.xxx 去获取dom元素
>          1. ref 标记的是普通dom元素，那么后续得到的就是这个元素的DOM对象
>          2. ref 标记的是自定义组件，那么后续得到的是这个组件的实例对象。 this.$el
>  3. 方案三：Swiper 组件中 根元素 swiper 容器，所以我们可以通过使用 this.$el 实例属性

### 十一、项目开发中1px的问题

ios无法将1像素压缩成0.5像素

声明混合

引入是@import "~@/assets/styles/mixins.scss";

调用@include border-bottom;

> 声明一个混合 /mixins.scss

```css
@mixin border-bottom {
  position: relative;
  &::after{
    content: '';
    position: absolute;
    width: 100%;
    height: 1px;
    background-color: #e9e9e9;
    left: 0px;
    bottom: 0px;
    transform: scaleY(0.5);
  }
}

//调用
@include border-bottom;
```