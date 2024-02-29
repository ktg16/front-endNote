#### defineComponent

1.defineComponent 是 Vue 3 推出的一个全新 API ，可用于对 TypeScript 代码的类型推导，帮助开发者简化掉很多编码过程中的类型声明。

```
const uids: number[] = reactive([1, 2, 3])

/**

 * 推荐使用这种方式，不会破坏响应性
   */
   uids.length = 0

// 异步获取数据后，模板可以正确的展示
setTimeout(() => {
  uids.push(1)
}, 1000)



```

js基础

https://juejin.cn/post/6996289669851774984#heading-7 



我的vue写法就是。Hooks 写法

```
export const getData = ()=>{}
export default function unInstance () {
	...
	return{...}
}

import unInstance,{ getData } from 'xxx.js'
const {,,,} = unInstance()
onMounted(()=>{	
	getData()
})
```

https://juejin.cn/post/7073774752606715935 css





/组件通信 props emits。  defineExpose/ref。 Vuex/Pinia  mitt provide/inject

Attrs.可以直接使用const attires =  useAttrs() attrs v-model可以链接子组件
