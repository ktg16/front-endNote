https://yiming_chang.gitee.io/pure-admin-doc/pages/routerMenu/#%E5%A6%82%E4%BD%95%E7%94%9F%E6%88%90%E4%B8%80%E7%BA%A7%E8%8F%9C%E5%8D%95

“一个人能做到什么，并不完全取决于血统，而是他想做到什么。我认为你不行，不是说血统或者能力，而是你没有目标，”楚子航说，“没有什么目标能让你豁出去、用尽全力，豁不出去的人是没有用的，就算你的血统比我们都强。

本文档目的为了学习vue3+Ts的项目实战及脚手架进阶

为了大型项目做基础 小东西已经满足不了个人的胃口了

完整目录结构

```javascript
├── .github  # GitHub 配置文件
│   ├── ISSUE_TEMPLATE  # 问题提交参考模板
│   ├── workflows git  # 工作流
├── .husky  # 代码提交前校验配置文件
├── .vscode  # IDE 工具推荐配置文件
│   │   ├── extensions.json  # 一键安装平台推荐的 vscode 插件
│   │   ├── settings.json  # 设置扩展程序或 vscode 编辑器的一些属性
│   │   ├── vue3.0.code-snippets  # vue3.0 代码片段
│   │   └── vue3.2.code-snippets  # vue3.2 代码片段
├── build  # 构建工具
│   │   ├── cdn.ts  # 打包时采用 cdn 模式
│   │   ├── compress.ts  # 打包时启用 gzip 压缩或 brotli 压缩
│   │   ├── index.ts  # 导出环境变量、跨域代理函数
│   │   ├── info.ts  # 输出打包信息（大小、用时）
│   │   ├── optimize.ts  # vite 依赖预构建配置项
│   │   ├── plugins.ts  # vite 相关插件存放处
├── locales  # 国际化文件存放处
│   │   ├── en.yaml  # 英文配置
│   │   ├── zh-CN.yaml  # 中文配置
├── mock  # mock 模拟后台数据
│   │   ├── asyncRoutes.ts  # 模拟后台返回动态路由
│   │   ├── ...
├── node_modules  # 模块依赖
├── public  # 静态资源
│   │   ├── html  # 静态 iframe 页面
│   │   ├── favicon.ico  # favicon
│   │   ├── serverConfig.json  # 全局配置文件（打包后修改也可生效）
├── src
│   ├── api  # 接口请求统一管理
│   ├── assets  # 字体、图片等静态资源
│   ├── components  # 自定义通用组件
│   │   ├── ReAuth  # 按钮级别权限管理组件
│   │   ├── ReBarcode  # 条形码组件
│   │   ├── ReCountTo  # 数字动画组件
│   │   ├── ReCropper  # 图片裁剪组件
│   │   ├── ReFlicker  # 圆点、方形闪烁动画组件
│   │   ├── ReFlop  # 时间翻牌组件
│   │   ├── ReFlowChart  # LogicFlow 流程图组件
│   │   ├── ReIcon  # 图标组件
│   │   ├── ReImageVerify  # 图形验证码组件
│   │   ├── ReMap  # 高德地图组件
│   │   ├── ReQrcode  # 二维码组件
│   │   ├── ReSeamlessScroll  # 无缝滚动组件
│   │   ├── ReSelector  # 选择器组件
│   │   ├── ReSplitPane  # 切割面板组件
│   │   ├── ReTreeLine  # 树形连接线组件（基于element-plus）
│   │   ├── ReTypeit  # 打字机效果组件
│   ├── config  # 获取平台动态全局配置
│   ├── directives  # 自定义指令
│   │   ├── auth  # 按钮级别权限指令
│   │   ├── elResizeDetector  # 监听容器改变指令
│   ├── layout  # 主要页面布局
│   ├── plugins  # 处理一些库或插件，导出更方便的 api
│   ├── router  # 路由配置
│   ├── store  # pinia 状态管理
│   ├── style  # 全局样式
│   │   ├── dark.scss  # 暗黑模式样式适配文件
│   │   ├── element-plus.scss  # 全局覆盖 element-plus 样式文件
│   │   ├── reset.scss  # 全局重置样式文件
│   │   ├── sidebar.scss  # layout 布局样式文件
│   │   ├── tailwind.css  # tailwindcss 自定义样式配置文件
│   │   ├── ...
│   ├── utils  # 全局工具方法
│   │   ├── http  # 封装 axios 文件
│   │   ├── progress  # 封装 nprogress
│   │   └── auth.ts  # 处理用户信息和 token 相关
│   │   └── chinaArea.ts  # 汉字转区域码
│   │   └── globalPolyfills.ts  # 解决项目可能因为安装某个依赖出现 `global is not defined` 报错
│   │   └── message.ts  # 消息提示函数
│   │   ├── mitt.ts  # 触发公共事件，类似 EventBus
│   │   ├── print.ts  # 打印函数
│   │   ├── propTypes.ts  # 二次封装 vue 的 propTypes
│   │   ├── responsive.ts  # 全局响应式 storage 配置
│   │   ├── sso.ts  # 前端单点登录逻辑处理
│   │   ├── tree.ts  # 树结构相关处理函数
│   ├── views  # 存放编写业务代码页面
│   ├── App.vue  # 入口页面
│   ├── main.ts  # 入口文件
│   └── mockProdServer.ts  # mock 服务相关
├── types  # 全局 TS 类型配置
│   │   ├── global.d.ts  # 全局类型声明文件
│   │   ├── index.d.ts  # 全局类型声明文件
│   │   ├── index.ts  # 全局类型声明文件
│   │   ├── shims-tsx.d.ts  # 该文件是为了给 .tsx 文件提供类型支持，在编写时能正确识别语法
│   │   └── shims-vue.d.ts  # .vue、.scss 文件不是常规的文件类型，typescript 无法识别，所以我们需要通过下图的代码告诉 typescript 这些文件的类型，防止类型报错
├── .editorconfig  # 编辑器读取文件格式及样式定义配置 https://editorconfig.org/
├── .env  # 全局环境变量配置（当 .env 文件与 .env.development、.env.production、.env.staging 这三个文件之一存在相同的配置 key 时，.env 优先级更低）
├── .env.development  # 开发环境变量配置
├── .env.production  # 生产环境变量配置
├── .env.staging  # 预发布环境变量配置
├── .eslintignore  # eslint 语法检查忽略文件
├── .eslintrc.js  # eslint 语法检查配置
├── .gitignore  # git 提交忽略文件
├── .gitpod.yml  # gitpod 部署配置
├── .markdownlint.json  # markdown 格式检查配置
├── .npmrc  # npm 配置文件
├── .prettierrc.js  # prettier 插件配置
├── .stylelintignore  # stylelint 插件检查忽略文件
├── CHANGELOG.en_US.md  # 版本更新日志（英文版）
├── CHANGELOG.md  # 版本更新日志（英文版）
├── CHANGELOG.zh_CN.md  # 版本更新日志（中文版）
├── commitlint.config.js  # git 提交前检查配置
├── index.html  # html 主入口
├── LICENSE  # 证书
├── package.json  # 依赖包管理以及命令配置
├── pnpm-lock.yaml  # 依赖包版本锁定文件
├── postcss.config.js  # postcss 插件配置
├── README.en-US.md  # README（英文版）
├── README.md  # README
├── stylelint.config.js  # stylelint 配置
├── tailwind.config.js  # tailwindcss 配置
├── tsconfig.json  # typescript 配置
└── vite.config.ts  # vite 配置
```

