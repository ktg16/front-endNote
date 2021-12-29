Node.js 

http://nodejs.cn/learn/reading-files-with-nodejs

## 什么是node.js?

node.js 是一个基于 Chrome V8 引擎的js运行环境

写一段代码放在node(基于 Chrome V8)执行 就是一段后端代码

浏览器执行的代码是前端代码

### node运行环境

1.v8引擎

2.内置api:  fs  path  http

3.node.js无法调用DOM和BOM等浏览器内置api

### node做什么

1. express框架    快速搭建web应用
2. electron  构建跨平台桌面应用
3. restify  构建api接口项目
4. 读写和操作数据库   

主要学习 ：js语法+node api + 第三方api

### fs文件系统模块(做服务端渲染时)

fs模块（内置api）是node 提供 用来操作文件的模块 他提供一系列方法属性 用来满足对文件的操作需求(安装node之后  fs自动存在)

[api](http://nodejs.cn/learn/the-nodejs-fs-module)

#### fs.readFile

```
const fs = require('fs')
fs.readFile(path[,options],callback) 读取文件内容
// 只要看见被[]包裹的  就是可选参数
path 必选参数，字符串 表示文件的路径
[,options] 可选参数 被[]包裹   以xx编码格式来读取
callback 必选参数 文件读取后可通过回调函数拿到读取的结果

示例:
fs.readFile('./react.txt','utf-8',function(err,datae){
    console.log(err)
    console.log('--------')
    console.log(datae)
})
同步版本
try {
  const data = fs.readFileSync('/Users/joe/test.txt', 'utf8')
  console.log(data)
} catch (err) {
  console.error(err)
}
```

#### fs.writeFile

写入文件内容

fs.writeFile(path, content[,options], callback())

```
fs.writeFile('./react.txt','utf8',function(err){
  if(err){
  return console.log(err)
  }
  // 文件写入成功
})
```

练习  - 整理考试成绩

小红=100  => 小红：100

1.导入fs文件系统模块

2.读取fs.readFile()

3.读取成功 处理数据  ， 使用fs.wirteFile()写入

#### __dirname 表示当前文件所处的目录

__dirname+'/files/1.txt'  不用动态拼接的那种方式了

### path路径模块

用来处理路径的模块

#### path.join（替换了+拼接号）

拼接多个路径片段

```
'../' 会抵消上一次路径

const name = 'joe'
require('path').join('/', 'users', name, 'notes.txt') //'/users/joe/notes.txt'
```

#### path.basename()

返回路径文件名  第二个参数可以过滤掉文件的扩展名

```
require('path').basename('/test/something') //something
require('path').basename('/test/something.txt') //something.txt
require('path').basename('/test/something.txt', '.txt') //something
```

#### path.extname()

获取文件扩展名

```
require('path').extname('/test/something/file.txt') // '.txt
```

### Http模块

http模块是 用来创建web服务器的模块。通过http模块提供的http.createServer()的方法 实现一台web服务器

```
const http = require('http')
```

http作用： 实现 Apache 第三方web服务器软件

相关概念  ip地址是互联网上每台计算机唯一地址

127.0.0.1用于服务器的测试

#### 创建服务器步骤

```
const http = require('http')

const server = http.createServer()
//给服务器绑定事件
//客户端请求server了
server.on('request',(req,res)=>{

console.log('回调')
})

server.listen(80,()=>{
  console.log('启动服务默认运行 http://127.0.0.1')
})
```

#### req请求对象

req 可以访问与客户端相关的数据或属性

前端通过 接口传递过来的一个数据或属性 通过req获得

#### res响应对象

向客户端响应一部分内容

```
res.end(str)
//向客户端发送指定的内容，并结束请求的处理过程
```

#### 解决中文乱码问题

使用res.setHeader('Content-Type','text/html; charset = utf-8')

```
res.setHeader('Content-Type','text/html; charset=utf-8') //必须是这样
```

设置Content-Type(内容类型)  ’text/html; charset = utf-8‘

#### 4.5根据不同的url返回不同的html内容

1.获取请求url地址

2.设置默认的响应数据

3.判断请求的router

4.res.end()

```
const http = require('http')

const server = http.createServer()
//给服务器绑定事件
//客户端请求server了
server.on('request',(req,res)=>{
const url =  req.url
let content = '找不到页面'
if(url == '/'||url=='/index.html'){
    content = '<h1>首页</h1>'
} else if(url == '/about.html'){
    content = '<h2>其他</h2>'
}
console.log('回调',req.url,req.method)
res.setHeader('Content-Type','text/html; charset=utf-8')
res.end(content)
})

server.listen(80,()=>{
  console.log('启动服务默认运行 http://127.0.0.1')
})
```

可以使用这种方法直接请求文件内容并响应客户端

```
const http = require('http')
const path = require('path')
const fs = require('fs')
const server = http.createServer()
//给服务器绑定事件
//客户端请求server了
server.on('request',(req,res)=>{
	//输入对应的url 如果觉得url复杂可以进行优化
    const url =  req.url
    let content = '找不到页面'
    const fpath = path.join(__dirname,url)
   fs.readFile(fpath,'utf-8',function(err,data){
       if(err) return console.log('读取失败')

       res.end(data)
   })
    console.log('回调',req.url,req.method)
    res.setHeader('Content-Type','text/html; charset=utf-8')
    // res.end(content)
})

server.listen(80,()=>{
  console.log('启动服务默认运行 http://127.0.0.1')
})
```

res.wirte('{ss:kk}') 将数据返回客户端



## 爬虫

使用http请求 

```
const https = require('https')
const http = require('http')
const cheerio = require('cheerio')
function filterData(data){
	//使用cheerio（dom操作） 把html拿过来
 let $ = cheerio.load(data)
    let $movieList = $('.movie-item')
    let movies = []
    $movieList.each((index, value) => {
      movies.push({
        title: $(value).find('.movie-title').attr('title'),
        score: $(value).find('.movie-score i').text(),
      })
    })

}



const server = http.createServe((req,res)=>{

https.get('https//www.meizu.com',(result)=>{
		let data = ''
		result.on('data',(chunk)=>{
			data = +chunk
		})
		result.on('end',()=>{
		filterData(data)
		})
})

})
```



## 模块化

## npm

[node基础](https://lurongtao.gitee.io/felixbooks-gp19-node.js/basics/01-Node.js%E5%9F%BA%E7%A1%80.html) 

npm xx -s  装在dependencies 生产

npm xx -D   就装在dev（开发）环境中

## Events

```js
const EventEmitter = require('events')

class MyEventEmitter extends EventEmitter {}

const event = new MyEventEmitter()
//定义一个事件
event.on('play', (movie) => {
  console.log(movie)
})
//触发事件
event.emit('play', '我和我的祖国')
event.emit('play', '中国机长')
```

## Zlib压缩模块

```js
const zlib = require('zlib');
```