### 转义字符

```plain
`\t 制表位
`\n 换行符
`\\ 一个\`
`\" 一个"`
`\'`一个‘
‘\r’ 回车。 后面替换前面的
```

### 文档注释

可以被jdk提供的工具javadoc所解析 生成一套网页文件形式体现的该程序的说明文档，一般写在类

是使用javadoc标签构成

```java
/**
* @author 小明
* @version 1.0
*/
```

如何生成对应的文档注释

javadoc -d 文件夹名 -xx  -yy Demo3.java

有哪些标签直接看文档即可

### 代码规范

1.运算符等号两侧要加空格符，

2.单行不要超过80行

3.代码编写次行风格和行尾风格（推荐）



### dos命令

dos： disl operating Syetem

1.查看当前目录是有什么内容 dir d:\abc\test 

2.cd 切换到其他盘下

3.tree 查看目录树

4.清屏cls

变量  （变化值）

### 数据类型

每一种数据都定义了明确的数据类型（**强类型**），在内存中分配了不同大小的内存空间

1.基本数据类型

数值型：

整数类型：存放整数（byte[1],short[2],int[4],long[8]）

浮点(小数)类型：float[4],double[8]   是怎么构成的浮点数 = 符号位 + 指数位 +尾数位

字符型 char[2]

布尔型 boolean[1] 存放true false

2.引用数据类型

类 class 接口interfance 数组[] 自定义的类也属于基本类型

java的整型常量具体值默认为 int型 声明long型常量须后加‘l’或‘L’

浮点型常量默认为double型  声明float须加“f” “F”

通常情况下 应该使用double型 因为它比float型更精确

浮点数陷阱：2.7和8.1/3的比较   8.1/3得不到2.7只能够得到2.6999999需要进行Math.abs()相减得到的值进行判断

### 编码表

utf-8编码表 大小可变的编码字母使用1个字节，汉字使用3个字节

有什么用？ 将代码保存起来。决定了文件的大小



### 基本数据类型转换

精度小的类型自动转换为精度大的数据类型

char -> int -> long -> float-> double

byte -> short -> int -> long -> float ->double

short char byte进行运算会自动升级类型为int

强制类型转换  将容量大的数据类型转为容量小的类型  使用时要加上强制转换符()

强转符合只针对最近的操作数有效，往往使用小括号提升  优先级 



### 命名规范				 						 						 					

- 1) 包名:多单词组成时所有字母都小写:aaa.bbb.ccc //比如 com.hsp.crm  						

- 2) 类名、接口名:多单词组成时，所有单词的首字母大写:XxxYyyZzz[大驼峰]  		比如: TankShotGame 

- 3) 变量名、方法名:多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写:xxxYyyZzz [小 驼峰， 简称 驼峰法]

  比如: tankShotGame 		 			

- 4) 常量名:所有字母都大写。多单词时每个单词用下划线连接:XXX_YYY_ZZZ 比如 :定义一个所得税率 TAX_RATE  						

- 5) 后面我们学习到类，包，接口，等时，我们的命名规范要这样遵守,更加详细的看文档.  						

###  数组

需要先定义

1.动态初始化

int[] a = new int[5] //创建一个数组

1.先声明数组  int[] a

2.创建数组   a = new int[10]

2.静态初始化

int a[] = {2,5,6,7,8,89,90,34,56}



### 排序、查找

### 二维数组

动态初始化 比如 int[][] a = new int[2][3]

静态初始化 int[][] arr  = {{1,11,1},{8,8,9},{100}}

​    String[] strs = {'a', 'b', 'c', 'd', 'e'};  单引号是表示char

## 面向对象编程（基础部分）

类和对象的区别 					 				

1) 类是抽象的，概念的，代表一类事物,比如人类,猫类.., 即它是数据类型. 2) 对象是具体的，实际的，代表一个具体事物, 即 是实例.
2) 类是对象的模板，对象是类的一个个体，对应一个实例 

​		

定义一个类

```java
AA a  = new AA()
// 直接调用对象。a 其实是调用的a.toString 方法
class AA {
public void f4() {

 } }
