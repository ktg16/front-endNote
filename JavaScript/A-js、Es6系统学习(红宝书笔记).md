
ps：本文有链接，翻版的永不如官方的解释清楚 。（如有不理解本人会另外用通俗语言解释。个人不熟悉的知识也将重复记录） 

昨天的已成为过去 明天的还未到来

产生跨域的原理是：ajax引擎，把返回给浏览器的数据挡在了外面

设置个代理 （中间人与浏览器同源、没有ajax引擎）

浏览器中的JavaScript有 Js核心语法、 WebApi



浏览器运行环境(代码正常运行所需的必要环境)

1.各浏览器存在不同的引擎(谷歌V8)来解析和执行js代码

2.内置webApi是由运行环境提供的特殊接口  只能在所属环境中被调用

# JavaScript 数据类型和数据结构

## [动态类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#动态类型)

JavaScript 是一种**弱类型**或者说**动态**语言。这意味着你不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。这也意味着你可以使用同一个变量保存不同类型的数据：

var foo = 42；

foo= 'basic'

foo = true



## [数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#数据类型)

基本数据类型

- [undefined](https://developer.mozilla.org/zh-CN/docs/Glossary/undefined)：`typeof instance === "undefined"`
- [Boolean](https://developer.mozilla.org/zh-CN/docs/Glossary/Boolean)：`typeof instance === "boolean"`
- [Number](https://developer.mozilla.org/zh-CN/docs/Glossary/Number)：`typeof instance === "number"`
- [String](https://developer.mozilla.org/zh-CN/docs/Glossary/String)：`typeof instance === "string`
- [BigInt](https://developer.mozilla.org/zh-CN/docs/Glossary/BigInt)：`typeof instance === "bigint"`
- [Symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) ：`typeof instance === "symbol"`   表示值为符号 （常用作 symbol）
- [null](https://developer.mozilla.org/zh-CN/docs/Glossary/Null)：`typeof instance === "object"`。

复杂数据类型

Object Array



## 判断类型方式（typeof）

使用方法

var instance(例子)

`typeof  instance`

### instanceof（常判断具体类型）

（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof） **运算符**用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。



```
var instance = {}
instance instanceof Object(构造函数)
```



### typeof  (原始类型除了null都可以判断)

只能判断基本数据类型

对一个值使用type of 操作符会返回下列字符之一

❑"undefined"表示值未定义；

❑ "boolean"表示值为布尔值；

❑ "string"表示值为字符串；

❑ "number"表示值为数值；

❑ "object"表示值为对象（而不是函数）或null；

❑ "function"表示值为函数；❑ "symbol"表示值为符号。

type of '类型'  string

type of 95 number

typeof null "object"

### Object.prototype.toString（类型判断最佳类型）

```js
//语法
obj.toString()
返回值 一个表示该对象的字符串
可以自定义一个方法，来取代默认的 toString() 方法。该 toString() 方法不能传入参数，并且必须返回一个字符串。
var toString = Object.prototype.toString;
// 使用toString检测对象类型
toString.call(new Date); // [object Date]
toString.call(new String); // [object String]
```



### 2.isXXX 例如 `isArray` 方法

**Array.isArray()** 用于确定传递的值是否是一个 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)。

```
Array.isArray(obj)

返回值：值是Array 返回true 反之为false
```
```js
```
### Array.prototype.isPrototypeOf（arr）

返回值为true

## 变量（let var const）

let声明的范围是块作用域，而var声明的范围是函数作用域。

#### 暂时性死区 let

在解析代码时，JavaScript引擎也会注意出现在块后面的let声明，只不过在此之前不能以任何方式来引用未声明的变量。在let声明之前的执行瞬间被称为“暂时性死区”（temporaldead zone），在此阶段引用任何后面才声明的变量都会抛出ReferenceError。

#### const

它声明变量时必须同时初始化变量，且尝试修改const声明的变量会导致运行时错误。

const声明的限制只适用于它指向的变量的引用。换句话说，如果const变量引用的是一个对象，那么修改这个对象内部的属性并不违反const的限制

## 类型转换

https://github.com/mqyqingfeng/Blog/issues/159

## null 类型

null值表示一个空对象指针，这也是给typeof传一个null会返回"object"的原因：

```javascript
let cat = null
console.log(typeof cat) //'object'
```



## Set、Map

### set基本法

ES6提供了新的数据结构 Set 。 类似数组，但其成员值都是唯一的(没有重复的值)

```js
const set = new Set([1,2,3,4,4]) 
//1,2,3,4
[...newSet([1,2,3,4,4,4,])] 
// 去重
```

Set内部不会发生类型转换,5和‘5’是两个不同的值

其原因是使用的算法是“Same-value-zero equality”,类似于精确相等运算符(===),主要的区别是向Set 加入值认为NaN等于,自身而精确相等运算符认为`NaN`不等于自身。

```
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b)
set // Set {NaN}
```

### Set实例的属性和方法

 Set.prototype.size: 返回Set实例的成员 总数

Set.prototype.add(val):添加某个值 （返回的是Set结构本身）

Set.prototype.delete(val):删除某值

Set.prototype.has(val):返回一个布尔值,表示值是否为Set的成员

Set.prototype.clear():清除所有成员  无返回值

```javascript
s.add(1).add(2).add(2);
// 注意2被加入了两次

s.size // 2

s.has(1) // true
s.has(2) // true
s.has(3) // false
if(s.has(3)) //使用这种方法判断3是否存在
s.delete(2);
s.has(2) // false
```

遍历方法

我一般使用for  of或者forEach/[...set] (或者解构为[])

### WeakSet 弱集合

WeakSet中的“weak”（弱），描述的是JavaScript垃圾回收程序对待“弱集合”中值的方式。

WeakSet 的成员只能是对象，而不能是其他类型的值。

WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

### Map含义/基本用法(重点介绍)

​	*JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。*

```javascript
const data = {};
const element = document.getElementById('myDiv');

data[element] = 'metadata';
data['[object HTMLDivElement]'] // "metadata"
```

为了解决问题ES6提供了Map数据结构 

**由上可见,Map类似于对象也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。**

```javascript
const m = new Map();
const o = {p: 'Hello World'};
//把对象o当做键
m.set(o, 'content') //设置/添加键值对
m.get(o) // "content" //读取

m.has(o) // true    // 判断是否存在
m.delete(o) // true //删除键
m.has(o) // false
```

*事实上，不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作`Map`构造函数的参数。这就是说，`Set`和`Map`都可以用来生成新的 Map。*

```javascript
const items = [
  ['name', '张三'],
  ['title', 'Author']
];

const map = new Map();

items.forEach(
  ([key, value]) => map.set(key, value)
);
const m2 = new Map([['baz', 3]]);
const m3 = new Map(m2);
m3.get('baz') //3
```

```javascript
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```

上面代码的`set`和`get`方法，表面是针对同一个键，**但实际上这是两个不同的数组实例，内存地址是不一样的**，因此`get`方法无法读取该键，返回`undefined`。(有疑惑看下面部分)

同理，同样的值的两个实例，在 Map 结构中被视为两个键。

```javascript
const map = new Map();

const k1 = ['a'];
const k2 = ['a'];

map
.set(k1, 111)
.set(k2, 222);

map.get(k1) // 111
map.get(k2) // 222
```

Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。**这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，**就不用担心自己的属性与原作者的属性同名。

如果Map的键是一个简单的类型的值(数字、字符、布尔值)只要两个值严格相等，Map 将其视为一个键，比如**`0`和`-0`就是一个键**，**布尔值`true`和字符串`true`则是两个不同的键**。另外，**`undefined`和`null`也是两个不同的键**。虽然**`NaN`不严格相等于自身**（与Set一样，不区分NAN)，但 Map 将其视为同一个键。

### Map实例的属性及用法

size

map.set(key,value)

```javascript
//返回当前的map 可使用链式写法
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```

map.get

map.has

map.delete

map.clear

最常用的一种（map最常使用的场景）

```
let a = [1,2,3,4,5]
let map = new Map()
for(let i=0;i<a.len;i++){
	map.set(a[i],i)
}
map.forEach((value,key)=>{
	console.log(value)
})
```

遍历方法 如果不会的时候查看

```javascript
for (let [key, value] of map) {
  console.log(key, value);
} //常使用
```

https://es6.ruanyifeng.com/#docs/set-map#%E9%81%8D%E5%8E%86%E6%96%B9%E6%B3%95

### WeakMap 弱映射

“weak”（弱），描述的是JavaScript垃圾回收程序对待“弱映射”中值的方式。

键必须是对象 {}

## this 绑定

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this

https://segmentfault.com/a/1190000011194676   思否文章

😎首先对this下个定义：**this是在执行上下文创建时确定的一个在执行过程中不可更改的变量。**

所谓**执行上下文**，就是JavaScript引擎在执行一段代码之前将代码内部会用到的一些**变量**、**函数**、**this**提前声明然后保存在变量对象中的过程。

this绑定优先级

```haxe
new 绑定 > 显示绑定 > 隐式绑定 > 默认绑定
```

在绝大多数情况下，函数的调用方式决定了 `this` 的值（运行时绑定）

无论是否在严格模式下，在全局执行环境中（在任何函数体外部）`this` 都指向全局对象

```
console.log(this === window); // true
a = 37 
console.log(window.a) //37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

因为下面的代码不在严格模式下，且 `this` 的值不是由该调用设置的，所以 `this` 的值默认指向全局对象

```
function f1(){
  return this;
}
//在浏览器中：
f1() === window;   //在浏览器中，全局对象是window
//在Node中：
f1() === globalThis;
```

### [函数上下文中的 this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this#函数上下文中的_this)

```javaScript
// 对象可以作为 bind 或 apply 的第一个参数传递，并且该参数将绑定到该对象。
var obj = {a: 'Custom'};

// 声明一个变量，并将该变量作为全局对象 window 的属性。
var a = 'Global';

function whatsThis() {
  return this.a;  // this 的值取决于函数被调用的方式
}

whatsThis();          // 'Global' 因为在这个函数中 this 没有被设定，所以它默认为 全局/ window 对象
whatsThis.call(obj);  // 'Custom' 因为函数中的 this 被设置为obj
whatsThis.apply(obj); // 'Custom' 因为函数中的 this 被设置为obj
```

### [this 和对象转换](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this#this_和对象转换)

setTimeout会改变this的指向

```javascript
function foo() {
	console.log(this.a)
}
var a = 1
foo()

var obj = {
	a: 2,
	foo: foo
}
obj.foo()

// 以上情况就是看函数是被谁调用，那么 `this` 就是谁，没有被对象调用，`this` 就是 `window`

// 以下情况是优先级最高的，`this` 只会绑定在 `c` 上，不会被任何方式修改 `this` 指向
var c = new foo()
c.a = 3
console.log(c.a)

// 还有种就是利用 call，apply，bind 改变 this，这个优先级仅次于 new
```

在[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)中，`this`与封闭词法环境的`this`保持一致。在全局代码中，它将被设置为全局对象：

```
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true
```

箭头函数

```
// 创建一个含有bar方法的obj对象，
// bar返回一个函数，
// 这个函数返回this，
// 这个返回的函数是以箭头函数创建的，
// 所以它的this被永久绑定到了它外层函数的this。
// bar的值可以在调用中设置，这反过来又设置了返回函数的值。
var obj = {
  bar: function() {
    var x = (() => this);
    return x;
  }
};

// 作为obj对象的一个方法来调用bar，把它的this绑定到obj。
// 将返回的函数的引用赋值给fn。
var fn = obj.bar();

// 直接调用fn而不设置this，
// 通常(即不使用箭头函数的情况)默认为全局对象
// 若在严格模式则为undefined
console.log(fn() === obj); // true

// 但是注意，如果你只是引用obj的方法，
// 而没有调用它
var fn2 = obj.bar;
// 那么调用箭头函数后，this指向window，因为它从 bar 继承了this。
console.log(fn2()() == window); // tru
```

如果函数是在某个 上下文对象 下被调用

```
   this绑定的是那个上下文对象，例 : var obj = { foo : foo };    obj.foo();  foo 中的 this 就是 obj . 这样的绑定方式叫 隐性绑定 .
```

## 闭包

```
闭包不是私有的，闭的意思不是封闭内部状态 ，而是‘封闭外部状态’ 一个函数如何能够封闭外部状态呢 当外部状态的scope失效的时候， 还有一份留在内部状态里面 
```

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures

一个函数和对其周围状态（**lexical environment，词法环境**）的引用捆绑在一起（或者说函数被引用包围），这样的组合就是**闭包**（**closure**）

也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用域。在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。

参考节流防抖 

特点   闭包允许将函数与其所操作的某些数据（环境）关联起来

```
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);
```

## Scope（作用域）

https://developer.mozilla.org/zh-CN/docs/Glossary/Scope

什么是作用域？

作用域可以理解为变量的可访问性，总共分为三种类型，分别为：

- 全局作用域
- 函数作用域
- 块级作用域，ES6 中的 `let`、`const` 就可以产生该作用域

什么是作用域链？

jS 到底是如何访问需要的变量或者函数的。 实体就是 [[Scopes]]

JS采用静态作用域（记忆）

因为 JavaScript 采用的是词法作用域，**函数的作用域在函数定义的时候就决定了。**（函数的作用域基于函数创建的位置。）**后续不会改变，和箭头函数中的this是一样的，js会一层一层往上寻找需要的内容**

而与词法作用域相对的是动态作用域，函数的作用域是在函数调用的时候才决定的。

```
var value = 1;

function foo() {
    console.log(value);
}

function bar() {
    var value = 2;
    foo();
}

bar();

假设JavaScript采用静态作用域，让我们分析下执行过程：

执行 foo 函数，先从 foo 函数内部查找是否有局部变量 value，如果没有，就根据书写的位置，查找上面一层的代码，也就是 value 等于 1，所以结果会打印 1。

假设JavaScript采用动态作用域，让我们分析下执行过程：

执行 foo 函数，依然是从 foo 函数内部查找是否有局部变量 value。如果没有，就从调用函数的作用域，也就是 bar 函数内部查找 value 变量，所以结果会打印 2。
```

## new

https://zhuanlan.zhihu.com/p/23987456 实现组合继承  （构造继承+原型链）

#### call、apply、bind

https://segmentfault.com/a/1190000018270750

#### 原型

https://github.com/febobo/web-interview/issues/59

https://jsgodroad.com/interview/js#%E5%8E%9F%E5%9E%8B   666

什么是原型？

原型是对象中的内置属性，其实就是对象其他属性的引用

几乎所有的对象在创建时会产生一个赋值的[[prototype]]属性 

什么是原型链？

原型链是一种关系

实例对象通过属性 `_proto_`查找其构造函数的属性或者方法

`__proto__`作为不同对象之间的桥梁，用来指向创建它的构造函数的原型对象的

[![img](https://camo.githubusercontent.com/10ba2b15ee90f7a8d9881431005ad5e9b004a740878fa7727e631e5597504400/68747470733a2f2f7374617469632e7675652d6a732e636f6d2f36613734323136302d373235652d313165622d616239302d6439616538313462323430642e706e67)](https://camo.githubusercontent.com/10ba2b15ee90f7a8d9881431005ad5e9b004a740878fa7727e631e5597504400/68747470733a2f2f7374617469632e7675652d6a732e636f6d2f36613734323136302d373235652d313165622d616239302d6439616538313462323430642e706e67)

每个对象的`__proto__`都是指向它的构造函数的原型对象`prototype`的（这个就叫做原型链）

```
person1.__proto__ === Person.prototype
```

构造函数是一个函数对象，是通过 `Function `构造器产生的

```
Person.__proto__ === Function.prototype
```

原型对象本身是一个普通对象，而普通对象的构造函数都是`Object`

```
Person.prototype.__proto__ === Object.prototype
```

刚刚上面说了，所有的构造器都是函数对象，函数对象都是 `Function `构造产生的

```
Object.__proto__ === Function.prototype
```

`Object `的原型对象也有`__proto__`属性指向`null`，`null`是原型链的顶端

```
Object.prototype.__proto__ === null
```

## Class

https://zhuanlan.zhihu.com/p/158956514

使用class

```text
class Person {
  constructor (name) {
    this.name = name
  }
  
  talk () {
    console.log(`${this.name} says hello`)
  }
}
非常接近于
function Person (name) {
  this.name = name
}
Person.prototype.talk = function () {
  console.log(`${this.name} says hello`)
}
执行代码时

const dwx  = new Preson('dwx')
const button ={}
button.onclick = dwx.talk() //可以执行
button.onclick = dwx.talk
button.onclick() // 输出 undefined says hello 原因是this被改变了

原因 this变为window上的this了而不是Preson里的this了

修改方式一 使用bind修改this指向 bind不会立即执行且参数只有一个

class Person {
  constructor (name) {
    this.name = name
    this.talk = this.talk.bind(this); // 在构造器里显式调用 bind 函数绑定 this
  }

  talk () {
    console.log(`${this.name} says hello`)
  }
}
方法二：
使用箭头函数 
使用类属性+箭头函数的方式来定义方法 
class Person {
  constructor(name) {
    this.name = name
  }

  talk = () => {
    console.log(`${this.name} says hello`)
  }
}
```

工厂函数替代class

```text
const PersonFactory = (name) => {
  return {
    talk: () => {
      console.log(`${name} says Hello`)
    }
  }
}//闭包特性
```

```text
工厂模式写接口

function httpClientFactory(baseUrl) {
  return {
    baseUrl: baseUrl,
    listUsers: () => {
      return axios.get(`${baseUrl}/users`)
    },
    getUser: (id) => {
      return axios.get(`${baseUrl}/users/${id}`)
    },
    createUser: (user) => {
      return axios.post(`${baseUrl}/users`, user);
    },
    listBooks: () => {
      return axios.get(`${baseUrl}/books`)
    },
    getBook: (bookName) => {
      return axios.get(`${baseUrl}/books/${bookName}`)
    },
    createBook: (book) => {
      return axios.post(`${baseUrl}/books`, book)
    }
  }
}

const httpClient = httpClientFactory("https://your-endpoints/api");
httpClient.getUser("123");
httpClient.getBook("JavaScript Is Interesting");
console.log("The httpClient's baseUrl is " + httpClient.baseUrl);
```

https://juejin.cn/post/6844904094079926286

### 静态方法

### super用法

1. super( ) 只能在constructor中使用不能够在其他地方使用

2.

```javascript
// 使用super调用父亲的方法
class A {
  constructor() {
    this.x = 1;
  }
  print() {
    console.log(this.x);
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
  }
  m() {
    super.print();
  }
}

let b = new B();
b.m() // 2
super.print()虽然调用的是A.prototype.print()，但是A.prototype.print()内部的this指向子类B的实例，导致输出的是2，而不是1。也就是说，实际上执行的是super.print.call(this)。
```

https://es6.ruanyifeng.com/#docs/class-extends#super-%E5%85%B3%E9%94%AE%E5%AD%97

## Promise

```javaScript
// promis写法 
let newPromise = new Promise((resolve, reject) => {

  setTimeout(() => {

​    resolve('成功了！') //成功输出 执行就会输出这个

​    reject('失败了')

  }, 500);

})



newPromise.then((res) => {

  return new Promise((resolve) => {

​    setTimeout(() => {

​      resolve(res + '之后再次成功')

​    }, 500)

  })

}).then(res => {

  console.log('结果' + res)

})

.catch((res) => {

  console.log('结果' + res)

})
```

*pending*等待 resolve成功 reject失败    方法

三种状态是  pending   fulfilled  rejected 

上述的代码promise链式调用解决了回调地狱( 一个异步请求套着一个异步请求，一个异步请求依赖于另一个的执行结果，使用回调的方式相互嵌套。)
### 实例方法
promise.protype.then()
Promise.protype.catch()
Promise.protype.finally() 指定不管 Promise 对象最后状态如何，都会执行的操作
### 静态方法
Promise.resolve
Promise.race
Promise.all 将多个 `Promise` 实例，包装成一个新的 `Promise` 实例
-   遇到执行回调中第一个失败。会立刻执行自身的`rejected`的回调函数，并且只会抛出第一个失败`rejected`，后续遇到`rejected`均不执行
    
-   不会因为内部异步函数的失败，而中断后续所有的异步函数执行
promise.any() 接受一组Promise实例作为参数   有一个成功就返回第一个 后续不返回，如果失败需要等到所有失败才会返回失败`Promise`
## Iterator 迭代器

https://es6.ruanyifeng.com/#docs/iterator

js原有表示‘集合’的结构  array、object 新增Map Set

作用：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令`for...of`循环，Iterator 接口主要供`for...of`消费。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的`next`方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的`next`方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的`next`方法，直到它指向数据结构的结束位置。

```javascript
var it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }

function makeIterator(array) {
  var nextIndex = 0;
  return {
    next: function() {
      return nextIndex < array.length ?
        {value: array[nextIndex++], done: false} :
        {value: undefined, done: true};
    }
  };
}
```

Iterator 接口的目的，就是为所有数据结构，提供了一种统一的访问机制`for...of`循环

原生具备Iterator接口的数据结构：（可直接使用for  in  遍历）

- Array
- Map
- Set
- String
- TypedArray
- 函数的 arguments 对象
- NodeList 对象

ES6 规定，默认的 Iterator 接口部署在数据结构的`Symbol.iterator`属性，或者说，一个数据结构只要具有`Symbol.iterator`属性，就可以认为是“可遍历的”

```javascript
const obj = {
  [Symbol.iterator] : function () {
    return {
      next: function () {
        return {
          value: 1,
          done: true
        };
      }
    };
  }
};
```

## Generator函数

https://es6.ruanyifeng.com/#docs/generator

Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）。

```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

调用 Generator 函数后，该函数并不执行，**返回的也不是函数运行结果，而是一个指向内部状态的指针对象**，也就是上一章介绍的遍历器对象（Iterator Object）。

```javascript
hw.next()
// { value: 'hello', done: false }

hw.next()
// { value: 'world', done: false }

hw.next()
// { value: 'ending', done: true }

hw.next()
// { value: undefined, done: true }
```

ES6 提供了`yield*`表达式，作为解决办法，用来在一个 Generator 函数里面执行另一个 Generator 函数。



## async函数

async函数是generator函数的语法糖

https://juejin.cn/post/6844904102053281806

async await 后面必须跟着promise的方法不然不会生效

利用 generator

```javascript
function* testG() {
  // await被编译成了yield
  const data = yield getData()
  console.log('data: ', data);
  const data2 = yield getData()
  console.log('data2: ', data2);
  return 'success'
}

```

generator函数不会自动执行需要使用 .next()执行  需要编写自动函数让这个generator函数实现async功能



```javaScript
const getData = () => new Promise(resolve => setTimeout(() => resolve("data"), 1000))
  
var test = asyncToGenerator(
    function* testG() {
      // await被编译成了yield
      const data = yield getData()
      console.log('data: ', data);
      const data2 = yield getData()
      console.log('data2: ', data2);
      return 'success'
    }
)

test().then(res => console.log(res))

```

```
asyncToGenerator`接受一个`generator`函数，返回一个`promise
=======
ps：本文有链接，翻版的永不如官方的解释清楚 。（如有不理解本人会另外用通俗语言解释。个人不熟悉的知识也将重复记录） 

昨天的已成为过去 明天的还未到来

产生跨域的原理是：ajax引擎，把返回给浏览器的数据挡在了外面

设置个代理 （中间人与浏览器同源、没有ajax引擎）

浏览器中的JavaScript有 Js核心语法、 WebApi



浏览器运行环境(代码正常运行所需的必要环境)

1.各浏览器存在不同的引擎(谷歌V8)来解析和执行js代码

2.内置webApi是由运行环境提供的特殊接口  只能在所属环境中被调用

# JavaScript 数据类型和数据结构

## [动态类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#动态类型)

JavaScript 是一种**弱类型**或者说**动态**语言。这意味着你不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。这也意味着你可以使用同一个变量保存不同类型的数据：

var foo = 42；

foo= 'basic'

foo = true



## [数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#数据类型)

基本数据类型

- [undefined](https://developer.mozilla.org/zh-CN/docs/Glossary/undefined)：`typeof instance === "undefined"`
- [Boolean](https://developer.mozilla.org/zh-CN/docs/Glossary/Boolean)：`typeof instance === "boolean"`
- [Number](https://developer.mozilla.org/zh-CN/docs/Glossary/Number)：`typeof instance === "number"`
- [String](https://developer.mozilla.org/zh-CN/docs/Glossary/String)：`typeof instance === "string`
- [BigInt](https://developer.mozilla.org/zh-CN/docs/Glossary/BigInt)：`typeof instance === "bigint"`
- [Symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) ：`typeof instance === "symbol"`
- [null](https://developer.mozilla.org/zh-CN/docs/Glossary/Null)：`typeof instance === "object"`。

复杂数据类型

Object Array



## 判断类型方式（typeof）

使用方法

var instance(例子)

`typeof  instance`

instanceof（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof） **运算符**用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。

`instance instanceof Object`

Object.prototype.toString

​```js
//语法
obj.toString()
返回值 一个表示该对象的字符串
可以自定义一个方法，来取代默认的 toString() 方法。该 toString() 方法不能传入参数，并且必须返回一个字符串。
var toString = Object.prototype.toString;
// 使用toString检测对象类型
toString.call(new Date); // [object Date]
toString.call(new String); // [object String]
```



2.isXXX 例如 `isArray` 方法

**Array.isArray()** 用于确定传递的值是否是一个 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)。

```
Array.isArray(obj)

返回值：值是Array 返回true 反之为false
```

## 类型转换

https://github.com/mqyqingfeng/Blog/issues/159

## Set、Map

### set基本法

ES6提供了新的数据结构 Set 。 类似数组，但其成员值都是唯一的(没有重复的值)

```js
const set = new Set([1,2,3,4,4]) 
//1,2,3,4
[...newSet([1,2,3,4,4,4,])] 
// 去重
```

Set内部不会发生类型转换,5和‘5’是两个不同的值

其原因是使用的算法是“Same-value-zero equality”,类似于精确相等运算符(===),主要的区别是向Set 加入值认为NaN等于,自身而精确相等运算符认为`NaN`不等于自身。

```
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b)
set // Set {NaN}
```

### Set实例的属性和方法

 Set.prototype.size: 返回Set实例的成员 总数

Set.prototype.add(val):添加某个值 （返回的是Set结构本身）

Set.prototype.delete(val):删除某值

Set.prototype.has(val):返回一个布尔值,表示值是否为Set的成员

Set.prototype.clear():清除所有成员  无返回值

```javascript
s.add(1).add(2).add(2);
// 注意2被加入了两次

s.size // 2

s.has(1) // true
s.has(2) // true
s.has(3) // false
if(s.has(3)) //使用这种方法判断3是否存在
s.delete(2);
s.has(2) // false
```

遍历方法

我一般使用for  of或者forEach/[...set] (或者解构为[])

### WeakSet

WeakSet 是一个构造函数，可以使用`new`命令，创建 WeakSet 数据结构。  (在此不过多介绍)

### Map含义/基本用法(重点介绍)

​	*JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。*

```javascript
const data = {};
const element = document.getElementById('myDiv');

data[element] = 'metadata';
data['[object HTMLDivElement]'] // "metadata"
```

为了解决问题ES6提供了Map数据结构 

**由上可见,Map类似于对象也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。**

```javascript
const m = new Map();
const o = {p: 'Hello World'};
//把对象o当做键
m.set(o, 'content') //设置/添加键值对
m.get(o) // "content" //读取

m.has(o) // true    // 判断是否存在
m.delete(o) // true //删除键
m.has(o) // false
```

*事实上，不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作`Map`构造函数的参数。这就是说，`Set`和`Map`都可以用来生成新的 Map。*

```javascript
const items = [
  ['name', '张三'],
  ['title', 'Author']
];

const map = new Map();

items.forEach(
  ([key, value]) => map.set(key, value)
);
const m2 = new Map([['baz', 3]]);
const m3 = new Map(m2);
m3.get('baz') //3
```

```javascript
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```

上面代码的`set`和`get`方法，表面是针对同一个键，**但实际上这是两个不同的数组实例，内存地址是不一样的**，因此`get`方法无法读取该键，返回`undefined`。

同理，同样的值的两个实例，在 Map 结构中被视为两个键。

```javascript
const map = new Map();

const k1 = ['a'];
const k2 = ['a'];

map
.set(k1, 111)
.set(k2, 222);

map.get(k1) // 111
map.get(k2) // 222
```

Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。**这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，**就不用担心自己的属性与原作者的属性同名。

如果Map的键是一个简单的类型的值(数字、字符、布尔值)只要两个值严格相等，Map 将其视为一个键，比如**`0`和`-0`就是一个键**，**布尔值`true`和字符串`true`则是两个不同的键**。另外，**`undefined`和`null`也是两个不同的键**。虽然**`NaN`不严格相等于自身**（与Set一样，不区分NAN)，但 Map 将其视为同一个键。

### Map实例的属性及用法

size

map.set(key,value)

```javascript
//返回当前的map 可使用链式写法
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```

map.get

map.has

map.delete

map.clear

最常用的一种（map最常使用的场景）

```
let a = [1,2,3,4,5]
let map = new Map()
for(let i=0;i<a.len;i++){
	map.set(a[i],i)
}
map.forEach((value,key)=>{
	console.log(value)
})
```

遍历方法 如果不会的时候查看

```javascript
for (let [key, value] of map) {
  console.log(key, value);
} //常使用
```

https://es6.ruanyifeng.com/#docs/set-map#%E9%81%8D%E5%8E%86%E6%96%B9%E6%B3%95

## this 绑定

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this

https://segmentfault.com/a/1190000011194676   思否文章

😎首先对this下个定义：**this是在执行上下文创建时确定的一个在执行过程中不可更改的变量。**

所谓**执行上下文**，就是JavaScript引擎在执行一段代码之前将代码内部会用到的一些**变量**、**函数**、**this**提前声明然后保存在变量对象中的过程。

this绑定优先级

```haxe
new 绑定 > 显示绑定 > 隐式绑定 > 默认绑定
```

在绝大多数情况下，函数的调用方式决定了 `this` 的值（运行时绑定）

无论是否在严格模式下，在全局执行环境中（在任何函数体外部）`this` 都指向全局对象

```
console.log(this === window); // true
a = 37 
console.log(window.a) //37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

因为下面的代码不在严格模式下，且 `this` 的值不是由该调用设置的，所以 `this` 的值默认指向全局对象

```
function f1(){
  return this;
}
//在浏览器中：
f1() === window;   //在浏览器中，全局对象是window
//在Node中：
f1() === globalThis;
```

### [函数上下文中的 this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this#函数上下文中的_this)

```javaScript
// 对象可以作为 bind 或 apply 的第一个参数传递，并且该参数将绑定到该对象。
var obj = {a: 'Custom'};

// 声明一个变量，并将该变量作为全局对象 window 的属性。
var a = 'Global';

function whatsThis() {
  return this.a;  // this 的值取决于函数被调用的方式
}

whatsThis();          // 'Global' 因为在这个函数中 this 没有被设定，所以它默认为 全局/ window 对象
whatsThis.call(obj);  // 'Custom' 因为函数中的 this 被设置为obj
whatsThis.apply(obj); // 'Custom' 因为函数中的 this 被设置为obj
```

### [this 和对象转换](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this#this_和对象转换)

setTimeout会改变this的指向



在[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)中，`this`与封闭词法环境的`this`保持一致。在全局代码中，它将被设置为全局对象：

```
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true
```

箭头函数

```
// 创建一个含有bar方法的obj对象，
// bar返回一个函数，
// 这个函数返回this，
// 这个返回的函数是以箭头函数创建的，
// 所以它的this被永久绑定到了它外层函数的this。
// bar的值可以在调用中设置，这反过来又设置了返回函数的值。
var obj = {
  bar: function() {
    var x = (() => this);
    return x;
  }
};

// 作为obj对象的一个方法来调用bar，把它的this绑定到obj。
// 将返回的函数的引用赋值给fn。
var fn = obj.bar();

// 直接调用fn而不设置this，
// 通常(即不使用箭头函数的情况)默认为全局对象
// 若在严格模式则为undefined
console.log(fn() === obj); // true

// 但是注意，如果你只是引用obj的方法，
// 而没有调用它
var fn2 = obj.bar;
// 那么调用箭头函数后，this指向window，因为它从 bar 继承了this。
console.log(fn2()() == window); // tru
```

如果函数是在某个 上下文对象 下被调用

```
   this绑定的是那个上下文对象，例 : var obj = { foo : foo };    obj.foo();  foo 中的 this 就是 obj . 这样的绑定方式叫 隐性绑定 .
```

## 闭包

```
闭包不是私有的，闭的意思不是封闭内部状态 ，而是‘封闭外部状态’ 一个函数如何能够封闭外部状态呢 当外部状态的scope失效的时候， 还有一份留在内部状态里面 
```

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures

一个函数和对其周围状态（**lexical environment，词法环境**）的引用捆绑在一起（或者说函数被引用包围），这样的组合就是**闭包**（**closure**）

也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用域。在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。

参考节流防抖 

特点   闭包允许将函数与其所操作的某些数据（环境）关联起来 函数嵌套函数 函数内部可以使用外包的函数   不会被js 垃圾处理机制所影响

```
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);
```

## Scope（作用域）

https://developer.mozilla.org/zh-CN/docs/Glossary/Scope

JS采用静态作用域（记忆）

因为 JavaScript 采用的是词法作用域，**函数的作用域在函数定义的时候就决定了。**（函数的作用域基于函数创建的位置。）

而与词法作用域相对的是动态作用域，函数的作用域是在函数调用的时候才决定的。

```
var value = 1;

function foo() {
    console.log(value);
}

function bar() {
    var value = 2;
    foo();
}

bar();

假设JavaScript采用静态作用域，让我们分析下执行过程：

执行 foo 函数，先从 foo 函数内部查找是否有局部变量 value，如果没有，就根据书写的位置，查找上面一层的代码，也就是 value 等于 1，所以结果会打印 1。

假设JavaScript采用动态作用域，让我们分析下执行过程：

执行 foo 函数，依然是从 foo 函数内部查找是否有局部变量 value。如果没有，就从调用函数的作用域，也就是 bar 函数内部查找 value 变量，所以结果会打印 2。
```

## new

https://zhuanlan.zhihu.com/p/23987456 实现组合继承  （构造继承+原型链）

#### call、apply、bind

https://segmentfault.com/a/1190000018270750

#### 原型

https://github.com/febobo/web-interview/issues/59

什么是原型？

原型是对象中的内置属性，其实就是对象其他属性的引用

几乎所有的对象在创建时会产生一个赋值的[[prototype]]属性 

什么是原型链？

原型链是一种关系

实例对象通过属性 `_proto_`查找其构造函数的属性或者方法

`__proto__`作为不同对象之间的桥梁，用来指向创建它的构造函数的原型对象的

[![img](https://camo.githubusercontent.com/10ba2b15ee90f7a8d9881431005ad5e9b004a740878fa7727e631e5597504400/68747470733a2f2f7374617469632e7675652d6a732e636f6d2f36613734323136302d373235652d313165622d616239302d6439616538313462323430642e706e67)](https://camo.githubusercontent.com/10ba2b15ee90f7a8d9881431005ad5e9b004a740878fa7727e631e5597504400/68747470733a2f2f7374617469632e7675652d6a732e636f6d2f36613734323136302d373235652d313165622d616239302d6439616538313462323430642e706e67)

每个对象的`__proto__`都是指向它的构造函数的原型对象`prototype`的（这个就叫做原型链）

```
person1.__proto__ === Person.prototype
```

构造函数是一个函数对象，是通过 `Function `构造器产生的

```
Person.__proto__ === Function.prototype
```

原型对象本身是一个普通对象，而普通对象的构造函数都是`Object`

```
Person.prototype.__proto__ === Object.prototype
```

刚刚上面说了，所有的构造器都是函数对象，函数对象都是 `Function `构造产生的

```
Object.__proto__ === Function.prototype
```

`Object `的原型对象也有`__proto__`属性指向`null`，`null`是原型链的顶端

```
Object.prototype.__proto__ === null
```

#### Class

https://zhuanlan.zhihu.com/p/158956514

使用class

```text
class Person {
  constructor (name) {
    this.name = name
  }
  
  talk () {
    console.log(`${this.name} says hello`)
  }
}
非常接近于
function Person (name) {
  this.name = name
}
Person.prototype.talk = function () {
  console.log(`${this.name} says hello`)
}
执行代码时

const dwx  = new Preson('dwx')
const button ={}
button.onclick = dwx.talk() //可以执行
button.onclick = dwx.talk
button.onclick() // 输出 undefined says hello 原因是this被改变了

原因 this变为window上的this了而不是Preson里的this了

修改方式一 使用bind修改this指向 bind不会立即执行且参数只有一个

class Person {
  constructor (name) {
    this.name = name
    this.talk = this.talk.bind(this); // 在构造器里显式调用 bind 函数绑定 this
  }

  talk () {
    console.log(`${this.name} says hello`)
  }
}
方法二：
使用箭头函数 
使用类属性+箭头函数的方式来定义方法
class Person {
  constructor(name) {
    this.name = name
  }

  talk = () => {
    console.log(`${this.name} says hello`)
  }
}
```

工厂函数替代class

```text
const PersonFactory = (name) => {
  return {
    talk: () => {
      console.log(`${name} says Hello`)
    }
  }
}//闭包特性
```

```text
工厂模式写接口

function httpClientFactory(baseUrl) {
  return {
    baseUrl: baseUrl,
    listUsers: () => {
      return axios.get(`${baseUrl}/users`)
    },
    getUser: (id) => {
      return axios.get(`${baseUrl}/users/${id}`)
    },
    createUser: (user) => {
      return axios.post(`${baseUrl}/users`, user);
    },
    listBooks: () => {
      return axios.get(`${baseUrl}/books`)
    },
    getBook: (bookName) => {
      return axios.get(`${baseUrl}/books/${bookName}`)
    },
    createBook: (book) => {
      return axios.post(`${baseUrl}/books`, book)
    }
  }
}

const httpClient = httpClientFactory("https://your-endpoints/api");
httpClient.getUser("123");
httpClient.getBook("JavaScript Is Interesting");
console.log("The httpClient's baseUrl is " + httpClient.baseUrl);
```

https://juejin.cn/post/6844904094079926286

## Promise

```javaScript
// promis写法 
let newPromise = new Promise((resolve, reject) => {

  setTimeout(() => {

​    resolve('成功了！') //成功输出

​    reject('失败了')

  }, 500);

})



newPromise.then((res) => {

  return new Promise((resolve) => {

​    setTimeout(() => {

​      resolve(res + '之后再次成功')

​    }, 500)

  })

}).then(res => {

  console.log('结果' + res)

})

.catch((res) => {

  console.log('结果' + res)

})
```

*pending*等待 resolve成功 reject失败  三种状态

上述的代码promise链式调用解决了回调地狱( 一个异步请求套着一个异步请求，一个异步请求依赖于另一个的执行结果，使用回调的方式相互嵌套。)



## Iterator 迭代器

https://es6.ruanyifeng.com/#docs/iterator

js原有表示‘集合’的结构  array、object 新增Map Set

作用：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令`for...of`循环，Iterator 接口主要供`for...of`消费。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的`next`方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的`next`方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的`next`方法，直到它指向数据结构的结束位置。

```javascript
var it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }

