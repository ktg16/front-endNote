# less学习

https://juejin.cn/post/6844903520441729037#heading-6 文档

### 安装

 npm install less less-loader --save-dev

npm i -D  xxx   简化

### 变量

```
@width:10px
@height:@width+10px

#header{
	width:@width;
	height:@height
}
@Warp:wrap
#@{Warp}{
	color:#666
}
```

### 混合方法（Mixins）

混合（Mixin）是一种将一组属性从一个规则集包含（或混入）到另一个规则集的方法。假设我们定义了一个类（class）如下：

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

如果我们希望在其它规则集中使用这些属性呢？没问题，我们只需像下面这样输入所需属性的类（class）名称即可，如下所示：

```less
#menu a {
  color: #111;
  .bordered();
}

.post a {
  color: red;
  .bordered();
}
```

`.bordered` 类所包含的属性就将同时出现在 `#menu a` 和 `.post a` 中了。

```less
// Variables
@my-selector: banner;

// Usage
.@{my-selector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

#### 1.方法条件的筛选

less没有if else ，可是他有when

```
/* Less */
#card{
    
    // and 运算符 ，相当于 与运算 &&，必须条件全部符合才会执行
    .border(@width,@color,@style) when (@width>100px) and(@color=#999){
        border:@style @color @width;
    }

    // not 运算符，相当于 非运算 !，条件为 不符合才会执行
    .background(@color) when not (@color>=#222){
        background:@color;
    }

    // , 逗号分隔符：相当于 或运算 ||，只要有一个符合条件就会执行
    .font(@size:20px) when (@size>50px) , (@size<100px){
        font-size: @size;
    }
}
#main{
    #card>.border(200px,#999,solid);
    #card .background(#111);
    #card > .font(40px);
}
/* 生成后的 CSS */
#main{
  border:solid #999 200px;
  background:#111;
  font-size:40px;
}

```

#### 2.数量不定的参数

```less
/* Less */
.boxShadow(...){
    box-shadow: @arguments;
}
.textShadow(@a,...){
    text-shadow: @arguments;
}
#main{
    .boxShadow(1px,4px,30px,red);
    .textShadow(1px,4px,30px,red);
}

/* 生成后的 CSS */
#main{
  box-shadow: 1px 4px 30px red;
  text-shadow: 1px 4px 30px red;
}

```

#### 3.使用important

```less
.in{
	width:100px;
	
}
.wid{
	.in!important;
}
//编译之后
.wid{
  width:100px !important;  
}
```



#### 4.循环方式

```less
// 函数

.generate-column(@n,@i:1) when (@i=<@n){
    .column-@{i}{
        width:(@i*100%/@n);
    }
    .generate-column(@n,(@i+1));
}


/* 生成后的 CSS */
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
```

使用技巧

```
/* Less */
.average(@x, @y) {
  @average: ((@x + @y) / 2);
}

div {
  .average(16px, 50px); // 调用 方法
  padding: @average;    // 使用返回值
}

/* 生成的 CSS */
div {
  padding: 33px;
}
```



#### URLs

```less
// Variables
@images: "../img";

// Usage
body {
  color: #444;
  background: url("@{images}/white-sand.png");
}
```

*v1.6.0*

```less
@property: color;

