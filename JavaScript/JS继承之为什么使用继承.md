JS继承之为什么使用继承

Js继承之prototype 与 _ _propto_ _关系

__proto__（隐式原型）与prototype（显式原型）

显示原型

每一个函数在创建之后都会拥有一个名为prototype的属性，这个属性指向函数的原型对象

隐式原型

JavaScript中任意对象都有一个内置属性[[prototype]]，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过__proto__来访问S5中有了对于这个内置属性标准的Get方法Object.getPrototypeOf().

隐式原型指向**创建**这个对象的函数(constructor)的prototype

```js
function object(o){
    function F(){}
    F.prototype = o;
    return new F()
}
//以下是用于验证的伪代码
var f = new F(); 
//于是有
f.__proto__ === F.prototype //true
//又因为
F.prototype === o;//true
//所以
f.__proto__ === o;



function Foo(){}
var foo = new Foo()
fo.__proto__ === Foo.prototype
Foo.prototype.__proto__ === Object.prototype //true 理由同上
  

var foo = new Foo() //会立即执行一下Foo()
new操作符干了啥
var obj = {}
obj._proto_ ===Foo.prototype
Foo.call(obj);//会立即执行一下Foo() apply也会执行  bind第一次不会执行
```



## js继承方法

https://juejin.cn/post/6844903696111763470#heading-2

### 1.原型链继承

构造函数、原型和实例之间的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个**原型对象的指针**。

继承的本质就是**复制，即重写原型对象，代之以一个新类型的实例**。

```js
function superType(){
	this.name = 'hihi'
	this.color = ['green','yellow']
	this.getName = ()=>{
		console.log(this.name)
	}
}
function supType(){
	
}

supType.prototype = new superType()

var instance = new supType()
console.log(instance.name)
var instance1 = new supType()
instance.color.push('ss')

instance1.color  // ['green','yellow','ss'] 被篡改了

```

缺点:原型链方案存在的缺点：多个实例对引用类型的操作会被篡改

### 2.构造继承

使用父类的构造函数来增强子类**实例**，等同于复制父类的实例给子类（不使用原型）

```
function superType(){
	this.color = ['green']
	this.name = 'hihi'
}
function supType(){
	superType.call(this)
}
var instance = new supType()
console.log(instance.color)
var instance1  = new superType()
console.log(instance1.color)

```

- 只能继承父类的**实例**属性和方法，不能**继承原型属性/方法(superType.prototype)**
- 无法实现复用，**每个子类都有父类实例函数的副本**，影响性能

### 3.组合继承(原型链+构造)



用**原型链**实现对**原型**属性和方法的继承，用借用**构造函数**技术来实现**实例**属性的继承。

```
function  superType(){
	this.name = '123456'
	this.color = ['red']

}
superType.prototype.sayName = function(){
console.log(this.name)
} 
function supType(age,name){
	this.age = age
	superType.call(this,name)
}

supType.prototype = new superType()
supType.prototype.contustor  =  supType

supType.prototype.sayAge = ()=>{
	cosnole.log(this.name)
}
 var instance1 = new supType(16,'dwx')
```

缺点: 第一次调用SuperType():给 supType 写入两个属性 name，color 

第二次调用`SuperType()`：给`instance1`写入两个属性name，color

实例对象`instance1`上的两个属性就屏蔽了其原型对象SubType.prototype的两个同名属性。所以，组合模式的缺点就是在使用子类创建实例对象时，其原型中会**存在两份相同的属性/方法（影响性能）。**（不懂可以看链接）



### 4.原型继承 

 创建一个createObj   作为一个空对象作为中介  将某个对象直接赋值给空对象构造函数的原型

```js
function createObj(obj){

 function F (){}

​		F.prototype  = obj

return new F()

}

var Person = {

name:'per',

friends:['Lisa']

}

var instance =  createObj(Person)
instance.__proto__ === Person
//缺点:1.无法传递参数 2.原型链继承多个实例的引用类型，存在篡改的可能  因为是浅复制


```

### 5.寄生继承（原型继承的加强）

核心：**在原型式继承的基础上，增强对象**，返回构造函数（实际上就是在原有中介再加一个中介 称之为加强中介）

```
// 寄生继承

function createAnother(original) {
    var clone = new createObj(original)
    clone.sayAge = function(){  //增强对象  添加调用的方法
        console.log('hi')
    }
    return clone
}

var  another = createAnother(person)
another.sayAge()
console.log(another.name)


```

函数的主要作用是为构造函数新增属性和**方法**，以**增强函数**

缺点与原型继承一样  会被篡改

### 6.寄生组合函数

```
function inheritPrototype(superType,supType){
    //supType.prototype = Object.create(superType.prototype)
    //supType.prototype.constructor = supType
    //console.log(supType.prototype)
    
    var prototype = Object.create(superType.prototype); // 创建对象，创建父类原型的一个副本
  prototype.constructor = subType;                    // 增强对象，弥补因重写原型而失去的默认的constructor 属性
  subType.prototype = prototype;                      // 指定对象，将新创建的对象赋值给子类的原型

}

function superType(name){
    this.name=name
    this.color=['red']
}
superType.prototype.sayName = function(){
    console.log(this.name)
}

function supType(name,age){
    this.age = age
    superType.call(this,name)
}

supType.prototype.sayAge = function(){ console.log(this.age)}

inheritPrototype(superType,supType)

var instance = new supType('dwx',22)
console.log(instance,instance.age)
```

这个例子的高效率体现在它只调用了一次`SuperType` 构造函数，并且因此避免了在`SubType.prototype` 上创建不必要的、多余的属性。于此同时，原型链还能保持不变；因此，还能够正常使用`instanceof` 和`isPrototypeOf()`

**这是最成熟的方法，也是现在库实现的方法**

### 7.class 继承

```JavaScript
class reinforce {
    constructor(name, age) {
        this.name = name
        this.age = age
        this.length = 10
    }
    sayName() {
        console.log(this.name)
    }
    sayAge() {
        console.log(this.age)
    }
}

class instance extends reinforce {
    constructor(name, age) {
        super(name, age)
        this.name = name
    }

    sayName() {
        super.sayAge()
        console.log(this.name, 'instance')
    }

}
let instance1 = new instance('dwx', 22) //new 之后调用

console.log(instance1.sayName())
```

2、ES5继承和ES6继承的区别

- ES5的继承实质上是先创建子类的实例对象，然后再将父类的方法添加到this上（Parent.call(this)）.
- ES6的继承有所不同，实质上是先创建父类的实例对象this，然后再用子类的构造函数修改this。因为子类没有自己的this对象，所以必须先调用父类的super()方法，否则新建实例报错

