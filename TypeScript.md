# TypeScript

```js
npm install typescript -g 全局安装Ts
```



create-react-app proName --typescript  创建react项目

简介

TypeScript 是由微软公司在 2012 年正式发布，现在也有 8 年的不断更新和维护了，TypeScript 的成长速度是非常快的，现在已经变成了前端必会的一门技能。TypeScript 其实就是 JavaScript 的超集，也就是说 TypeScript 是建立在 JavaScript 之上的，最后都会转变成 JavaScript。这就好比漫威里的钢铁侠，没穿装甲之前，他实力一般，虽然聪明有钱，但还是接近人类。但是有了装甲，他就厉害太多了，甚至可以和神干一架。



使用方式

Node 不能直接运行`TypeScript`文件，需要用`tsc Demo1.ts`转换一下，转换完成后`typeScript`代码被编译成了`javaScript`代码,新生成一个`demo1.js`的文件，这时候你在命令行输入`node Demo1.js`,在终端里就可以顺利的输出`jspang`的字符了。

```js
npm install -g ts-node  //全局安装ts-node插件
```

## 什么是静态类型？

就是你一旦定义了，就不可以再改变了

demo

```js
const count: number = 1; //基础静态类型
count 可以使用number类型上所有的属性和方法
```

#### 自定义静态类型

```js
interface XiaoJieJie {
  uname: string;
  age: number;
}

const xiaohong: XiaoJieJie = {
  uname: "小红",
  age: 18,
};
```

如果使用了静态类型，不仅意味着变量的类型不可以改变，还意味着类型的属性和方法也跟着确定了

对象类型

用类的形式，来定义变量

```js
class Person {}
const dajiao: Person = new Person();
```

```js
const xiaoJieJies: String[] = ["谢大脚", "刘英", "小红"]; 数组类型
```

函数类型

```js
const jianXiaoJieJie:string = () => {
  return "大脚";
};
```

```
类型注解`和`类型推断
```

```js
let count: number;  类型注解   count变量是数字类型
count = 123;  

let countInference = 123;  //TypeScript 自动把变量注释为了number（数字）类型 TS 会自动的去尝试分析变量的类型
```

- 对象类型
- 数组类型
- 类类型
- 函数类型

这几种形式我们在`TypeScript`里叫做对象类型。

工作中使用问题

- 如果 `TS` 能够自动分析变量类型， 我们就什么也不需要做了
- 如果 `TS` 无法分析变量类型的话， 我们就需要使用类型注解

**函数的参数类型定义和返回值的定义**

```js
function getTotal(one: number, two: number): number//函数返回值的类型注释 {
  return one + two;
}

const total = getTotal(1, 2);
```

函数无返回值的定义方法 (void 代表无返回值)

```js
function sayHello(): void {
  console.log("hello world");
}
```

never返回值类型

```js
function errorFuntion(): never {
  throw new Error();
  console.log("Hello World");
} //执行的时候，抛出了异常，这时候就无法执行完了
```

```js
function forNever(): never {
  while (true) {}
  console.log("Hello JSPang");
} //死循环
```

函数的参数是对象是（解构 ） 时

```js
function add({ one, two }: { one: number, two: number }): number {
  return one + two;
}

const three = add({ one: 1, two: 2 });

//错误写法（绝对不可以写这种写法）
function getNumber({ one }: number) {
  return one;
}

const one = getNumber({ one: 1 });
```





#### 基本类型

any 任意类型

number 表示数字   整数和分数

string 表示 字符串

boolean 布尔类型

数组类型  

`let arr:number[] = [1,2]`    

```js
const stringArr: string[] = ["a", "b", "c"];
const arr: (number | string)[] = [1, "string", 2]; //数组中既有数字又有字符串
```

**数组中对象类型的定义**

```js
const xiaoJieJies: { name: string, age: Number }[]// {对象格式}[数组里面是对象]
= [
  { name: "刘英", age: 18 },
  { name: "谢大脚", age: 28 },
];
```

#### **类型别名**

优先定义一个类型别名  

```js
type Lady = { name: string, age: Number };
//也可以这样子
class Madam {
  name: string;
  age: number;
}
const xiaoJieJies: Madam[] = [
  { name: "刘英", age: 18 },
  { name: "谢大脚", age: 28 },
];


```



#### interface接口

```js
interfance Girl{
	name：string;
	age:number;
	bust:number;
}
const screenResume = (girl:Girl)=>{
 girl.age < 24 && girl.bust >= 90 && console.log(girl.name + "进入面试");
  girl.age > 24 || (girl.bust < 90 && console.log(girl.name + "你被淘汰"));
}
const getResume = (girl: Girl) => {
  console.log(girl.name + "年龄是：" + girl.age);
  console.log(girl.name + "胸围是：" + girl.bust);
};
cosnt girl = {
    name:'大脚',
    age:18，
    bust:94
}
screenResume(girl);
getResume(girl);
```

#### 接口和类型别名的区别

*类型别名可以直接给类型，比如`string`，而接口必须代表对象。*

