#  vue

 https://www.jsdelivr.com/ 查找我们要用的一些第三方的框架，cdn配置服务器的url。

mvvm模式   module-view-module         模板改变视图改变    视图改变   模板改变



vue提供一个双向数据绑定的  指令   v-model 绑定两个数据绑定name

vue的vue-cli4.0  https://github.com/staven630/vue-cli4-config#compressimage

###### v-text

挂载  纯文本  标签间可以写模板字符串    指令里面只能写表达式

###### v-html 

语法一致   解析标签

###### v-show

 绑定两个节点  根据表达式结果的真假值   切换元素的display属性 v-show = '!isLogin' v-show = 'isLogin'

###### v - if

与v-show相似  通过表达式的值，来控制元素是否渲染    v-if = "xxx" xxx就是表达式

v - if与v-show区别

1. v-if 是真的条件渲染，默认条件为false时，元素不渲染，默认条件是true时，元素渲染
2. v-show控制display 的变化  一开始都会被渲染
3. v-if 可以通过template 做一些配合使用  v-show不可以

v-else-if   v-else 用于判断      <p v-else-if = "score >= 60">及格</p>

###### template

 元素    不会渲染到我们的页面上，不会影响样式布局  如果只使用v-if会影响布局

###### v-for

1. v-for指令  用于循环v-for = "item in xxx";  循环数组

   ​    item 循环中元素

   ​    in  语法

   ​    xxx  要循环的数据 

   v-for = "(item, index) in xxx";

      index  循环的下标

2.  循环对象  v-for = "item in xxx";

​    item 循环的xxx的属性值

3. 循环字符串

   v-for = "item in 字符串"

​    item是字符

4.循环数字

   v-for = "item in 10";

###### 数组的变更方法

- `push()`

- `pop()`

- `shift()`从头取下

- `unshift()从头添加`

