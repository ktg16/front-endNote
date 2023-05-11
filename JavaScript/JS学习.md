# JS学习Object的方法

勤看勤用勤记录

js是异步执行的

## Object的方法

### Object.create()

**`Object.create(fn)`**方法创建一个新对象，使用现有的对象(fn)来提供新创建的对象(newFn)的__proto__。 新创建的对象

 newFn =  Object.create(fn)   newFn.__proto__ = fn 

### Object.value (obj)

将传入的值装换为 数组形式 类似于for循环

返回值 一个包含对象自身的所有可**枚举**(类似循环 一个一个举出来)属性值的数组。[]

示例

```
var obj ={ foo:'bar',baz:42 }
console.log(Object.value(obj)) // [bar,42]

//属性的顺序与通过手动循环对象的属性值所给出的顺序相同。

var an_obj={100:'a',2:'b',9:'c'} //[b,c,a]

Object.values('foo') // ['f','o','o']
```

Object.hasOwnProperty(props)

表示是否有自己的属性

这个方法会查找一个对象是否有某个属性  但是不会去查找它的原型链

```javascript
var  obj = {
	a:1,
	fn:function(){},
	c:{
		d:{}
	}
}
console.log(obj.hasOwnProperty(a)) //true
```



## js 新增方法

### reduce

arr.reduce(function(prev,cur,index,arr){

},int)

arr 表示原数组

prev 表示上一次调用**回调的返回值**，或者**初始值int**；

cur 表示当前正在处理的数组**元素**

index表示 当前正在处理的数组元素的**索引** 提供 int 值，则索引为0，否则索引为1；

常用的只有prev和cur

var sum= arr.reduce(function(prev,cur){

return prev+cur  求数组项数和  pre为上一次返回的（prev+cur）

}，0)

### flat()方法 

可以将多维数组降维  传的参数是多少就降多少维

var a = [1, 2, 5, [7, 8, [99]]];

console.log(a.flat()); //[ 1, 2, 5, 7, 8, [ 99 ] ]

不传参默认为降维1

Math.max

### **switch 用法**

switch(index){

case 0: //判断index是否为0

​	this.currentType =POP;

​	break;

case 1:

​	this.currentType = New;

​	break

case 2:

​	break

}



### Set方法

 对数组进行去重

[...new Set(arr)]



### sort

sort 对数组进行排序

let arr = []

arr.sort((a,b)=>{

return a-b //为升序 b-a为降序

})

函数防抖在一定时间内再次触发，清除等待时间 重新记录等待时间

函数节流 在一定时间内再次触发 不会有任何操作  等待时间一过清空定时器

### 什么是纯函数？

如果函数的调用参数相同，则永远返回相同的结果。

它不依赖于程序执行期间函数外部任何状态或数据的变化，**必须只依赖于其输入参数**。

# js基本方法

## 1.Array.from() 将两类对象转换为真正的数组

 参数1转化为数组  

参数2可选  类似数组的map方法，对每个元素进行处理，将处理后的值放入返回的数组。

 第三个参数(可选): 用来绑定this。

## 2.**改变原数组的方法**(9个):

   let a = [1,2,3];

   ES5:

   a.splice()/ a.sort() / a.pop()/ a.shift()/  a.push()/ a.unshift()/ a.reverse()

  ES6:

   a.copyWithin() / a.fill

### 1.splice 添加/删除数组的元素

array.splice(index,howmany,item1,.....,itemX)

1. index：必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
2. howmany：可选。要删除的项目数量。如果设置为 0，则不会删除项目。
3. item1, ..., itemX： 可选。向数组添加的新项目。

返回值: 如果有元素被删除,返回值为被删除元素的新数组。

```
[4,5,6,7]
删除元素
let item = a.splice(-1, 3); // [7]  
  // 从最后一个元素开始删除3个元素，因为最后一个元素，所以只删除了7
添加元素 
a.splice(0,3,'添加')  //[1,2,3]
a = [7,'添加']
不删除只添加
a.splice(0,0,'添加')//在最前面添加
a= [添加,4,5,6,7]
```

### 2.sort排序 b是前面的数

```
sort有限制需要借助回调函数
升序降序
var array =  [10, 1, 3, 4,20,4,25,8];
 // 升序 a-b < 0   a将排到b的前面，按照a的大小来排序的 
 // 比如被减数a是10，减数是20  10-20 < 0   被减数a(10)在减数b(20)前面   
 array.sort(function(a,b){
   return a-b; //  >0时 b在a前面
 });
 console.log(array); // [1,3,4,4,8,10,20,25];
 // 降序 被减数和减数调换了  20-10>0 被减数b(20)在减数a(10)的前面
 array.sort(function(a,b){
   return b-a;  <0 就倒过来
 });
 console.log(array); // [25,20,10,8,4,4,3,1];


a为后面的数  b为前面的数



 var array = [{name:'Koro1'},{name:'Koro1'},{name:'OB'},{name:'Koro1'},{name:'OB'},{name:'OB'}];
    array.sort(function(a,b){
        if(a.name === 'Koro1'){// 如果name是'Koro1' 返回-1 ，-1<0 a排在b的前面
            return -1
        }else{ // 如果不是的话，a排在b的后面
          return 1
        }
    })
    // [{"name":"Koro1"},{"name":"Koro1"},{"name":"Koro1"},{"name":"OB"},{"name":"OB"},{"name":"OB"}] 

```