type Girl1 =  string

interfance 只能是代表一个对象

interfance girl ={

​	namer:'大脚';

​	age:18;

​	bust:94;

}

**interfance 非必选定义**

interfance Girl{

​	name:string;

​	age:number;

​	bust:number

​	waistline?:number //定义时可以存在 也可以不存在

}

#### interface接口2

允许加入任意值

```js
interfance Girl{
	name:string;
	age:number;
	bust:number
	waistline?:number //定义时可以存在 也可以不存在
	[propname:string]:any;
}
const girl = {
  name: "大脚",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
}; //这时候可以传入参数
```

接口里的方法

```js
interface Girl {
  name: string;
  age: number;
  bust: number;
  waistline?: number;
  [propname: string]: any;
  say(): string;
}//面向对象编程

const girl = {
  name: "大脚",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
  say() {
    return "欢迎光临 ，红浪漫洗浴！！";
  },
};
```

接口和类的约束

```js
class XiaoJieJie implements Girl { //类与接口很好的结合（重点）
     name = "刘英";
  age = 18;
  bust = 90;
  say() {
    return "欢迎光临 ，红浪漫洗浴！！";
  }
}
```

接口间的继承

```tsx
interfance Teacher extends Gils{
    teach():string;
}
需要修改girl对象 才能传入方法（看不懂可参考技术胖文章）
const girl = {
  name: "大脚",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
  say() {
    return "欢迎光临 ，红浪漫洗浴！！";
  },
  teach() {
    return "我是一个老师";
  },
};
```

**Typescirpt中类的概念和使用**



```js
class Lady { //类的使用 继承
  content = "Hi，帅哥";
  sayHello() {
    return this.content;
  }
}
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you";
  }
}

const goddess = new XiaoJieJie();
console.log(goddess.sayHello());
console.log(goddess.sayLove());
//super关键字和类的重写
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you!";
  }
  sayHello() {
    return super.sayHello() + "。你好！"; //使用父元素中的sayHello()
  }
}
```



**类的访问类型**就是基于三个关键词`private`、`protected`和`public`

private  私有的 只允许内部使用

protected   允许在类内及继承子类中使用

```js
class Person{
	protected name：string;
    public sayHello(){
        console.log(this.name)//不报错
    }
}
class Teacher extends Person{
    public sayBye(
    	this.name
    )
}
```

类的构造函数

构造函数的关键字是constructor 常与super一起使用

> 这就是子类继承父类并有构造函数的原则，就是在子类里写构造函数时，必须用super()调用父类的构造函数，如果需要传值，也必须进行传值操作。就是是父类没有构造函数，子类也要使用super()进行调用，否则就会报错。

```js
class Person{
    constructor(public name:string){}
}
class Person{
	constructor(public name:sting){}
}
//等同于 下列写法
class Person{
    public name :string ;
    constructor(name:string){
        this.name=name
    }

}

class Teacher extends Person{
    constructor(public age:number){
        super('jspang')
    }
}

const teacher = new Teacher(18)
console.log(teacher.age)
console.log(teacher.name)
```

#### 类的getter和Setter static readonly

设置private类型 如果想访问需要借助getter 需要修改借助setter

```js
class Xiaojiejie {
  constructor(private _age:number){}
  get age(){
      return this._age-10
  }
  set age(age:number){
    this._age=age
  }
}

const dajiao = new Xiaojiejie(28)
dajiao.age=25  
console.log(dajiao.age) //15
```

静态修饰符 static

```js
class Girl {
  static sayLove() {    //用static声明的属性和方法不需要进行声明对象就可以直接使用 
    return "I Love you";
  }
}
console.log(Girl.sayLove());
```

只读属性 readonly



```js
class Person {
    public readonly _name :string //设置_name为只读  不能修改
    constructor(name:string){
        this.name = name
    }
}

const person = new Person('jspang')
person._name = 'dwx'
console.log(person_name) //jspang
```

什么是抽象类？

#### abstract 抽象类的关键词

有了这个抽象类，三个类就可以继承这个类，然后会要求必须实现`skill()`方法

```js
abstract class Girl{
    abstract skill()  //因为没有具体的方法，所以我们这里不写括号
}
class Waiter extends Girl{
    skill(){
        console.log('大爷，请喝水！')
    }
}

class BaseTeacher extends Girl{
    skill(){
        console.log('大爷，来个泰式按摩吧！')
    }
}

class seniorTeacher extends Girl{
    skill(){
        console.log('大爷，来个SPA全身按摩吧！')
    }
}
```







#### 元组         

元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，对应位置的类型需要相同。

let x:[string,number];

x=['Runoob',1];//运行正常

console.log(x[0])







#### 函数返回值

```js
function greet():string {

     // 返回一个字符串    

    return "Hello World"

     var msg = greet() // 调用 greet() 函数 

  } 

function caller() {     

var msg = greet() // 调用 greet() 函数     

console.log(msg)  } 
```

带参数函数

```js
function add(x:number,y:number): number//返回值{
return x+y
}
console.log(add(1,2))
```