function makeIterator(array) {
  var nextIndex = 0;
  return {
    next: function() {
      return nextIndex < array.length ?
        {value: array[nextIndex++], done: false} :
        {value: undefined, done: true};
    }
  };
}
```

Iterator 接口的目的，就是为所有数据结构，提供了一种统一的访问机制`for...of`循环

ES6 规定，默认的 Iterator 接口部署在数据结构的`Symbol.iterator`属性，或者说，一个数据结构只要具有`Symbol.iterator`属性，就可以认为是“可遍历的”

```javascript
const obj = {
  [Symbol.iterator] : function () {
    return {
      next: function () {
        return {
          value: 1,
          done: true
        };
      }
    };
  }
};
```

## Generator函数

https://es6.ruanyifeng.com/#docs/generator

Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）。

```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

调用 Generator 函数后，该函数并不执行，**返回的也不是函数运行结果，而是一个指向内部状态的指针对象**，也就是上一章介绍的遍历器对象（Iterator Object）。

```javascript
hw.next()
// { value: 'hello', done: false }

hw.next()
// { value: 'world', done: false }

hw.next()
// { value: 'ending', done: true }

hw.next()
// { value: undefined, done: true }
```

ES6 提供了`yield*`表达式，作为解决办法，用来在一个 Generator 函数里面执行另一个 Generator 函数。