### pop() 删除一个数组中的最后的一个元素

```
let  a =  [1,2,3];
let item = a.pop();  // 3
```

### push() 向数组的末尾添加元素

```
let a = [1,2,3]

 a.push('1') 
```



### unshift() 向开头添加元素

```
let a = [1,2,3]

 a.unshift('1') 
```

## 不改变原数组

- reverse（将数组反转）

```
var a = [1,2,3]

var result = arr.reverse();//[3,2,1]
```

- join（根据条件对数组组合成字符串）、

```
var a = [1,2,3]

var result = arr.join(',') //123
```

# 数组方法

## Array.from 方法

```
类似于 []但永不完全是
let str = Array.from("RUNOOB") //['R','U','N','O','O','B']
Array.from(...set([1,1,1,55,66]))
```

## fill方法

```javascript
定义一个 Array() 使用 fill 进行填充
let arr =  Array(5).fill(2) //[ 2, 2, 2, 2, 2 ]
```



## flat()方法 

```js
arr.flat() //传的参数是多少就降多少维
```

## flatMap()方法 

```js
flatMap()方法对原数组的每个成员执行一个函数（相当于执行Array.prototype.map()）
arr.flatMap((item,index,arr)=> item) //将里面的item各项执行一次flat  可以在里面操作flat
```



## findindex 

```js
var arr=[20,31,22,23,24]

arr.findindex(20) // 0 返回下标
arr.findindex(110) // -1 数组中没有该值
```

## filter

```
let a =  arr.filter((item)=>{return item > 18}) 返回过滤的数组
```

## find

```
let a = arr.find((item)=> (item > 18 ) ) //返回当前item值 找到符合的值之后不会再执行
```

## some

```
let a = arr.some((item,index,arr)=> (item > 18 ) ) //返回值为 boolean类型,表达式为true则不会继续执行 与find类似
```

😃

## map

返回一个数组

```
let a = arr.map((item,index,arr)=>{},this(当前this传递给回调函数)) // 返回一个新的数组
另一种用法

arr.map(Number)// 放进去一个函数
arr.map(Math.sqrt)
```



# 字符串方法

## toString

```
let arr = [1,2,3,4,5]
arr.toString() //返回一个字符串对象 '1,2,3,4,5'
```

## split

```
// 以(第一个参数)将字符串变为数组
arr.toString().split(',',5) // 以，分割成数组，限制数组的长度
```



# Object对象方法

# 遍历方法总结

while性能 > for循环 > forEach

for xx in 

for of

while

```
while(//相当于判断 true实现 false跳过){
}
```

map

forEach

filter



# Es6 

## Commonjs 模块化

模块化方案  将每个文件看做一个模块，其他方式是以编程方式声明模块

导入依赖依据require函数调用实现的。函数调用是同步的   会返回所请求模块暴露的接口



```js
function union(){
 return 123456
}

function update(){
    console.log('update')
}

module.exports = union  //暴露union函数  union.js
//2 另一种方式
module.exports = {union,update}
// 3 
exports.union = union
const union = require('./union.js') // 引入
console.log(union())
//../router_handler/userinfo
exports.getUserInfo = (req, res) => { res.send('ok') }

const userinfo_handler = require('../router_handler/userinfo')

```

## export与import

https://es6.ruanyifeng.com/#docs/module#export-%E5%91%BD%E4%BB%A4

```javascript
1.命名导出  导出列表
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
//等价于  优先考虑下方写法
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export { firstName, lastName, year };
//使用这种方式引入
import { firstName, lastName, year } from './circle';
import * as circle from './circle';
circle.year
//也可以输出函数或类
export function multiply(x, y) {
  return x * y;
};

//export输出的变量就是本来的名字，但是可以使用as关键字重命名。
function v1() { ... }
function v2() { ... }
//使用as关键字重命名
export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
//正确写法               
export var m = 1; 或者  export {m}
// 报错
var m = 1;
export m;
//因为没有提供对外的接口。第一种写法直接输出 1，第二种写法通过变量m，还是直接输出 1。1只是一个值，不是接口。               
               
```

2.导出默认绑定 及引入

从前面的例子可以看出，使用`import`命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。

需要使用export default命令 为模块指定默认输出

```javascript
export default function () {   // 把函数定义在default
  console.log('foo');
}
//导入
import customName from './export-default';
customName(); // 'foo'



```

export 与 export default区别  export导出 需要import { }引入

> export default**命令用于指定模块的默认输出**。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能唯一对应export default命令。

```javascript
//本质上，export default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字。

// modules.js
function add(x, y) {
  return x * y;
}
export {add as default};
// 等同于
// export default add;

// app.js
import { default as foo } from 'modules';
// 等同于
// import foo from 'modules';

//app.js
export default {
	function a(){},

	function b(){}
}

import c from 'app.js'
c.a()
c.b()
```

正是因为`export default`命令其实只是输出一个叫做`default`的变量，所以它后面不能跟变量声明语句。