- `splice()增删改查

- `sort()`

- `reverse()`

  

以下方式不会改变数组

1.直接修改下标的方式修改数组

2.修改数组长度改变数组的内容



###### 		数据监测更新

数组的一部分方法成立object.defineprototype()浅层监听



1. Vue.set(vm.target,index,value)
2. vm.$set(vm.target,index,value);



对象的更新检测

Vue.set(target,key,value)

v-on 事件 这个函数必须定义在 Vue 实例的 methods 选项中

@click

<button v-on:cliclk = 'fn1()'>加了()不会立即执行

methods:{

fn（）{

}

}

###### -on的修饰符

事件修饰符： .修饰符

1. stop  阻止冒泡

2. prevent 阻止默认行为

3. capture 让事件成为一种捕获行为

4. self  只有事件触发在绑定事件的元素上才触发

   5、keyCode | keyAlias 特定的键盘修饰符

​		.enter

​    .tab

​    .delete (捕获“删除”和“退格”键)

​    .esc

​    .space

​    .up

​    .down

​    .left

​    .right



 6、once  只绑定一次事件

   7、left  绑定鼠标左键

   8、right 绑定鼠标右键的

   9、middle 绑定鼠标滚轮

 系统修饰符

​    .ctrl

​    .alt

​    .shift

​    .meta

   10、exact 精准匹配  只能是这个常配合键盘事件使用

event事件对象   event.target.value  目标函数的值













###### **v-bind** 

将数据绑定在属性上     title id class value

v-bind:id = str   语法糖 简写  :id = str

v-bind = "{name:name, age: age}    等同于v-bind:name = "name" v-bind:age = "age"         也可以绑定字符串

# vue day2

v-bind绑定  class和style不一样



:class属性

1. v-bind:class = "'hello'"  直接使用字符串hello作为类名

2. v-bind:class = "hello"   使用 hello 这个数据的值作为类名

3. 对象 v-bind:class = "{key1: value1, key2: value2}

   根据 value1 这个值是否为真，来控制 key1 是否在class上添加

   根据 value2 这个值是否为真，来控制 key2 是否在class上添加

   

4. 数组 v-bind:class = "[value1, 'value2', value3, {key: value}]";

   a. 根据 value1 这个数据的值作为其中一个类名

      b. 根据 value2 这个字符串值作为其中一个类名

      c. 根据 value3 这个数据的值作为其中一个类名

      d. 根据 value 这个数据的真假，来确定 key 是否被添加到类名

-style绑定行间样式

1. v-bind:style = "color: red" 这种写法是直接报错的

2. :style = "{color : mycolor,fontSize:mysize,fontWeight:'blod'}"

   key为属性名 value值为属性的值 “blod”字符串为属性的值 

3. 数组  :style= "[value1, value2, {color: myColor}]"

   value1数据来控制   value2数据控制    myColor属性值控制

css属性名  是短横线写法，需要换成驼峰写法

font-size  >  fontSize

###### -model是语法糖  真实形态

```javascript
<p> {{msg}}</p>
<input type = "text" v-bind:value = 'msg' @input = "msg = $event.target.value"/>
```



v-model.number  强制转换成number类型 不能转换保持输入即可

.lazy失去焦点是才发生绑定    将默认的 input 事件修改为 change 事件修改内容失去焦点

.trim 去除前后多余的空格

###### v-pre   

需要在页面直接输出{{}}这种格式的字符串不让vue对其进行操作

```
<p v-pre>{{msg}}</p>
```

输出{{msg}}

###### v-cloak

 页面闪烁问题  ：vue 解析页面的时候需要时间

解决  或者不使用插值表达式 改用v-text

1.写在挂载点元素上  没有参数也没有表达式

2.需要些全局变量 [v-cloak]{display:none}

例子：  <p v-cloak>{{msg}}</p>

###### v-once

让元素默认绑定数据一次  后续数据不会改变



methods方法  用于事件方法

###### watch  

监听数据的变化    不与双向绑定冲突     new参数是现在的数   old是之前的数

普通函数写法

监听 a

​    // a:function(newVal,oldVal){

​    //   console.log(`newValue:${newVal}`);

​    //   console.log(`oldVal:${oldVal}`)

​    // }

​    //2对象函数的简写方法

​    // a(newVal,oldVal){

​    //   console.log(`newVal:${newVal}`);

​    //   console.log(`oldVal:${oldVal}`)

​    // }

​    //3.注意！！ 不能使用箭头函数 methods选项中也不可以使用箭头函数 因为this会指向vm实例 

​      // a:(newVal,oldVal) => {

​      // console.log(`newVal:${newVal}`);

​      // console.log(`oldVal:${oldVal}`)

​    // }

  //4.string方法

   // a:"hello" 

//methods：{hello:function(newval,oldVal)}

  //5.对象object写法



  // a:{

  //   //一定要提供一个handler属性   属性值，处理函数必须需要

  //   handler(newVal,oldVal){

  //     console.log(`newVal:${newVal}`);

  //     console.log(`oldVal:${oldVal}`)

  // }

###### 为什么要用object写法

  //6.object写法   可以做更多的监听配置比如深度监听  默认触发监听一次

​    // obj:{

​    //   handler(newVal,oldVal){

​    //   console.log(`newVal:${newVal}`);

​    //   console.log(`oldVal:${oldVal}`)

​    //   },

​    //   如果不写监听不到 deep:true,//代表深度监听

​    //   immediate:true//默认触发一次

​    // }

  //7.数组的写法 [string,function,{hander:funcion}]   当a去修改 三个方法都执行

  a:[

​    "hello",

​    function(){

​      console.log('12')

​    },

​    {

​      hander:function(){

​        console.log('12')      }

​    }

  ]

// key 可以写成表达式 直接去监听某一个对象的某一个属性obj.name

   "obj.name": function(newVal, oldVal){

​    console.log(newVal, oldVal);

   }

###### -computed

​      配置选项 （计算属性、衍生属性、派生属性）

**面试题   为什么不使用watch     优先选择使用 computed， computed 有缓存 会对比两次变化 如果相等则不执行**

面试题 computed 能实现的 都可以通过methods都能实现

优先选择使用 computed， computed 有缓存

调用的格式上：

   methods: xxx()

   computed: xxx

计算属性值不能修改！！  为单向数据流

 调用的格式上：

   methods:{ xxx()}

   computed: {xxx}

总结计算属性的特点：

​    1、计算属性可以像data中的数据一样去使用

​    2、计算属性不允许手动修改的它的值，因为它的值根据依赖项来的，只有依赖项发生变化，他的值才会发生变化

​    3、计算属性有缓存的，默认计算出来只有，如果依赖项不发生变化，后续将一直使用缓存的数据。

​    4、计算属性可以重设 setter 和getter方法，但是就算有setter，他也改变不了计算属性的值，真正能改变的，只有通过改变依赖项，才能改变。

###### template

1、template 作为包裹元素的标签来使用，最后不会渲染到页面上 配合v-if v-if 创建删除/v-show显示/隐藏

   2、template 配置选项

​    如果有 template 选项，那么就会直接使用 template 选项中的内容作为模板，**解析完成以后替换调换掉挂载元素。**

​    **如果没有 template 选项，那么使用指定 el 元素作为模板，后续解析完成以后，挂载元素**



描述vue原理

###### swiper使用

实现轮播 vue day42

官方推荐使用 vm.$nextTick(callback)

延时器  不能控制

swiper更新  每一次更改就更新数据量大



###### day42vue生命周期

箭头函数去看看  箭头函数this指向父元素

事件轮询event  loop

day16中



生命周期钩子函数

1. 初始化挂载阶段
   1. beforeCreate 
   2. created 是Vue实例 vm实现好了 使用vm.$mount("#app") 挂载
   3. beforeMount 
   4. mounted 
2. 更新阶段
   1. beforeUpdate 
   2. updated 
3. 销毁阶段
   1. beforeDestroy   在销毁前清除定时器清除全局否则会内存泄漏
   2. destroyed 

polyfill垫片  es6传入es5



###### component   注册组件

组件命名方式   baseInput    base-input

第一个参数是组件的名字，

 第二个参数配置项{} 基本上和 new Vue()参数差不多

components 局部组件   

```
Vue.component("com1",{

​    template:`
        <com4></com4>
        <div>我是组件</div>
		`,
		components:{
		com4:{template}
		}

  })