## async函数

async函数是generator函数的语法糖

https://juejin.cn/post/6844904102053281806

async await 后面必须跟着promise的方法不然不会生效

利用 generator

```javascript
function* testG() {
  // await被编译成了yield
  const data = yield getData()
  console.log('data: ', data);
  const data2 = yield getData()
  console.log('data2: ', data2);
  return 'success'
}

```

generator函数不会自动执行需要使用 .next()执行  需要编写自动函数让这个generator函数实现async功能



```javaScript
const getData = () => new Promise(resolve => setTimeout(() => resolve("data"), 1000))
  
var test = asyncToGenerator(
    function* testG() {
      // await被编译成了yield
      const data = yield getData()
      console.log('data: ', data);
      const data2 = yield getData()
      console.log('data2: ', data2);
      return 'success'
    }
)

test().then(res => console.log(res))

```

```
asyncToGenerator`接受一个`generator`函数，返回一个`promise
>>>>>>> Stashed changes:JavaScript/A-js系统学习.md
```

## Proxy(代理)
使用方法
```javaScript
	var obj = {
		val:1
	}
	var proxy = new Proxy(obj,{
		get:(target, propKey, receiver)=>{
			console.log(target, propKey, receiver)
			retun Reflect.get(target,propKey,receiver)
		},
		set:(target,propKey,receiver){
			console.log(target)
			return 
		     Reflect.set(target,propKey,receiver)
		}
		
	})

```

https://es6.ruanyifeng.com/#docs/proxy
## Reflect(与Proxy一起学习)
1.存在obj对象的方法
2.将某些 `Object` 方法 移植到`Reflect`并修改的更合理（修改属性添加返回值等）  
3.`Reflect`对象的方法与`Proxy`对象的方法一一对应
https://es6.ruanyifeng.com/#docs/reflect
例如:

-   `Reflect.get(target, name, receiver)` 查找并返回`target`对象的`name`属性，如果没有该属性，则返回`undefined`。