#### tsconfig.json文件

`complierOptions`配置项 配置（了解）

http://www.jspang.com/detailed?id=63#toc254

https://www.tslang.cn/docs/handbook/compiler-options.html  配置api

#### TypeScript 联合类型

```tsx
var val:string|number  
val = 12  
console.log("数字为 "+ val)  
val = "Runoob"  
console.log("字符串为 " + val)    

//如果我直接写一个这样的方法，就会报错
interfance Waiter {
	a:boolean;
    say:()=>{};
}
interfance Teacher{
    anjiao:boolean;
    skill:()=>{}
}
function demo(animal:Waiter|Teacher){
    animal.say()
}
```

#### 类型保护-类型断言

```js
//通过断言的方式确定传递过来的准确值 
function demo(animal:Waiter|Teacher){
    if(animal.a){   //animal是否存在a
        (animal as Teacher).skill() // 断言animal as Teacher
    }
}
```

#### 类型保护-in语法

```js
// 配合if判断里面是否存在xx

function demo(animal:Waiter|Teacher){
    if('skill' in animal){
        animal.skill()
    }else{
        animal.say()
    }
}
```

#### 类型保护-typeof语法

```js
function add(first: string | number, second: string | number) {
  return first + second;
} // 报错
```

```js
function add(first: string | number, second: string | number) {
  if (typeof first === "string" || typeof second === "string") {
    return `${first}${second}`;
  }
  return first + second;
}
```

#### 类型保护-instanceof语法

```js
class NumberObj{
	count:number
}

function addObj(first: object | NumberObj, second: object | NumberObj){
    if(first instanceof NumberObj && second instanceof NumberObj){
        return firstreturn first.count + second.count;
    }
    return 0;
}
```

#### 枚举  enum    枚举类型用于定义数值集合。

```
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2
```

```js
//判断最佳写法
enum Status {
  MASSAGE,
  SPA,
  DABAOJIAN,
}

function getServe(status: any) {
  if (status === Status.MASSAGE) {
    return "massage";
  } else if (status === Status.SPA) {
    return "spa";
  } else if (status === Status.DABAOJIAN) {
    return "dabaojian";
  }
}

const result = getServe(Status.SPA);

console.log(`我要去${result}`);
```

如果不想enum默认从0开始  

```js
enum Status {
  MASSAGE = 1, // 从1开始
  SPA,
  DABAOJIAN,
}
  console.log(Status.MASSAGE, Status[1]); //1,MASSAGE
```



#### 泛型

`泛型数组`   

`let arr：Array<number> =[1,2]`    

let    arr: number[] =[1,2]

`泛型：[generic - 通用、泛指的意思],那最简单的理解，泛型就是泛指的类型。`

泛型的定义使用`<>`（尖角号）进行定义的(想当于定义一个变量，调用的时候给变量赋值)

```js
function contact<joint>(first:joint,seconed:joint){
	return `${fitst}${seconed}`
}
contact< string >('fe','eel')
```



```js
function Fun <ARR>(params:ANY[]){
	return params
}
Fun< string > ['123','456']
```

多个泛型定义

一般情况下泛型用<T>来表示

```js
function join <T, P>(first:T,seconed:P){

	return `${first}${seconed}`
}  

join<string, number> ('123',12)
```

初始类的泛型

```tsx
class SelectGirl<T>{
    constructor(private girls:T[]){}
    getGils(index:number){
        return this.girl[index];
    }
}

const selectGirl = new SelectGil<string>(['小美'，'小圆',"小花"])
```









never 是其他类型  （包括 null 和 undefined）的子类型，代表从不会出现的值。









#### 类型断言

```
var str = '1' 
var str2:number = <number> <any> str   //str、str2 是 string 类型
console.log(str2)
```

#### 类型推断

```
var num = 2;    // 类型推断为 number
console.log("num 变量的值为 "+num); 
num = "12";    // 编译错误
console.log(num);
```

类运算符  typeof  num 返回操作数的数据类型









#### 变量作用域



### String 对象属性

prototype

允许您向对象添加属性和方法

```
function employee(id:number,name:string) { 
    this.id = id 
    this.name = name 
 } 
```

```
employee.prototype.email="admin@runoob.com"
```

### 数组解构

```tsx
var arr:number[] = [12,13] 
var[x,y] = arr // 将数组的两个元素赋值给变量 x 和 y
console.log(x) 
console.log(y)
```

```tsx
var j:any; 
var nums:number[] = [1001,1002,1003,1004] 
 
for(j in nums) { 
    console.log(nums[j]) 
}
```

#### 接口和数组

```tsx
interface namelist { 
   [index:number]:string 
} 
 
var list2:namelist = ["John",1,"Bran"] // 错误元素 1 不是 string 类型
interface ages { 
   [index:string]:number 
} 
 
var agelist:ages; 
agelist["John"] = 15   // 正确 
```

复方苯甲酸软膏、咪康唑霜剂 水杨酸软膏  特比萘芬霜剂 酮康唑乳膏