```

组件中的data  必须是一个函数  必须返回一个新的对象        只能data(){} 

  原因：组件可以被用来创建多个，如果data是一个一个纯粹的对象，那么所有创建出来的组件会引用同一个对象中的数据！！！。 不能共享数据

######  组件的 inheritAttrs 配置项

   组件接收到 非 props 属性 自动继承到组件的根元素上，但是不希望继承，就可以配置 inheritAttrs: false,、

###### this.$attrs

获取到组件上所有非props的attribute属性

组件名可以写在script标签里  需要设置  type = “text/x-template”  给其设置一个id（不用）

###### 组件关系

父 -> 子 props

子 -> 父 

兄弟

Vue 遵从一个原则： 单项数据流的原则     只能从父组件子组件改数据。



  如果我们组件中的值，需要外面在调用组件的时候确定的话，我们可以将组件的值，当做行间的属性传入进行。 

定义组件 ，组件只有一个根节点   

Vue.component("com1",{

props: ["name", 'age', "sex"],

    template:`
        <com4></com4>
        <div>我是组件</div>
    	`,
    	components:{
    	com4:{template}
    	}

  })

###### 在组件中如何设置默认值呢？



  Vue.component("hello", {

   props: {//里不可以设置驼峰式

​    key1: {type: String, default: ''},

​    key2: {type: String, default: ''}

​    ...

   }

  })



  type: String, Number ... 代码对应prop属性希望接收的数据类型是什么类型

  type：是用于做类型校验的

   required: true //必须传 不传入会报警告



  validator 对传入的值做判断

  validator: function(value){

   value 是 props = 值，如果满足return后面表达式，说明这个值就可以通过，否则校验不通过，报错。

   return value > 20;

###### 非 props 的 attribtue (非prop的特性)

在调用组件的时候，设置属性(attribtue)，如果这个组件中没有定义相应的prop，那么这个属性叫做非props 的 attribtue 属性

 二、非props 的 attribtue 属性

   1、他们会继承，直接继承组件的根元素上

   2、是一个替换覆盖的操作



  三、class 与 style 与上面的区别

   1、继承，直接继承组件的根元素上

   2、他们不是替换，而是拼接组件

​    3、当我们在调用组件时     除自定义组件class style      要修改样式时 直接在调用组件的时候设置自己clas和style。  

this.$attrs 获取非props属性    this.$props获取组件属性值

​	四   、组件接收到 非 props 属性 自动继承到组件的根元素上，但是不希望继承到根组件，就可以配置 inheritAttrs: false,

注册组件时  可以使用$attrs将非props属性绑定上去 ：v-bind =$attrs

如果使用inheritAttrs = true的话不合适 会挂载不到具体位置  

组件里面的data必须时函数   data(){ }

###### 单向数据流

子修改父时

1、子组件不能直接修改prop属性

  2、应该和父亲（打声招呼）

###### this.$emit("abc",{})  

//将abc绑定  值传入父亲需要通过父组件去修改值

   \1. 子组件中 $emit() 去触发这个自定义事件

   子组件的方法

​    methods: {

​     fn1(){

​      //触发自定义事件（emit发出发行）

​      this.$emit("abc", payload)

​     }

​    }

2. 父组件中注册一个自定义的事件，监听这个自定义事件  通过事件处理函数获得参数payload

   <son @abc = "事件处理函数"></son>



   【注】自定义事件 payload 参数 是 $emit("自定义事件", payload);

​      官方支持事件 payload $event;

###### 兄弟之间通信

 1、最简单粗暴的方式，找他们的共同的爹



   2、推荐 中央事件管理器（中央事件总线） 发布/订阅

​    适用于：亲兄弟之间或者关系比较复杂的组件之间都可以



​    1、先创建一个空Vue的实例，也就是不传入任何的配置项

​     const bus = new Vue();

​    2、A B 两个组件， A 通信 B

​     a. 先在B的组件里 created 中 通过bus 来监听自定义事件

​      bus.$on(eventName, callback)

​       \- eventName 要监听事件的名字（自定义）

​       \- callback  事件在触发的时候的回调函数

​        -payload  触发这个事件的时候传过来的 payload 参数



​     b. 在A 组件的某个时候触发这个事件名字

​      bus.$emit(eventName, payload);

​       \- eventName 要触发的事件名字

​       \- payload  触发事件时传递过去的参数



​    3、vuex 全局状态管理器

###### Object.definepropety

第一个参数:目标对象  

   第二个参数  需要定义的属性或方法名字

   第三个参数：配置项

​    configurable 总开关 （是否允许进行设置）

​     如果，不传入这个配置项，设置别的配置项，这个配置项会被设置为true。

​     如果configurable 设置false，其他的配置全部失效。

 var a = {};

  Object.defineProperty(a, "b",{

​    value: 123,

​    writable: true,  为false时    属性不能被修改  只能读取

​    enumerable: true, 默认时false  是否能在for  in遍历      或在Object.keys遍历

  })

console.log(Object.keys(a));键放在数组返回

  console.log(Object.values(a));值放在数组返回

Object.definepropety() 实际上就a.b=10 a['c'] =20的原理

###### set get

```
Object.defineProperty(a, "b", {
        set: function (newValue) { //newValue是等于号赋值进来的值
          console.log("你要给我赋值的新值是：" + newValue);
          // console.log(this); 查找this：这里面的this就是我们的a对象

          // this.b = newValue; 这样的代码非常危险 会产生递归 重新执行 a.b 使用value赋值不会重新触发
          this.value = newValue;
        },
        get: function () {
          console.log("你取我的值");
          // return 'hello';//返回的全是hello

          // return this.b  这个代码也递归
          return this.value;
        }
      });
