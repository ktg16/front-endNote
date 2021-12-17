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



js继承方法

