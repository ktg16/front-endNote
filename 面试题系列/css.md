## 介绍一下Flex的各个属性，以及原理？

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。![bg2015071004](.\bg2015071004.png)

(上面是了解，下面是重点)

### flex属性

​	1.flex-direction  决定主轴的方向

​     flex-direction:row(水平方向) row-reverse column(垂直方向) column-reverse

​	2.flex-wrap  是否换行  （当一条轴线排不下时如何换行）

```css
flex-wrap: nowrap | wrap | wrap-reverse（第一行在下方）;
}
```

3.flex-flow

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值 row direction

```css
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

4.justify-content属性  定义了项目(容器)在主轴上的对齐方式。

justify-content：flex-start | flex-end | center | space-between（两端对齐，项目之间的间隔都相等  两边无间隔，中间间隔大） | space-around（每个项目两侧的间隔相等）;

5. align-items

```css
lign-items: flex-start | flex-end | center | baseline | stretch;
```

- `flex-start`：交叉轴的起点对齐。

- `flex-end`：交叉轴的终点对齐。

- `center`：交叉轴的中点对齐。

- `baseline`: 项目的第一行文字的基线对齐。

- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

  6.`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```css
align-content: flex-start | flex-end | center | space-between（与交叉轴两端对齐，轴线之间的间隔平均分布） | space-around | stretch(默认值 轴线占满整个字符串);
```

### 项目的属性（也就是子元素属性）

**order**属性 定义元素的排列顺序。数值越小 排列越靠前

```css
.item {
  order: <integer>;
}
```

**flex-grow**属性  定义元素的放大比例  默认为0 即如果存在剩余空间，也不放大。

```css
.item {
  flex-grow: <number>; /* default 0 */
}
```

**flex-shrink**属性  定义了项目缩小的比例 默认为1  即如果空间不足，该项目将缩小。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

**flex-basis**属性 定义在分配剩余空间之前，项目占据的主轴空间。根据这个属性浏览器计算主轴是否有多余的空间。 它的默认值是auto即项目本来的大小

```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

可以设置为固定的大小例（350px）项目占据固定空间

4-5.flex属性

​		flex是flex-grow，flex-shrink，flex-basis的简写默认值为0 1 auto

该属性有两个快捷值：`auto` (`1 1 auto`) 也就是flex:1(1 1 auto)和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

4-6.aligin-self属性  允许单个项目有与其他项目不一样的对齐方式，可覆盖align-item属性。默认值为auto 继承父元素align-item的属性如果没有父元素则等同于stretch

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

flex布局

https://www.ruanyifeng.com/blog/2015/07/flex-examples.html

## 三栏布局方式两边固定中间自适应？

margin 负值法：左右两栏均左浮动，左右两栏采用负的 margin 值。中间栏被宽度为 100%的浮动元素包起来 

自身浮动法：左栏左浮动，右栏右浮动，中间栏放最后 

绝对定位法：左右两栏采用绝对定位，分别固定于页面的左右两侧，中间的主体栏用 左右 margin 值撑开距离。 

flex 左右固定宽 中间 flex：1



双飞翼布局

双飞翼布局与圣杯布局的不同之处，圣杯布局的的左中右三列容器，中间middle多了一个子容器存在，**通过控制 middle 的子容器的 margin 或者 padding 空出左右两列的宽度**。

圣杯布局

圣杯布局的的左中右三列容器没有多余子容器存在，通过控制父元素的 padding 空出左右两列的宽度。

## 如何设置背景色

当需要给页面设置一个背景色时  必须给父元素设置 height:100%；display:flex 再给子元素使用 flex:1