```



###### slot插槽

调用组件的时候，写在组件里的内容，默认是不会被渲染的

有时，我们需要在写组件的时候，希望写在组件标签内的内容也被渲染出来，这个时候，我们就使用slot这个功能。  <solt></solt>

```
//这个意思  父组件里面的‘测试’不会被渲染 如果子组件中加入了slot则 内容就会被渲染
<template>
<div>
    <my-button btnStyle='btn-warning'>
        测试
        //需要往组件插入一部分东西
    </my-button>
    </div>
</template>
```

solt可以设置默认内容

###### 具名插槽

 给slot标签设置一个 name 属性。这时这个 slot 标签 叫做具名插槽

给slot取了名字之后， slot内容渲染在哪个 slot 里面，可以通过设置slot属性的名字指定

top

```
<p slot = 'bottom'>我的天，你太帅了</p>
```

   

```
<p slot = 'top'></p>
```



 slot 有一个默认的名字 叫做 default

​    <slot></slot> <slot name = 'default'></slot>







###### 插槽作用域

1.编译作用域

父级模板里面所有的内容都是在父级作用域中编译的，子模版里面的内容都是在子作用域编译

子级内容在父级模板中显示

```
<hello> 
      <p slot='top' slot-scope = "{msg}" >{{msg}}  123456</p>
    </hello>
    
    
    
    Vue.component("hello",{
    data(){
      return {
        msg:"dwx"
      }
    },
    template:`
    <div>
      <p>{{msg}}</p>
      <slot name = 'top' :msg = 'msg'>
      </slot>
    </div>
    `

  })
