### vue3学习

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

Teleport 类似于toast创建之后不会影响   布局

Suspense 实现异步组件的方式

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

### vue插槽使用

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