## 1.插件

#### unplugin-vue-define-options

显示name属性

```
<script setup lang="ts">
defineOptions({
  name: "MyComponent"  
})
<script>
```

https://vue-macros.sxzz.moe/macros/define-options.html

## 2.vue的使用

### 全局注册组件

1.新建一个test.vue组件

<template>    
    <div> 
    一个测试组件    
    </div>
</template> 
<script>    
export default {     } 
</script> 
2.统一目录下建立index.js 使用install方法来全局注册组件（写vue插件的时候也需要这个）

```
export const withInstall = <T>(component: T) => {
  //通过断言的方式确定传递过来的准确值  可以不用
  const comp = component as any;
  comp.install = (app: App) => {
    app.component(comp.name, component);
  };
  return component as T & Plugin;//哪个存在返回哪个
};
vue插件都需要这种方式来注册
```

### emit的使用

```javascript
子组件调用: emit('update:prop',newValue)
父组件使用 <div v-model:prop='newValue'></div>
```

### 创建虚拟 DOM 节点 (vnode)，创建自定义指令（Motion）

#### (1) defineComponent()

第一个参数是一个组件选项对象。返回值将是该选项对象本身，**因为该函数实际上在运行时没有任何操作，仅用于提供类型推导。**

目的是为了配合Ts使用