```



2.插槽的编译作用域

 注意：虽然说插槽的内容最终渲染在子组件内，但是他的编译作用域，还是要看插槽的内容写在哪个组件的template里面，

​    而不是看插槽内容最终渲染在哪个组件的template里面的slot标签里。

```
<hello>
      <p>我是一个插槽内容{{msg}}</p>
    </hello>
    <hello></hello>
    
    Vue.component("hello", {
    data(){
      return {
        msg: "hello"
      }
    },
    template: `
      <div>
        <slot>
          //<p>默认内容{{msg}}</p>
        </slot>
        <h1>hello world -- {{msg}}</h1>
      </div>
    `
  })
  var vm = new Vue({
    el: "#app",
    data: {
      msg: 'root'
    }
  })
    
    
```

###### 新语法的具名插槽

、v-slot 语法

​    v-slot:xxx=yyy

​     \- xxx 插槽的名字

​     \- yyy 作用域插槽的数据



​    1、**v-slot 必须用在 template 包裹元素上**，也就说， 插槽内容 <template> 元素标签包裹起来然后再用组件名包裹

​    2、如果插槽没有设置名字name， v-slot === v-slot:default

​    3、v-bind 简写 :

​      v-on  简写 @

​      v-slot 简写 #

###### v-model在子组件上使用

v-model 是 v-bind:value = 'msg' @input = "handleInput" 的语法糖

需要使用$emit()方法

获取传入的内容

```
<base-input v-model = 'msg1'></base-input>

Vue.component("baseInput", {
    props: {
      value: {
        type: String
      }
    },
    template: `
      <div>
        <label>
          {{value}}
          <input type = 'text' :value = "value" @input = "handleInput"/>
        </label>
      </div>
    `,
    methods: {
      handleInput(event){
        //1、获取输入框输入的内容
        let value = event.target.value;
        console.log(value)
        this.$emit("input", value);
      }
    }
  })
var vm = new Vue({
    el: "#app",
    data: {
      msg1: "hello",
      msg2: 'world'
    },
    methods: {
      fn1(value){
        //value 子组件派发是传过来的payload
        // console.log("fn1", value);
        this.msg1 = value;
      }
    }
  })

