runoob.com/ajax/ajax-xmlhttprequest-create.html

## Ajax

AJAX 是一种用于创建快速动态网页的技术。

通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。

工作原理

## ![AJAX](https://www.runoob.com/wp-content/uploads/2013/09/ajax-yl.png)

创建XMLHttpRequest对象

XMLHttpRequest 是 AJAX 的基础。

### 请求类型

get

```javascript
//写法
 xmlhttp.open("GET",url+'?user='+str+'&password='+str,true) //(请求类型,请求地址(+使用http传输内容),是否异步(async))
 xmlhttp.send() // 发送请求
```

post

- 不愿使用缓存文件（更新服务器上的文件或数据库）

- 向服务器发送大量数据（POST 没有数据量限制）

- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

  

  ```javascript
  //写法 // get方式不用设置，而post必须设置
  xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
  xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");// 设置请求头(header,value)
  xmlhttp.send("fname=Henry&lname=Ford"); // (传递的值)
  ```

delete

put

主要是进行修改数据时候使用

### onreadystatechange事件

readyState  存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

- 0: 请求未初始化
- 1: 服务器连接已建立
- 2: 请求已接收
- 3: 请求处理中
- 4: 请求已完成，且响应已就绪

status 200:'OK' / 404: 未找到页面

### Ajax实例

```javascript
function loadXMLDoc(){
	var  xmlhttp
    // 创建http请求
	if(window.XMLHttpRequest){
		xmlhttp = new XMLHttpRequest()
	}else{
		xmlhttp = new ActiveXObject("Microsoft.XMLHTTP")
	}
	xmlhttp.onreadystatechange = function(){   // 响应事件 每当 readyState 改变时，就会触发 onreadystatechange 事件
		if(xmlhttp.readyState ==4 && xmlhttp.status ==200){
			console.log(xmlhttp.responseText) // 'get'响应返回的数据
		}
	}
    xmlhttp.open("GET",url,true) //(请求类型,请求地址,是否异步(async))
    xmlhttp.send() // 发送请求
}
```

### **xmlhttp.status的值及解释：**

100——客户必须继续发出请求

101——客户要求服务器根据请求转换HTTP协议版本

200——交易成功

201——提示知道新文件的URL

202——接受和处理、但处理未完成

203——返回信息不确定或不完整

204——请求收到，但返回信息为空

205——服务器完成了请求，用户代理必须复位当前已经浏览过的文件

206——服务器已经完成了部分用户的GET请求

300——请求的资源可在多处得到

301——删除请求数据

302——在其他地址发现了请求数据

303——建议客户访问其他URL或访问方式

304——客户端已经执行了GET，但文件未变化

305——请求的资源必须从服务器指定的地址得到

306——前一版本HTTP中使用的代码，现行版本中不再使用

307——申明请求的资源临时性删除

400——错误请求，如语法错误

401——请求授权失败

402——保留有效ChargeTo头响应

403——请求不允许

404——没有发现文件、查询或URl

405——用户在Request-Line字段定义的方法不允许

406——根据用户发送的Accept拖，请求资源不可访问

407——类似401，用户必须首先在代理服务器上得到授权

408——客户端没有在用户指定的饿时间内完成请求

409——对当前资源状态，请求不能完成

410——服务器上不再有此资源且无进一步的参考地址

411——服务器拒绝用户定义的Content-Length属性请求

412——一个或多个请求头字段在当前请求中错误

413——请求的资源大于服务器允许的大小

414——请求的资源URL长于服务器允许的长度

415——请求资源不支持请求项目格式

416——请求中包含Range请求头字段，在当前请求资源范围内没有range指示值，请求也不包含If-Range请求头字段

417——服务器不满足请求Expect头字段指定的期望值，如果是代理服务器，可能是下一级服务器不能满足请求

**合起来**

500——服务器产生内部错误

501——服务器不支持请求的函数

502——服务器暂时不可用，有时是为了防止发生系统过载

503——服务器过载或暂停维修

504——关口过载，服务器使用另一个关口或服务来响应用户，等待时间设定值较长

505——服务器不支持或拒绝支请求头中指定的HTTP版本

1xx:信息响应类，表示接收到请求并且继续处理

2xx:处理成功响应类，表示动作被成功接收、理解和接受

3xx:重定向响应类，为了完成指定的动作，必须接受进一步处理

4xx:客户端错误，客户请求包含语法错误或者是不能正确执行

5xx:服务端错误，服务器不能正确执行一个正确的请求

**xmlhttp.readyState==4 && xmlhttp.status==200**的解释：请求完成并且成功返回