#### (2) render 编程式地创建虚拟dom

```
//使用方式
render(){
	return VNodeChild
}
render() {
    const { delay } = this;
    const motion = resolveDirective("motion"); 解析一个directive
    return withDirectives( //用于给vnode添加自定义指令
      // 创建虚拟dom
      h(
        "div",
        {},
        {
          default: () => [this.$slots.default()]
        }
      ),
      [
        [
          motion,
          {
            initial: { opacity: 0, y: 100 },
            enter: {
              opacity: 1,
              y: 0,
              transition: {
                delay
              }
            }
          }
        ]
      ]
    );
  }
});
```

#### (3) h()

创建虚拟DOM节点（vnode）

```
function h(
  type: string | Component,
  props?: object | null,
  children?: Children | Slot | Slots
): VNode

// 省略 props
function h(type: string | Component, children?: Children | Slot): VNode
function h(
  type: string | Component,
  props?: object | null,
  children?: Children | Slot | Slots
): VNode

// 省略 props
function h(type: string | Component, children?: Children | Slot): VNode

type Children = string | number | boolean | VNode | null | Children[]

type Slot = () => Children

type Slots = { [name: string]: Slot }
```



#### (4)withDirectives()添加指令

用于给vnode添加自定义指令

```
function withDirectives(
  vnode: VNode,
  directives: DirectiveArguments
): VNode

directives:[[directive, value, arg, modifiers],[...]]
			value:		例如：v-my-directive="1 + 1" 中，绑定值为 2。
			arg:		例如 v-my-directive:foo 中，参数为 "foo"。
			modifiers:	例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }
```

#### (5)resolveDirectives() 解析指令

只能在render或setup函数中使用。

如果在当前应用实例中可用,则允许通过其名称解析一个directive。

返回一个Directive,

### 普通添加自定义指令



## 3.遇见不熟悉的点

### vw/vh

vw/vh  相对视图的宽高  1vw=1%

一般情况下，如果我们仅使用px或rem、em时，会在窗口缩放时，有一些卡顿等小瑕疵影响体验，所以如果可以用rem和vw配合使用，就会使页面布局更为优化，改善使用体验感。

### grid布局

#### 块级容器

1、display：grid；

2、使用 `grid-template-columns` 规则可划分列数，使用 `grid-template-rows` 划分行数。

- 固定宽度（具体像素）当容器宽度过大时将漏白。
- 百分比自动适就容器。
- 使用 `repeat` 统一设置值，第一个参数为重复数量，第二个参数是重复值。
- 自动填充,根据容器尺寸，自动设置元素尺寸。

- - `grid-template-columns：repeat(auto-fill,100px);`

- 使用 `fr` 单位设置元素在空间中所占的比例。

- - `grid-template-columns：1fr 2fr;``//1:2`
  - `grid-template-columns：repeat(2,1fr 2fr);//1:2:1:2`

- 组合定义

- - `grid-template：1fr 2fr;`

- minmax方法可以设置取值范围

#### 间距

1、使用 `row-gap` 设置行间距。

2、使用 `column-gap` 定义列间距。

3、`gap： 20px 10px;` // 行  列

　　行列间距相等则致谢一个值；

#### 元素定位

1、根据容器已经画好的行列来摆放

- `grid-row-start`：上边框所在的水平网格线
- `grid-row-end`：下边框所在的水平网格线
- `grid-column-start`：左边框所在的垂直网格线
- `grid-column-end`：右边框所在的垂直网格线

2、简写

- `grid-row:2/4;`//从第二行开始到第四行结束
- `grid-column:2/4;`

3、根据偏移量

使用 `span` 可以设置移动单元格数量，数值只能为正数。

//假设容器三行三列，则示例中元素处于中间

- `grid-row-start: 2;`
- `grid-column-start: 2;`
- `grid-row-end: span 1;`
- `grid-column-end: span 1;`

4、grid-area

```
grid-row-start/grid-column-start/grid-row-end/grid-column-end
```

#### 对齐

设置给容器

1、控制整行/列元素在栅格里的对齐

- justify-items  水平方向
- align-items  垂直方向
- place-items：align-items  justify-items；

　　可选值：