```

$event

​    1、原生的事件是事件对象

​    2、自定义事件，它是触发事件的时候传递过来的payload参数

​    $event = this.$emit("input", payload)

​    $event === payload

###### native修饰符

使用native  作用是将事件绑定在**组件根元素**上

如果不使用  原属性就是click 相当于  abc自定义一个组件

原理是   直接在组件上添加 @click = "$emit('click') 

###### 动态组件componentday44

需要一个属性  is属性   is属性的值就是需要渲染的组件的名字

  <component :is = "curPage"></component>

将is属性设置为可以变化的值  curpage如果组件不存在会报错  组件存在就显示

###### keep-alive内置组件（易面）

描述一下 keep-alive 缓存组件后的特点：

​    1、切换组件的时候，当前组件不会触发销毁的生命周期钩子函数，就是不会被销毁了

​    2、切换回来的时候，也不会被重新创建。

​    3、会多出来两个生命周期钩子函数

​     3.1 activated 缓存激活 第一次的时候触发，组件被看到的时候触发

​      一般在这个钩子函数里，做和created 一样的事情：请求数据



​     3.2 deactivated 缓存失活 组件看不到，消失的时候触发

​      一般做 beforeDestroy 做一样的事情，清除定时器，移出全局的事件绑定。

​    4、可以 vue devtools 上面可以组件的缓存效果

keep-alive 的更多属性设置：

​    \1. include 包含控制几种组件被缓存

​     <1> include = "组件1,组件2" 注意 逗号前后不要有空格

​     <2> :include = ["组件1", "组件2"]

​     <3> :include = "/^hello/"



​    2、exclude 排除    几种组件不被缓存

​      <1> exclude = "组件1,组件2" 注意 逗号前后不要有空格

​      <2> :exclude = ["组件1", "组件2"]

​      <3> :exclude = "/^hello/"



​    3、max 规定最大能缓存的组件的数量，默认没有现有限制的

​       队列的形式（第一次被创建的时候入队）

###### vue路由

三种创建方式

hashchange事件

window.onhashchange = function(){

​	根据hash值（#后面的部分）的变化   进行对应的路由操作

}

h5以后的新特性  在路径发生变化的时候会触发。

history.pushState和history.replaceState，1个事件是指window.onpopstate事



VueRouter 底层源码就是通过上述这两种方式实现的。

1.改变hash值  通过window.onhashchange  去改变页面

2.监听路径发生变化触发以上事件

vue

2.0新增  history模式路由     3.0修改  hash的操作 删除#

###### 如何实现路由vue

1.引入Vue核心文件后  再去引入VueRouter的核心文件

2、准备路由的页面组件

3、定义路由规则，是一个数组对象

4、实例化路由对象，使用new VueRouter 生成一个 router 实例

​     let router = new VueRouter({

​      //路由实例的配置，主要是一个routes 配置项，这个选项填入路由规则

​     })

5、实例化Vue根组件的时候，也就是`new Vue()`的时候，需要配置 router 选项，选项就是创建好的 router 实例。

​     这时，会发现，页面地址栏 出现 #

​     GET #/

​     GET #/home 渲染home组件的路由视图

​     GET #/list 渲染list组件的路由视图

​     GET #/about 渲染about组件的路由视图

【注】如果想要在页面上看到视图效果，那么你必须在你想显示的部分，填入一个router-view的全局组件，用于渲染我们的组件。

###### router-link  组件来导航

**<router-link>** 是一个组件，该组件用于设置一个导航链接，切换不同 HTML 内容。 

<router-link> 默认会被渲染成一个 `<a>` 标签

使用 router-link 比 普通 a 标签好在哪里？

   1.路径不需要写 # 号了。

​    hash history 两种模式 后期如果我们在两种中进行切换，更加方便。

   2.能够更加方便的去设置高亮效果。

   \1. router-link-exact-active

   \2. router-link-active

1.**to** 属性为目标地址， 即要显示的内容。

3.router-link-active/router-link-exact-active   这是router-link的默认属性 直接覆盖就可以，如果两个都实现router-link-exact-active          后面的会覆盖前面的

 如果要给上述这两个class进行重命名

   1、active-class = 'xxx'  重新设置的 router-link-active的样式

   2、exact-active-class = 'xxx'  重新设置的 router-link-exact-active 的样式

2.replace

3.append

4.tag

###### 路由模式

一、切换模式

   new VueRouter() mode选项，改一下就行   hash和history  默认hash



###### 二、路由高频面试题

   hash 模式 和 history的区别

   1、url地址表现不同，hash模式有#号，history模式没有

   2、实现原理不同

​    a. hash模式，是通过改变hash值改变路径， 监听hashchange这个事件

​    b. history模式，基于HTML5新增的属性history 相关的api进行的一些操作

​     history.pushstate()

​     history.replacestate()

​     history.onpopstate(); 监听浏览器前进后退的行为



   3、兼容性不同

​    a. hash模式都可以兼容

​    b. history模式，只能兼容IE10以上

​    ps：vue的兼容性，最多只能兼容到IE8以上。



   4、history模式，会刷新以后出现404找不到页面的这种情况，需要后端配置相关的处理才行，而hash模式没有这个问题

   5、history模式的时候，重定向会有些问题，需要页面的名字叫做index.html才行。

###### 路由重定向

需求：

   项目启动以后，默认访问路径是 #/

   希望项目默认打开以后，跳转#/home 这个路由

在定义路由规则最前面添加

```
{
   path: "/",
   redirect: "/home"
  },
