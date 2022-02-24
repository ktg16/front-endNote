路径 C:\Users\Administrator\Desktop\证件

## 1.1新建项目

 1. 新建项目目录

    ```
    npm init -y
    -y 的含义：yes的意思，在init的时候省去了敲回车的步骤，生成的默认的package.json
    ```

    

 2. 安装express

    ```
    npm i express@4.17.1
    ```

    

 3. 根目录新建app.js

    ```
    const cors = require('cors')
    const app =  require('express')()
    
    app.listen(3007,()=>{
    	console.log('project running at http:127.0.0.1:3007')
    })
    
    
    ```

 4. 配置cors跨域

    1.安装cors中间件

    2.在app.js导入配置cors中间件
    
    3.配置表单数据的中间件

```
const cors = require('cors')
app.use(cors) // 解决跨域问题
```

1.4初始化路由相关的文件夹

1.5初始化用户路由模块

```js
//user.js
const express  = require('express')
const router = express.Router()
// 注册新用户
router.post('/reguster',(req,res)=>{
	res.send('ok')
})
module.exports = router
//app.js
//在app.js 注册才可以使用
const userRouter = require('xxx')
app.use('/api',userRouter) //在这里我们有个前缀所以需要这样使用
```

1.6抽离路由模块化

```js
// router_hander.js/user.js
exports.regUser = (req,res)=>{
res.send('ok')
}
//user.js
const user_handler  = require('../router_hander.js/user.js')

router.post('/reguster',user_handler.regUser)
```

## 2.登录注册

2.1.新建ev_users表

### 2.2安装mysql模块并配置

npm i mysql@2.18.1

新建db文件夹

2.3判断表单数据

```
const userInfo = req.body   //获取前端传递的信息
if(!userInfo.username||!userInfo.password){
	return res.send({status:-1,message:'用户名或密码不合法'})
}
```

2.4  导入数据库   检测用户名是否被占用

```js
const db = require('../db/index')
//定义sql语句 查询用户名是否被占用


exports.regUser = (req,res)=>{

const userInfo = req.body   //获取前端传递的信息
if(!userInfo.username||!userInfo.password){
	return res.send({status:-1,message:'用户名或密码不合法'})
}
const sqlStr = 'select * from xx(ev_users) where username=? '
db.query(sqlStr,userInfo.username,(err,results)=>{

	if(err){
		return res.send({status:-1})
	}
	if(results.length>0){
	   return res.send({status:-1,message:'用户名被占用'}) 
	}
	// 用户名可以使用 继续后面的流程
    2.3.3(此处)
})
res.send('ok')
}

```

2.3.3加密密码 处理存入表中

 1.使用 bcrypt.js 进行加密 

```
npm i bcrypt.js@2.4.3 //加密
```

2.在  /router_handler/user.js  导入bcrypt.js

cosnt bcrypt = require('bcryptjs')

3. 在注册用户的处理函数中，确认用户名可用之后，调用 bcrypt.hashSync(明文密码, 随机的 长度) 方法，对用户的密码进行加密处理：

```
// 对用户的密码,进行 bcrype 加密，返回值是加密之后的密码字符串 userinfo.password = bcrypt.hashSync(userinfo.password, 10)
```

2.3.4 插入新用户

 	得到加密后的密码就可以实现插入用户了

​	1.定义插入用户的sql语句

​		const sql = ‘ insert into ev_users set ?’

​	2.调用 db.query() 执行 SQL 语句，插入新用户：

```
db.query(sql,{username:userInfo.username,password:userInfo.password},
    function(err,results){
		if(err) return res.send({status:1,message:err.message})
		if(result.affectedRows !==1 ){
		 return res.send({status:1,message:'注册用户失败，请稍后再试'})
		 res.send({status:0,message:'注册成功!'})
		}
	}
)
```

2.4优化res.send代码

​	多次调用res.send() 向客户端响应 处理失败 的结果，为了简化代码，