- - start：对其单元格的起始边缘
  - end：对齐单元格的结束边缘
  - center：单元格内居中
  - stretch：占满整个单元格

　　示例：

`justify-items：start；`//每一横行的元素都紧贴着单元格的左侧

2、整个内容区在容器里的位置

- justify-content  水平方向
- align-content  垂直方向
- place-content：align-content  justify-content；

　　可选值：

　　合在一起移动：

- - start
  - end
  - center
  - stretch

　　两侧有间距：

- - space-around
  - space-between：紧贴容器壁
  - space-evenly：等分

**设置给子元素**

3、单个元素在单元格内的位置

- justify-self  水平方向
- align-self  垂直方向
- place-self ：align-self  justify-self ；

　　可选值：

- - start：对其单元格的起始边缘
  - end：对齐单元格的结束边缘
  - center：单元格内居中
  - stretch：占满整个单元格

## 4.验证码的实现

1.安装

```JavaScript
import { ref, onMounted } from "vue";

/**
 * 绘制图形验证码
 * @param width - 图形宽度
 * @param height - 图形高度
 */
export const useImageVerify = (width = 120, height = 40) => {
  const domRef = ref<HTMLCanvasElement>();
  const imgCode = ref("");

  function setImgCode(code: string) {
    imgCode.value = code;
  }

  function getImgCode() {
    if (!domRef.value) return;
    imgCode.value = draw(domRef.value, width, height);
  }

  onMounted(() => {
    getImgCode();
  });

  return {
    domRef,
    imgCode,
    setImgCode,
    getImgCode
  };
};

function randomNum(min: number, max: number) {
  const num = Math.floor(Math.random() * (max - min) + min);
  return num;
}

function randomColor(min: number, max: number) {
  const r = randomNum(min, max);
  const g = randomNum(min, max);
  const b = randomNum(min, max);
  return `rgb(${r},${g},${b})`;
}

function draw(dom: HTMLCanvasElement, width: number, height: number) {
  let imgCode = "";

  const NUMBER_STRING = "0123456789";

  const ctx = dom.getContext("2d");
  if (!ctx) return imgCode;

  ctx.fillStyle = randomColor(180, 230);
  ctx.fillRect(0, 0, width, height);
  for (let i = 0; i < 4; i += 1) {
    const text = NUMBER_STRING[randomNum(0, NUMBER_STRING.length)];
    imgCode += text;
    const fontSize = randomNum(18, 41);
    const deg = randomNum(-30, 30);
    ctx.font = `${fontSize}px Simhei`;
    ctx.textBaseline = "top";
    ctx.fillStyle = randomColor(80, 150);
    ctx.save();
    ctx.translate(30 * i + 15, 15);
    ctx.rotate((deg * Math.PI) / 180);
    ctx.fillText(text, -15 + 5, -15);
    ctx.restore();
  }
  for (let i = 0; i < 5; i += 1) {
    ctx.beginPath();
    ctx.moveTo(randomNum(0, width), randomNum(0, height));
    ctx.lineTo(randomNum(0, width), randomNum(0, height));
    ctx.strokeStyle = randomColor(180, 230);
    ctx.closePath();
    ctx.stroke();
  }
  for (let i = 0; i < 41; i += 1) {
    ctx.beginPath();
    ctx.arc(randomNum(0, width), randomNum(0, height), 1, 0, 2 * Math.PI);
    ctx.closePath();
    ctx.fillStyle = randomColor(150, 200);
    ctx.fill();
  }
  return imgCode;
}
```

## 5.什么是单点登录？如何实现

## 6.路由实现

今天的任务：https://blog.csdn.net/m0_37410739/article/details/124516414

https://blog.csdn.net/qq_42238554/article/details/86161970

### (1)创建路由

hash与history的区别：写文章

npm run dev执行了什么 https://blog.csdn.net/web2022050901/article/details/125165316

```
createRouter({
  history: getHistoryMode(),    //获取历史方法
  routes: constantRoutes.concat(...remainingRouter), // 创建路由
  strict: true,//
  scrollBehavior(to, from, savedPosition) {//在页面之间导航时控制滚动的函数。可以返回一个 Promise 来延迟滚动
```

https://router.vuejs.org/zh/guide/essentials/history-mode.html  不同的历史模型  

### (2)vite环境配置

Vite 在一个特殊的 import.meta.env 对象上暴露环境变量

package.json里面的scripts的修改  增加多个环境模式