```





###### 路由别名

给路由规则中的path设置一个别名（外号）

   /home -> /a

   /list -> /b

   /about -> /c

   路由规则里面 配置项 alias 配置项 在定义路由规则写入  alias:"/a"

###### 动态路由

 路由规则中path 选项值 写成 ： /home/:xxx/:yyy 这种就是动态路由

   app.get("/admin/:id");  /admin/1

获取详情页面的id是多少

​    $route 对象，这个对象代表着当前匹配的路由的信息对象，这个对象中有

​    有很多属性：

​     **\- path 路由路径**

​     \- query **当前路由?号后面传递的参数，是一个对象。类似express req.query 获取到东西**

​     **\- params** 当前路由的动态参数，是一个对象。 类似express req.params 获取到东西

​     **\- fullPath** 与 path  当前路由的一个完整的路径，包括?后面的部分

​     \- meta  当前路由的元信息，是一个对象

​         定义在路由规则里，设置meta配置项

data(){}  data独享一个数据





###### *多级路由 嵌套路由*

问题需求  1.访问时详情页时不显示tabbar

解决方式 tabbar和页面同级 做一些路由级别的划分

###### 命名路由

在路由规则中加一个name

```
<router-link  :to ="{name:'a'}">home</router-link>
{
        path:'/home',
        name:'a',
        component:home
      },
```

###### 命名视图

有多个router-view给router-view  起名字

###### todolist程序

###### sync修饰符

传递给组件的prop属性  通过组件修改属性

1.组件内触发的自定义事件名字修改一下

this.$emit()

2.父亲组件的代码

###### 默认行为阻止   

@submit.prevent  或者   @input.enter  

进行本地存储

1.cookies

2.window.localStorage.setItem("todos",JSON.stringify(this.todos))本地设置

拿出 window.localStorage.getItem("todos") ? JSON.parse(window.localStorage.getItem("todos"))||[]

深入异步更新队列   ref需要和  this.$nextTick配合使用

```
Vue.component('example', {
  template: '<span>{{ message }}</span>',
  data: function () {
    return {
      message: '未更新'
    }
  },
  methods: {
    updateMessage: function () {
      this.message = '已更新'
      console.log(this.$el.textContent) // => '未更新'
      this.$nextTick(function () {
        console.log(this.$el.textContent) // => '已更新'
      })
    }
  }
})
```

##### vue知识点

 v-for优先级高于v-if  一般先套v-if v-for

双向数据流问题  

性能优化冻结对象  freeze

web安全 转译问题  xxs

