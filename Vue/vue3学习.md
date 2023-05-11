### vue3学习

#### 不使用构建工具直接在html中引入

https://staging-cn.vuejs.org/guide/quick-start.html#without-build-tools

```vue
<script src="https://unpkg.com/vue@3"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```



#### defineComponent

```typescript
// 在ts中写法  
//原本写法
import { Slots } from 'vue'

// 声明 props 和 return 的数据类型
interface Data {
  [key: string]: unknown
}

// 声明 context 的类型
interface SetupContext {
  attrs: Data
  slots: Slots
  emit: (event: string, ...args: unknown[]) => void
}

// 使用的时候入参要加上声明， return 也要加上声明
export default {
  setup(props: Data, context: SetupContext): Data {
    // ...

    return {
      // ...
    }
  },
}

import { defineComponent } from 'vue'

export default defineComponent({
  setup(props, context) {
    // 业务代码写这里...

    return {
      // 需要给 template 用的数据、函数放这里 return 出去...
    }
  },
})
```

下午任务  

1.缓存高度位置 keep-live

2.管理store

3. 动画 transition

vue-cli创建vue项目

```
$ vue create my-project
```

Vite 需要 [Node.js](https://nodejs.org/en/) 版本 >= 12.0.0。

单纯创建vite

```
yarn create @vitejs/app
npm init @vitejs/app
```

基于vite创建vue3

```
npm init @vitejs/app my-vue-app -- --template vue
yarn create @vitejs/app my-vue-app --template vue
```

ref可以吧基本数据结构包装成响应式

***//vue2 新增数据 新增功能业务逻辑  比较繁琐* 不利于管理维护**  

***//使用组合api*** 

***import{ref,reactive} from'vue'  //基本类型使用ref暴露出来 reactive监听复杂类型***

这意味着引用类的数据类型，如果希望数据是响应的，得使用reactive，而不使用ref。

使用方式时直接在入口函数内定义  暴露出来即可

setup(){

​	let count =  ref(0)

​	let state = reactive（{stus:[]}

function fun(){

alert(count.value++)

}

return {count,fun,state}

}

第二种方法 模块化

```javascript
export default {
name：'App'
setup(){

​	let {count,fun,state} = demo()
	let{count1}=	demo1(count)

    return {count,fun,state}

    }
}

//可以把其放在不同文件夹下 需要引入 reactive 再export default
function demo(){
	let count =  ref(0)

​	let state = reactive（{stus:[]}

    function fun(){

    alert(count.value++)

    }
    return{count,state,remStu}
}

function demo1(){

}
```



第三种方式 comptition api和option api

comptition api本质            set up  return出的属性 都会自动放入合适的位置

#### setup执行时机:

setup：先执行

beforeCreate:

Created:  

注意点  在执行setup函数时候没有执行created生命周期函数  setup函数中 无法使用data和menthods

setup函数中this修改成undefined

setup只能是同步

#### reactive 将数据合并在一起

#### toRefs解构  ...toRefs(xxx)

vue3响应数据时通过es6的Proxy实现的 

注意点：

reactive参数必须是对象（json/arr）

给reactive传递其他对象

默认情况下修改对象  但界面不会自动更新

如果想更新  可通过自动赋值 

#### 生命周期

```vue

setup() {
    onMounted(() => {
      console.log('mounted!')
    })
    onUpdated(() => {
      console.log('updated!')
    })
    onUnmounted(() => {
      console.log('unmounted!')
    })
  },

```

与 2.x 版本生命周期相对应的组合式 API
    beforeCreate -> 使用 setup()
    created -> 使用 setup()
    beforeMount -> onBeforeMount
    mounted -> onMounted
    beforeUpdate -> onBeforeUpdate
    updated -> onUpdated
    beforeDestroy -> onBeforeUnmount
    destroyed -> onUnmounted
    errorCaptured -> onErrorCaptured

2、新增的钩子函数

    除了和 2.x 生命周期等效项之外，组合式 API 还提供了以下调试钩子函数：
    onRenderTracked
    onRenderTriggered

   两个钩子函数都接收一个 DebuggerEvent，与 watchEffect 参数选项中的 onTrack 和 onTrigger 类似：

#### computed属性

```js
const twiceTheCounter = computed(() => counter.value * 2)
```

#### `watch` 响应式更改

```js
// 侦听一个 getter
const state = reactive({ count: 0 })
watch(
  () => state.count,
  (count, prevCount) => {
    /* ... */
  }
)
// 直接侦听ref
const counter = ref(0)
watch(counter, (newValue, oldValue) => {
  console.log('The new counter value is: ' + counter.value)
}
      
```

```js
之前
export default {
  data() {
    return {
      counter: 0
    }
  },
  watch: {
    counter(newValue, oldValue) {
      console.log('The new counter value is: ' + this.counter)
    }
  }
}
```

#### vite

取代webpack

```
npm install -g create-vite
create-vite-app  vue3-demo
```

Composition api

#### 组件

https://www.yuque.com/hugsun/vue3/component 用法

Fragment 开头少一个div

### Teleport 类似于toast创建之后不会影响   布局

### Suspense 实现异步组件的方式

```vue
<Suspense>
    <template #default>//需要时间去进行加载   特殊属性
     <User/> //引入异步的组件
    </template>
    <template #fallback>
	加载时间显示的内容
    </template>
</Suspense>


<template>
</template>
import {onErrorCaptured,ref } from

setup(){
	onErrorCaptured  (e=>{
	error.value =e
return true //向外传播
})
}
处理异步操作
```

this.$nextTick(()=>{})//vue2中 使用其预加载

```vue
需要写这个接受一下 
props:{

   text:String,

   errortext:String,

   checkshow:{

​     required:true

   }

 },
```

子给父传值

setup(props, context) {
    const colorValue = reactive({
      color: props.types || "#1989fa",
      submits: () => {
        context.emit("submitFn");
      },
    });
    return {
      ...toRefs(colorValue),
    };
  },

vuex

state:{

}

mutations:{

}

actions:{

test(context) context存在 state 、mutations getters

}

getters:{

}

moudle:{}

#### 访问vuex

```
import { useStore } from "vuex";

const store = useStore();
console.log(store.state.token);
store.dispach.('')//actions方法使用
```

#### dom操作

需要通过ref来定义

```
<van-search
    ref = "status"
    v-model="text"
    show-action
    placeholder="请输入搜索关键词"
    @search="onSearch"
    @cancel="onCancel"
    autofocus='true'
  />
  const status = ref(null)
  onMounted(() => {
      status.value.focus()
    })
```



```tsx
<template>
<div ref="msgInputContainer"></div>
<ul v-for="(item, i) in list" :ref="el => { ulContainer[i] = el }"></ul>
</template>

<script lang="ts">
  import { ref, reactive, onBeforeUpdate } from "vue";
  setup(){
    export default defineComponent({
    // DOM操作,必须return否则不会生效
    // 获取单一dom
    const messagesContainer = ref<HTMLDivElement | null>(null);
    // 获取列表dom
    const ulContainer = ref<HTMLUListElement>([]);
    const list = reactive([1, 2, 3]);
    // 列表dom在组件更新前必须初始化
    onBeforeUpdate(() => {
       ulContainer.value = [];
    });
    return {
      messagesContainer,
      list,
      ulContainer
    }
  })
  }
```

vue3挂载全局属性和方法

```
const { proxy } = getCurrentInstance();
const showMessage = () => {
    proxy.$message.success("this is message");
};
return {
   showMessage
}
```

#### vue插槽使用

```vue
<template>
<div>
    <my-button btnStyle='btn-warning'>
        测试
        //需要往组件插入一部分东西
    </my-button>
    </div>
</template>

//插槽作用  当组件内需要插入一部分值时插入在那 就在哪里写<slot></slot>
组件

<template>
<buttton :class="[btnStyle]">
    <slot>
    </slot>
    </buttton>
</template>
```

inject

provide 父子组件中的值传递

只有携带Proxy的属性才可以进行双向绑定



Vue路由跳转 

```js
import { useRouter } from "vue-router";
const router = useRouter();
router.push({
              name: "ReportDetailPdf",
              params: {
                typename2: item.typename2,
                typeid2: item.typeid2,
                id2: item.id2,
                pid2: item.pid2,
                presid2: item.presid2,
                prescriptionno2: item.prescriptionno2,
                realname2: item.realname2,
                excutedate2: item.excutedate2,
                receivedate2: item.receivedate2,
              },
            });
```

#### nextTick的使用

https://staging-cn.vuejs.org/guide/essentials/reactivity-fundamentals.html#dom-update-timing

当你更改响应式状态后，DOM 也会自动更新。然而，你得注意 DOM 的更新并不是同步的。相反，Vue 将缓冲它们直到更新周期的 “下个时机” 以确保无论你进行了多少次声明更改，每个组件都只需要更新一次。

若要等待一个状态改变后的 DOM 更新完成，你可以使用 [nextTick()](https://staging-cn.vuejs.org/api/general.html#nexttick) 这个全局 API：

```
DOM更新后所要进行的操作
import { nextTick } from 'vue'

function increment() {
  state.count++
  nextTick(() => {
    // 访问更新后的 DOM
  })
}
```

# vue复习
## 动态绑定多个值[#](https://staging-cn.vuejs.org/guide/essentials/template-syntax.html#dynamically-binding-multiple-attributes

如果你有像这样的一个包含多个 attribute 的 JavaScript 对象：

```
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper'
}
```

通过不带参数的 `v-bind`，你可以将它们绑定到单个元素上：

```
<div v-bind="objectOfAttrs"></div>
```

### Class的绑定
https://staging-cn.vuejs.org/guide/essentials/class-and-style.html#binding-html-classes
```javaScript

<div :class='[active,deactive]'></div>
<div :class='{actice:active,deactive:deactive}'></div>
<div :class='state'></div>
active = ref(true)
deactive  = ref(false)

state = reactive({
	actice:true
	deactive:false
}) 
```
## 列表渲染
在计算属性中使用 `reverse()` 和 `sort()` 请保持谨慎！这两个方法将变更原始数组，计算函数中不应该这么做。请在调用这些方法之前创建一个原数组的副本：
```
- return numbers.reverse()
+ return [...numbers].reverse()
```
## 在内联事件处理器中访问事件参数[#](https://staging-cn.vuejs.org/guide/essentials/event-handling.html#accessing-event-argument-in-inline-handlers)

有时我们需要在内联事件处理器中访问原生 DOM 事件。你可以向该处理器方法传入一个特殊的 `$event` 变量，或者使用内联箭头函数：
```
<!-- 使用特殊的 $event 变量 -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- 使用内联箭头函数 -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>

function warn(message, event) {
  // 这里可以访问原生事件
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
```
## WatchEffect
回调会立即执行。在执行期间，它会自动追踪 `url.value` 作为依赖（近似于计算属性）。每当 `url.value` 变化时，回调会再次执行。

```
watchEffect(async () => {
  const response = await fetch(url.value)
  data.value = await response.json()
})
```

`watch` 和 `watchEffect` 都能响应式地执行有副作用的回调。它们之间的主要区别是**追踪响应式依赖的方式：**

-   `watch` 只追踪明确侦听的源。它不会追踪任何在回调中访问到的东西。另外，仅在响应源确实改变时才会触发回调。`watch` 会避免在发生副作用时追踪依赖，因此，我们能更加精确地控制回调函数的触发时机。
    
-   `watchEffect`，则会在副作用发生期间追踪依赖。它会在同步执行过程中，自动追踪所有能访问到的响应式 property。这更方便，而且代码往往更简洁，但其响应性依赖关系不那么明确。
## vue 模板

https://staging-cn.vuejs.org/guide/essentials/component-basics.html#defining-a-component

当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 `.vue` 文件中，这被叫做[单文件组件](https://staging-cn.vuejs.org/guide/scaling-up/sfc.html) (简称 SFC)：

1.单文件组件  也可以使用kebab-case
```
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```
2. 内联JavaScript字符串模板
```
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
  // 或者 `template: '#my-template-element'`
}
```

3.DOM模板

不能使用闭合 </>
需要使用类似 <demo-grid></demo-grid>格式 

``` javascript
<script type="module">
import DemoGrid from './Grid.js'
import { createApp, ref } from 'vue'

createApp({
  components: {
    DemoGrid
  },
  setup() {
    const searchQuery = ref('')
    const gridColumns = ['name', 'power']
    const gridData = [
      { name: 'Chuck Norris', power: Infinity },
      { name: 'Bruce Lee', power: 9000 },
      { name: 'Jackie Chan', power: 7000 },
      { name: 'Jet Li', power: 8000 }
    ]

    return {
      searchQuery,
      gridColumns,
      gridData
    }
  }
}).mount('#app')
</script>

<div id="app">
  <form id="search">
    Search <input name="query" v-model="searchQuery">
  </form>
  <demo-grid
    :data="gridData"
    :columns="gridColumns"
    :filter-key="searchQuery">
  </demo-grid>
</div>
```

## 使用 props 和 emit
需要 宏来注册一下
```
<!-- BlogPost.vue -->
<script setup>
defineProps(['title'])
defineEmits(['enlarge-text'])
</script>
```

## Component 与 is的使用
https://staging-cn.vuejs.org/guide/essentials/component-basics.html#dynamic-components
``` vue
<script setup>
import Home from './Home.vue'
import Posts from './Posts.vue'
import Archive from './Archive.vue'
import { ref } from 'vue'


const currentTab = ref('Home')

const tabs  = {
	Home,
	Posts,
	Arichve
}

<div>
	<button v-for:'(item,key) in tabs ' :key='key' @click = 'cuttentTab = key'>
		{{key}}
	<button>
		// 这个地方的值需要是组件不能够是字符串
	<component :is = 'tabs[cuttentTab]'></component>
</div>

<script>	

```

## deftineProps的校验

```javascript
defineProps({
  // 基础类型检查
  // （给出 `null` 和 `undefined` 值则会跳过任何类型检查）
  propA: Number,
  // 多种可能的类型
  propB: [String, Number],
  // 必传，且为 String 类型
  propC: {
    type: String,
    required: true
  },
  // Number 类型的默认值
  propD: {
    type: Number,
    default: 100
  },
  // 对象类型的默认值
  propE: {
    type: Object,
    // 对象或数组的默认值
    // 必须从一个工厂函数返回。
    // 该函数接收组件所接收到的原始 prop 作为参数。
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  // 自定义类型校验函数
  propF: {
    validator(value) {
      // The value must match one of these strings
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // 函数类型的默认值
  propG: {
    type: Function,
    // 不像对象或数组的默认，这不是一个工厂函数。这会是一个用来作为默认值的函数
    default() {
      return 'Default function'
    }
  }
})
```

### Boolean类型转换

```javascript
defineProps({
	disabled:Boolean
})
// 等同于 :disabled = 'true' 
<Mycomponent disabled>
</Mycomponent>
```

## emit事件校验

```javascript
<script setup>
const emit = defineEmits({
  // 没有校验
  click: null,

  // 校验 submit 事件
  submit: ({ email, password }) => {
    if (email && password) {
      return true
    } else {
      console.warn('Invalid submit event payload!')
      return false
    }
  }
})

function submitForm(email, password) {
  emit('submit', { email, password })
}
</script>
```

### v-model 代替

```Javascript
<script setup>
	defineProps(['inputValue'])
	defineEmits(['update:inputValue'])
	<template>
     <input :value='inputValue' @input = '$emit('update:inputValue',$event.target.value')/>
        </template>
</script>

//使用
const message = ref('默认值')
<Component v-model='message'></Component>
```

多个v-model绑定

```javascript
<UserName v-mdel:first-name='first' v-model:last-name='last' />
 <script setup>
defineProps({
  firstName: String,
  lastName: String
})

defineEmits(['update:firstName', 'update:lastName'])
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>   
    
```

### 处理 `v-model` 修饰符

自定义一个修饰符    依据modelModifiers

https://staging-cn.vuejs.org/guide/components/events.html#usage-with-v-model

## *作用域插槽的优雅使用

```
<Component v-slot='{x,y}'>
	Mouse is at：{{x}}，{{y}}
</Component>
```

另一种方式组合式函数的引入(建议使用) https://staging-cn.vuejs.org/guide/reusability/composables.html

## 依赖注入

provide  inject

## 异步组件（查看掘金文章）

## 组合式函数的核心知识点

将函数按功能划分，分别创建js文件  使用的时候只需要引入js文件即可

https://staging-cn.vuejs.org/guide/reusability/composables.html#mouse-tracker-example

# Vueapi

unref   类似  val ==ref ？val.value:val

isref 判断是否为ref



## 自定义指令

组合式使用方法

```javascript
1.局部指令
<script setup>
// 在模板中启用 v-focus
const vFocus = {
  mounted: (el) => el.focus()
}
</script>

<template>
  <input v-focus />
</template> 

2.全局指令

const app = createApp()

app.directive('focus',{    
})
```

指令钩子(一个指令的定义对象可以提供几种钩子函数 (都是可选的))

```JavaScript
const myDirective = {
  // 在绑定元素的 attribute 前
  // 或事件监听器应用前调用
  created(el, binding, vnode, prevVnode) {
    // 下面会介绍各个参数的细节
  },
  // 在元素被插入到 DOM 前调用
  beforeMount() {},
  // 在绑定元素的父组件
  // 及他自己的所有子节点都挂载完成后调用
  mounted() {},
  // 绑定元素的父组件更新前调用
  beforeUpdate() {},
  // 在绑定元素的父组件
  // 及他自己的所有子节点都更新后调用
  updated() {},
  // 绑定元素的父组件卸载前调用
  beforeUnmount() {},
  // 绑定元素的父组件卸载后调用
  unmounted() {}
}
```

### 钩子参数[#](https://staging-cn.vuejs.org/guide/reusability/custom-directives.html#hook-arguments

指令的钩子会传递以下几种参数：

- `el`：指令绑定到的元素。这可以用于直接操作 DOM。
- `binding`：一个对象，包含以下 property。
  - `value`：传递给指令的值。例如在 `v-my-directive="1 + 1"` 中，值是 `2`。
  - `oldValue`：之前的值，仅在 `beforeUpdate` 和 `updated` 中可用。无论值是否更改，它都可用。
  - `arg`：传递给指令的参数 (如果有的话)。例如在 `v-my-directive:foo` 中，参数是 `"foo"`。
  - `modifiers`：一个包含修饰符的对象 (如果有的话)。例如在 `v-my-directive.foo.bar` 中，修饰符对象是 `{ foo: true, bar: true }`。
  - `instance`：使用该指令的组件实例。
  - `dir`：指令的定义对象。
- `vnode`：代表绑定元素的底层 VNode。
- `prevNode`：之前的渲染中代表指令所绑定元素的 VNode。仅在 `beforeUpdate` 和 `updated` 钩子中可用。

```
<div v-example:foo.bar="baz">
{
  arg: 'foo',
  modifiers: { bar: true },
  value: /* `baz` 的值 */,
  oldValue: /* 上一次更新时 `baz` 的值 */
}
<div v-example:[arg]="value"></div>
```

## 插件

插件是一种能为 Vue 添加全局功能的工具代码。我们会这样安装一个插件：

```
import { createApp } from 'vue'

const app = createApp({})

app.use(myPlugin, {
  /* 可选的选项 */
})
```

它可以是一个拥有 *`install()` 方法的对象*，或者就简单地**只是一个函数**，它自己就是安装函数。安装函数接收[应用实例](https://staging-cn.vuejs.org/api/application.html)和传递给 `app.use()` 的额外选项：

```
const myPlugin = {
  install(app, options) {
    // 配置此应用
  }
}
```

插件没有严格定义的使用范围，但是插件发挥作用的常见场景主要包括以下几种：

1. 通过 [`app.component()`](https://staging-cn.vuejs.org/api/application.html#app-component) 和 [`app.directive()`](https://staging-cn.vuejs.org/api/application.html#app-directive) 注册一到多个全局组件或自定义指令。
2. 通过 [`app.provide()`](https://staging-cn.vuejs.org/api/application.html#app-provide) 使一个资源[可被注入](https://staging-cn.vuejs.org/guide/components/provide-inject.html)进整个应用。
3. 向 [`app.config.globalProperties`](https://staging-cn.vuejs.org/api/application.html#app-config-globalproperties) 中添加一些全局实例属性或方法
4. 一个可能上述三种都包含了的功能库 (例如 [vue-router](https://github.com/vuejs/vue-router-next))。

### 编写一个插件 

编写一个简单的插件(一定要学一下)

```
./plugins/i18n
export default {
	install:(app,option)=>{
		app.config.globalProperties.$translate = (key)=>{
			return key.split(',').reduce((o,i)=>{
			if(o) return o[i]
			},options)
		}
	}
}

// 使用方法
import i18nPlugin from './plugins/i18n'
// 注册之后全局使用
app.use(i18nPlugin, {
  greetings: {
    hello: 'Bonjour!'
  }
})
<h1>{{ $translate('greetings.hello') }}</h1>
```

### 插件中的注入与供给

```javascript
export default {
	install:(app,option)=>{
		app.config.globalProperties.$translate = (key)=>{
			return key.split(',').reduce((o,i)=>{
			if(o) return o[i]
			},options)
		}
        // 全部注入
        app.provide('i18n',option)
	}
}
// 使用

<script setup>
import { inject } from 'vue'
const i18n = inject('i18n')
console.log(i18n.greetings.hello)
</script>
```

## 内置组件

### Teleport 

`<Teleport>` 是一个内置组件，使我们可以将一个组件的一部分模板“**传送**”到**该组件的 DOM 层次结构之外的 DOM 节点中**

```javascript
// 例子
<button @click="open = true">Open Modal</button>

<Teleport to="body">
  <div v-if="open" class="modal">
    <p>Hello from the modal!</p>
    <button @click="open = false">Close</button>
  </div>
</Teleport>
```

### Suspense 异步组件

如果该组件是异步的 则会在等待时候触发 #fallback

```
<Suspense>
  <!-- 具有深层异步依赖的组件 -->
  <Dashboard />

  <!-- 在 #fallback 插槽中显示 “正在加载中” -->
  <template #fallback>
    Loading...
  </template>
</Suspense>
```

`<Suspense>` 可以等待的异步依赖有两种：

1. 带有异步 `setup()` 钩子的组件。这也包含了使用 `<script setup>` 时有顶层 `await` 表达式的组件。
2. [异步组件](https://staging-cn.vuejs.org/guide/components/async.html)。

## 升级规模

通过[动态组件](https://staging-cn.vuejs.org/guide/essentials/component-basics.html#dynamic-components)的方式，监听浏览器 [`hashchange` 事件](https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event)或使用 [History API](https://developer.mozilla.org/en-US/docs/Web/API/History) 来更新当前组件。

[`hashchange` 事件](https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event)

特点:1.带#丑陋 

[History API](https://developer.mozilla.org/en-US/docs/Web/API/History) 



使用history的时候会有一些问题  需要修改配置