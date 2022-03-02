## axios的使用；

https://juejin.cn/post/7034827130701611016#heading-7

调用型

axios.get('/get',{params:{}}).then()

axios.post('/post',{})

方法型

axios({method:'post',url:'/',data:data}).then()

put更新数据（将所有数据均推放到服务端） patch更新数据（只将修改的数据推送到后端）写法与post没有区别   只是method不同

delete写法

并发请求

function getUserAccount() {  return axios.get('/user/12345'); } function getUserPermissions() {  return axios.get('/user/12345/permissions'); }



axios.all([getUserAccount(), getUserPermissions()])  .then(axios.spread((acct, perms) => {    // 两个请求都完成后,acct是getUserAccount的返回值，同理，perms是 getUserPermissions的返回值  }));

jq的ajax

1.本身是针对MVC的编程,不符合现在前端**MVVM**的浪潮
2.基于原生的XHR开发，XHR本身的架构不清晰。

3.JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）
4.不符合关注分离（Separation of Concerns）的原则

Axios与ajax的区别；

传统 Ajax 指的是 XMLHttpRequest（XHR）

axios是对于ajax的封装解决了ajax的回调地狱

websocket跟ajax区别；

服务端向客户端发送请求

了解fetch；



request header；response header；

# 什么是axios?

Axios是一个基于promise的http库,可以用在浏览器和node.js中

对原生XHR的封装

## axios特性

- 从浏览器创建XMLHttpRequest
- 从node.js创建http请求
- 支持promise Api
- 拦截请求与响应
- 取消请求
- 自动装换JSON数据
- 支持客户端XSRF攻击 **跨站请求伪造** **防止CSRF**
- 提供了一些并发请求的接口（重要，方便了很多的操作）

## 1.Axios为什么可以用于浏览器和node.js

简单来说就是通过**判断是服务器还是浏览器环境**,来决定使用xmlHttpRequest还是Node.js的http来创建请求，这个逻辑被叫做适配器 



```js
//源码 lib/defaults.js
function getDefaultAdapter(){
	var adapter;
	if(typeof XMLHttpRequest !=='undefined') {
		adapter = require('./adapter/xhr');
	}else if(typeof process !=='undefined' && Object.prototype.toString.call(process) === '[object process]'){
        adapter = require('./adapter/http');
    }
    return adapter
}
//对于 Node 环境的判断逻辑在我们做 ssr 服务端渲染的时候，也可以复用
```

Adapter xhr  axios对适配器的封装

```js
module.exports = function xhrAdapter(config){
	return new Promise(function dispatchXhrRequest(resolve,reject){
		var requestData = config.data;
        //创建xhr
        var request  = new XMLHttpRequest(); 
 //open启动请求        
        request.open(config.method.toUpperCase(),buildURL(fullPath,config.params,config.paramsSerializer),true);
        //监听xhr状态
 		request.onreadystatechange = function handleLoad(){}
        request.onabort = function handleAbort() {}
        request.onerror = function handleError() {}
        request.ontimeout = function handleTimeout(){}
        // 发送请求
        request.send(requestData)
	})
}
```

其实就是XMLHTTPRequest使用方法  

## Fetch

fetch号称AJAX的替代品   Fetch是基于promise设计的 Fetch的代码结构比起ajax简单多了 但**fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象**。

1. 语法简洁，更加语义化 

2. 基于标准 Promise 实现，支持 async/await

   3.同构方便，使用 [isomorphic-fetch](https://github.com/matthew-andrews/isomorphic-fetch) 

   4.更加底层，提供的API丰富（request, response） 

   5.脱离了XHR，是ES规范里新的实现方式

```
1）fetch只对网络请求报错，对400，500都当做成功的请求，服务器返回 400，500 错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject。
2）fetch默认不会带cookie，需要添加配置项： fetch(url, {credentials: 'include'})
3）fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程 继续在后台运行，造成了流量的浪费
4）fetch没有办法原生监测请求的进度，而XHR可以

```

**axios既提供了并发的封装，也没有fetch的各种问题，而且体积也较小，当之无愧现在最应该选用的请求的方式。**