```
"scripts": {
    "dev": "vite serve --mode development",
    "test": "vite serve --mode test",
    "ppe": "vite serve --mode ppe",
    "prod": "vite serve --mode production",
    "build:dev": "vue-tsc --noEmit && vite build --mode development",
    "build:test": "vue-tsc --noEmit && vite build --mode test",
    "build:ppe": "vue-tsc --noEmit && vite build --mode ppe",
    "build:prod": "vue-tsc --noEmit && vite build --mode production",
    "serve": "vite preview"
  }
```

在项目目录添加环境变量文件

.env.development

```cobol
# 开发环境变量
VITE_APP_TITLE=记账簿development
```

.env.test

```cobol
# 质控环境变量
VITE_APP_TITLE=记账簿test
```

.env.production

```cobol
# 生产环境变量
      
VITE_APP_TITLE=记账簿
```

在vue中使用 vite_APP_TITle

```
console.log('VITE_APP_TITLE:' + import.meta.env.VITE_APP_TITLE);
```

### (3)判断路由模式

```
// 获取路由历史模式 https://next.router.vuejs.org/zh/guide/essentials/history-mode.html
function getHistoryMode(): RouterHistory {
  const routerHistory = loadEnv().VITE_ROUTER_HISTORY;
  // len为1 代表只有历史模式 为2 代表历史模式中存在base参数 https://next.router.vuejs.org/zh/api/#%E5%8F%82%E6%95%B0-1
  const historyMode = routerHistory.split(",");//截取变成数组
  const leftMode = historyMode[0];//base指存在某个文件夹下

  const rightMode = historyMode[1];
  console.log(routerHistory, historyMode, leftMode, rightMode, 'router')

  // no param
  if (historyMode.length === 1) {
    if (leftMode === "hash") {
      return createWebHashHistory("");
    } else if (leftMode === "h5") {
      return createWebHistory("");
    }
  } //has param
  else if (historyMode.length === 2) {
    if (leftMode === "hash") {
      return createWebHashHistory(rightMode);
    } else if (leftMode === "h5") {
      return createWebHistory(rightMode);
    }
  }
}

```

### (4)保存滚动位置

https://router.vuejs.org/zh/guide/advanced/scroll-behavior.html

```
  scrollBehavior(to, from, savedPosition) {//在页面之间导航时控制滚动的函数。可以返回一个 Promise 来延迟滚动
    return new Promise(resolve => {
      if (savedPosition) {
        return savedPosition;//期望滚动的位置
      } else {
        if (from.meta.saveSrollTop) {
          const top: number =
            document.documentElement.scrollTop || document.body.scrollTop;
          resolve({ left: 0, top });
        }
      }
    });
  }
```

### (5)进入路由之前所做的操作  beforeEach

```JavaScript
router.beforeEach((to: toRouteType, _from, next) => {
//1.关于keepAlive的操作 配合Pinan把keepAlive路由管理并保存起来   让你跳转时还在统一高度
if (to.meta?.keepAlive) {
    const newMatched = to.matched;
    handleAliveRoute(newMatched, "add");
    // 页面整体刷新和点击标签页刷新
    if (_from.name === undefined || _from.name === "Redirect") {
      handleAliveRoute(newMatched);
    }
  }
<keep-alive
    v-if="keepAlive"
    :include="usePermissionStoreHook().cachePageList"
 >
   <component
   :key="route.fullPath"
   class="main-content"
   />
</keep-alive>
                  
//2.判断外部链接                  
//3.依据用户信息存取    路由权限     
//4.刷新时  会重新获取动态路由                  
```

## 7.Pinia的使用

https://pinia.web3doc.top/core-concepts/state.html

与之前的vuex类似基本无差别

尝试写文章

## 8.实现贪吃蛇

1.地图渲染

2.蛇 食物

3.动画

## 9.组件

1)、高德地图、echart地图

实现echart地图需要map/qd-north-district.json（省市区县乡镇三级或四级城市数据https://github.com/xiangyuecn/AreaCity-JsSpider-StatsGov）

高德地图（参考文档即可完成https://console.amap.com/dev/key/app）

随机模拟了计程车的数据

(我可以模拟各个街道或者小区监控人数或者签约人数)

2)、视频

西瓜视频组件 (https://v2.h5player.bytedance.com/gettingStarted/#%E5%AE%89%E8%A3%85)