```

 成员方法的定义 

访问修饰符 返回数据类型 方法名(形参列表..) {//方法体 语句; 

return 返回值; } 

public  void（无数据类型返回 比如：int[] double[]） mul(){

} 			

### 成员方法传参机制 	 	 		

 	 	 		

 			

 				

 基本数据类型，传递的是值（值拷贝），形参的任何改变不影响实参		

（参考java零基础笔记）

（解释：地址没有参与只是值的改变 与js中的深浅拷贝一直只是值的传递,栈空间的独立性） 				

引用数据类型的传参机制  				

 引用类型传递的是地址(传递也是值，但是值是地址)，可以通过形参影响实参!  

引用类型指向的都是同一地址 与javasc有区别（引用类型貌似是存在在堆里）

（js中引用数据类型传参，也不会修改实参）				

 **对象传参机制**			

 与引用类型传参一样，创建的对象也是存在堆里面的			

```java
 Person p  = new Person();
    p.name = "jack";
    p.age = 18;
    b.test200(p);
    System.out.println(p.age)//18
class Person{
  String name;
  int age;
}
class B{
  public void test200(Person p){
     p  = new Person();
     p.name = "John";
     p.age = 1;
  }
}       
```

当 在方法中新创建 p= null 或者 p = new Person()时 main中对象不会改变

（解释: 创建了一个新的对象与我前任没有任何关系）		

### 递归

### 八皇后

回溯法：先把值赋值上再进行去判断  如果判断失败怎返回原来的数据 



### 重载（overload）	 		 				

java 中允许同一个类中，多个同名方法的存在，但要求 形参列表不一致! 

比如:System.out.println(形参); OverLoad01.java  out 是 PrintStream 类型 

7.5.2 重载的好处

1) 减轻了起名的麻烦 
2) 减轻了记名的麻烦

### 可变参数 					 				

java 允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法。  					 					 				

访问修饰符 返回类型 方法名(数据类型... 形参名) { 

} 

### Void 返回类型

void无返回类型

### 作用域 

全局变量：属性			

局部变量也就是除了属性之外的其它变量 作用域为它定义在代码块中 		

 ![img](https://cdn.nlark.com/yuque/0/2023/png/12803466/1683772372105-53eed483-4257-480f-9e18-dbb44fe2eb3e.png)	  			

### 构造方法/构造器 		

（创建对象时，就直接指定这个对象的属性） 	 					 				

1) 方法名和类名相同
2) 没有返回值
3) 在创建对象时，系统会自动的调用该类的构造器完成对象的初始化。 

4）可以默认构造器

一个类中可以有多个构造器

```java
Person p1 = new Person("smith", 80); // 创建对象
class Person {
String name;
int age;
//构造器
//老韩解读
//1. 构造器没有返回值, 也不能写 void //2. 构造器的名称和类 Person 一样
//3. (String pName, int pAge) 是构造器形参列表，规则和成员方法一样 public Person(String pName, int pAge) {
System.out.println("构造器被调用~~ 完成对象的属性初始化"); name = pName;
age = pAge;
}
```

 

构造器重载：再给person类定义一个构造器，用来创建对象的时候，只指定人名,		

 		

```java
class Person { 
    String name;
	int age;//默认 0 //第 1 个构造器
	public Person(String pName, int pAge) { 
        name = pName;
        age = pAge; }
//第 2 个构造器, 只指定人名，不需要指定年龄 public Person(String pName) {
public Person(String pName) {
    name = pName; }

}    
```

### 对象创建流程分析 	 

![img](https://cdn.nlark.com/yuque/0/2023/png/12803466/1683774903619-64b6d165-a8c9-4f4c-bd25-169e67698692.png)

### this关键字

哪个对象调用，this就代表哪个对象

 			

 		

 	 