可以手动封装一个 res.cc() 函数：

1. 在 app.js 中，所有路由之前，声明一个全局中间件，为 res 对象挂载一个 res.cc() 函数 ：

```js
// 响应数据的中间件
app.use(function (req, res, next) { 
// status = 0 为成功； status = 1 为失败； 默认将 status 的值设置为 1，方便处理失败的情 况 
	res.cc = function (err, status = 1) { 
	res.send({ 
	// 状态 status, // 状态描述，判断 err 是 错误对象 还是 字符串 
        message: err instanceof Error ? err.message : err, }) }
	next()})
```

2.5优化表单验证

单纯的使用 if...else... 的形式对数据合法性进行验证，效率低下、出错率高、维护性差。因此，

推荐使用**第三方数据验证模块**，来降低出错率、提高验证的效率与可维护性，**让后端程序员把更多的精力放在核心业务逻辑的处理上**

1.安装 @hapi/joi 包，为表单中携带的每个数据项，定义验证规则：

```
npm install @hapi/joi@17.1.0
```

2.安装 @escook/express-joi 中间件, 来实现自动对表单数据进行验证的功能:

```
npm i @escook/express-joi
```

3.新建 /schema/user.js 用户信息验证规则模块，并初始化代码如下：





2.6登录

\1. 检测表单数据是否合法

\2. 根据用户名查询用户的数据

\3. 判断用户输入的密码是否正确

\4. 生成 JWT 的 Token 字符串

2.6.1检测表单数据合法  使用

const expressJoi = require('@escook/express-joi')

2.6.2根据用户名查询用户的数据

```
const userinfo = req.body

const sql = 'select * from ev_users where username=?'

db.query(sql,userInfo.usename,function(err,results){
	if(err)
	if(results.length!==1)
	//2.6.3判断输入的密码是否正确
})
```

2.6.3判断用户输入的密码是否正确

```
// 拿着用户输入的密码,和数据库中存储的密码进行对比 c
onst compareResult = bcrypt.compareSync(userinfo.password, results[0].password) 
// 如果对比的结果等于 false, 则证明用户输入的密码错误 
if (!compareResult) { return res.cc('登录失败！') }
// TODO：登录成功，生成 Token 字符串
```

2.6.4生成JWT的Token字符串

```
npm i jsonwebtoken@8.5.1 //安装生成Token字符串的包
```

2.7配置解析 Token中间件

```
npm i express-jwt@5.3.3  //安装解析Token的中间件
```

## 3.个人中心

3.1获取用户基本信息

3.1.0 获取基本信息实现步骤

	1. 初始化路由模块(基础接口)
	2. 路由处理函数  通过前端传递过来的数据进行查表
	3. 获取用户的基本信息

3.1.1 初始化路由模块

​	1.创建路由模块 新建文件 /router/userinfo.js 路由模块

```
const express = require('express')

const router = express.Router()
//get 请求
router.get('/userInfo',(req,res)=>{
	res.send('ok')
})

//暴露出去
module.exports = router
```

2.app.js 引入

3.1.2初始化路由处理函数

3.1.3获取用户基本信息

与前面类型 写sql语句 处理数据 判断

3.2更新用户数据

​	步骤

​	1.实现路由

​	2.验证表单数据 （依据joi）

​	3.实现更新用户基本信息的功能



```
expressJoi(update_userinfo_schema)//使用验证规则对象
router.post('/userinfo', expressJoi(update_userinfo_schema), userinfo_handler.updateUserInfo)
```

3.3重置密码

​	1.定义路由 处理函数

​	2.验证表单数据

​	3.重置密码

​		1.查询密码是否存在

```js
const sql = `select * from ev_users' where id=?`

db.query(sql , req.user.id ,(err,result)=>{
xxx
	//判断密码是否正确
	const compareResult = bcrypt.compareSync(req.body.oldPwd, results[0].password) 
	if (!compareResult) return res.cc('原密码错误！')
	//设置新密码
})
```

