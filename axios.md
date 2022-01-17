# 什么是axios?

Axios是一个基于promise的http库,可以用在浏览器和node.js中

## axios特性

- 从浏览器创建XMLHttpRequest
- 从node.js创建http请求
- 支持promise Api
- 拦截请求与响应
- 取消请求
- 自动装换JSON数据
- 支持客户端XSRF攻击 **跨站请求伪造**

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