.widget {
  @{property}: #0ee;
  background-@{property}: #999;
}
```

### 嵌套   常见

解决高度塌陷

你还可以使用此方法将伪选择器（pseudo-selectors）与混合（mixins）一同使用。下面是一个经典的 clearfix 技巧，重写为一个混合（mixin） (`&` 表示当前选择器的父级）：

```less
.clearfix {
  display: block;
  zoom: 1;

  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```

#### @规则嵌套和冒泡

媒体查询

@ 规则（例如 `@media` 或 `@supports`）可以与选择器以相同的方式进行嵌套。@ 规则会被放在前面，**同一规则集中的其它元素的相对顺序保持不变。这叫做冒泡（bubbling）。**

```less
.component {
  width: 300px;
  @media (min-width: 768px) {
    width: 600px;
    @media  (min-resolution: 192dpi) { //设备的分辨率
      background-image: url(/img/retina2x.png);
    }
  }
  @media (min-width: 1280px) {
    width: 800px;
  }
}
```



### 继承

#### 1.extend关键字的使用

```less
/* 生成后的 CSS */
.animation,#main{
  transition: all .3s ease-out;
}
.animation .hide , #con{
    transform:scale(0);
}
```

#### 2.减少代码的重复性

与上面的方法使用相比 减少了代码的复用性 但是extend存在一定的局限性

#### 3.要点

选择器和扩展之间 是允许有空格的：pre:hover :extend(div pre).

可以有多个扩展: pre:hover:extend(div pre):extend(.bucket tr) - 注意这与 pre:hover:extend(div pre, .bucket tr)一样。

这是不可以的，扩展必须在最后 : pre:hover:extend(div pre).nth-child(odd)。

如果一个规则集包含多个选择器，所有选择器都可以使用extend关键字。



### 运算（不常用）

### 函数

http://lesscss.cn/functions/ less函数链接

1.判断类型

isnumber

iscolor

isurl

2.颜色操作

3.数学函数

ceil 向上取整

floor  向下取整

### 其他

1.注释

- /* */ CSS原生注释，会被编译在 CSS 文件中。
- /  / Less提供的一种注释，不会被编译在 CSS 文件中。

2.避免编译

~‘ 值’

3.变量拼接

在平时工作中，这种需求 太常见了。 在下面例子中， 实现了不同的 transtion-delay、animation、@keyframes

```
.judge(@i) when(@i=1){
  @size:15px;
}
.judge(@i) when(@i>1){
  @size:16px;
}
.loopAnimation(@i) when (@i<16) {
  
  .circle:nth-child(@{i}){
      .judeg(@i);
      border-radius:@size @size 0 0;
      animation: ~"circle-@{i}" @duration infinite @ease;
      transition-delay:~"@{i}ms";
  }
  @keyframes ~"circle-@{i}" {
      // do something...
  }
  .loopAnimation(@i + 1);
}
复制代码
```

结构： `~"字符@{变量(i是可变的)}字符"`;

#### 4.使用js

因为 Less 是由 JS 编写，所以 Less 有一得天独厚的特性：代码中使用 Javascript 。

```
/* Less */
@content:`"aaa".toUpperCase()`;
#randomColor{
  @randomColor: ~"rgb(`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`)";
}
#wrap{
  width: ~"`Math.round(Math.random() * 100)`px";
  &:after{
      content:@content;
  }
  height: ~"`window.innerHeight`px";
  alert:~"`alert(1)`";
  #randomColor();
  background-color: @randomColor;
}
/* 生成后的 CSS */

// 弹出 1
#wrap{
  width: 随机值（0~100）px;
  height: 743px;//由电脑而异
  background: 随机颜色;
}
#wrap::after{
  content:"AAA";
}
复制代码
```




### 命名空间和访问符

```less
#bundle() {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white;
    }
  }
  .tab { ... }
  .citation { ... }
}
```

现在，如果我们希望把 `.button` 类混合到 `#header a` 中，我们可以这样做：

```less
#header a {
  color: orange;
  #bundle.button();  // 还可以书写为 #bundle > .button 形式
}
```



###  映射（Maps）a[i]

从 Less 3.5 版本开始，你还可以将混合（mixins）和规则集（rulesets）作为一组值的映射（map）使用。

```less
#colors() {
  primary: blue;
  secondary: green;
}

.button {
  color: #colors[primary];
  border: 1px solid #colors[secondary];
}
```

输出符合预期：

```css
.button {
  color: blue;
  border: 1px solid green;
}
```

###  作用域（Scope）

Less 中的作用域与 CSS 中的作用域非常类似。首先在本地查找变量和混合（mixins），如果找不到，则从“父”级作用域继承。

```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```

与 CSS 自定义属性一样，混合（mixin）和变量的定义**不必在引用之前事先定义**。因此，下面的 Less 代码示例和上面的代码示例是相同的：(等css加载完 再挂载)

```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```