第一天 

实现 vue-router

1.实现之前会有一些问题

（1）VueRouter是一个插件？  内部做了什么   实现两个组件

​		1.router-view router-link

​		2. install方法: this.$router.push()

​	2 创建实例（单例模式）

​	3 添加到配置项  为什么  在main.js中引入

​	4  路由出口 <router-view></router-view>

vue插件怎么写

**必须有一个install方法，将来要被Vue.use调用**



```js
let  Vue   //保存Vue构造函数  插件中要使用
class VueRouter {
	constructor（options）{
        this.$options = options
        
        (需要修改为响应式数据)
        //this.current ="/"
        //修改之后
        const inital = window.location.hash.slice(1) || '/'
        Vue.util.defineReactive(this,'current',inital) //设置响应式   给this定义一个current  inital为初始值
        //监听hash变化
        
        window.addEventListener("hashchange",()=>{
            console.log(this.current);
            this.current = window.location.hash.slice(1) //截取hash路径
        })
    }

}
VueRouter.install = function(_Vue){   //使用ues调用  执行时很早
	Vue = _Vue
    //全局混入  混入也可以进行全局注册。使用时格外小心！一旦使用全局混入，它将影响每一个之后创建的 Vue 实例。使用恰当时，这可以用来为自定义选项注入处理逻辑。    创建后的实例都有这个
	Vue.mixin({    
		beforeCreate(){
	
		//1.挂载$router属性
        // this.$router.push() 路由器实例    
             //根实例  将router挂载到Vue.protortype 
            //this.$options 用于当前 Vue 实例的初始化选项。需要在选项中包含自定义 property 时会有用处：
            if(this.$options.router){
                Vue.prototype.router = this.$options.router
            }
		}
	})
        
        2.注册实现组件 
        Vue.component('router-link',{
        props：{
        to:{
        type:String
    }
    }
       //h == (createElement: () => VNode) => VNode
        render(h){
        //<a href={'#'+this.to}>{this.$slot.default}</a>
        	return h("a",{attrs:{href:"#"+this.to}},this.$slot.default) //渲染函数方式 虚拟domrender函数
    	}
    })
    Vue.component('router-view',{
        render(h){            
            this.$router.$options.routes.find((route)=> route.path === this.$router.current)
            return h(null)
        }
    })
}


VueRouter.install = function(Vue)
```

需要借用响应式数据  实现监听改变 路由操作（无法实现嵌套路由）

## Vuex 源码分析

//1.实现插件：挂载store

//2.实现store

//mutations 里add方法中的state怎么来的

```

```

//actions 里的参数是哪来的{commit}

```js
let Vue

class Store {
    cunstructor(options){
        //data响应式处理
        this.state = new Vue({
            data:{
                $$state:options.state
            }
        })
        
        this._mutations  = options.mutations
        this._actions = options.actions 
        
        this.commit = this.commit.bind(this)
        this.dispatch = this.dispatch.bind(this)
        this.getters={} //定义响应式 建议使用difineproperty 控制里面值
    }
    get state(){
        return this._vm._data.$$state //_data为$data  是vue内部的东西
    }//不能够赋值直接替换  只能得到state 不能直接 this.state == 11
    set state(v){
        console.error()
    }
    commit(type,payload){
        const entry = this.mutations[type]
        if(!entry){
            console.log('unkown mutation type')
        }
        entry(this.state,payload)
    }
    dispatch(type,payload){
        const entry = this.actions[type]
        if(!entry){
            console.log('unkown actions type')
        }
        entry(this.state,payload)
    }
    
}

//Vue.use调用 写法 install.call(this,.)
function install(_Vue){
	
	Vue =_Vue
	//挂载到Vue  vue.use调用拿到
	Vue.mixin({
	beforeCreate(){
	if(this.$options.store){
	Vue.prototype.$store = this.$options.store
		}
	}
	})

}
//创建install的时候与Vuex有一定的区别

//因为引入时 是Vuex.Store 所以暴露出来的 要改变

export default {Store，install}
```

属性为什么放在data里？

 需要把所有的属性递归 转化为响应式

data()为什么是函数式  因为data如果是对象 所有组件都会在同一个data里

