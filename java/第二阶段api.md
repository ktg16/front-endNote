实现梦想 

### Math 类方法



| 方法      |                                     |
| --------- | :---------------------------------: |
| abs       |               绝对值                |
| pow       |                求幂                 |
| ceil      | 向上取整 返回大于等于该参数最小整数 |
| floor     |              向下取整               |
| round     |              四舍五入               |
| sqrt      |               求开方                |
| random    |               随机数                |
| max , min |         返回最大值和最小值·         |

random计算公式：(int)(a + Math.random() * (b-a +1) )

### Arrary类方法

```
1.toString 返回数组的字符串形式

Arrays.toString(arr)

2.sort排序（自然排序/定制排序）
Arrays.sort(arr)
// 第二个参数传入匿名内部类
Arrays.sort(arr,new Comparator(){
  public int compare(object o1,object o1){
			Integer i1 = (Integer) o1;
			Integer i2 = (Integer) o2;
			return i2 - i1; //倒叙  二叉排序 //主要是这个地方起作用
			
  }
})

3.BinarySearch 通过二分搜索法查找（要求：有序）
// 想看源码去看视频
int index = Array.binarySearch(arr,3)
4.copyOf 数组元素的复制
Integer[] newArr = Arrays.copyOf(arr.length);

5.fill 数组元素的填充
Integer[] num = new Integer[]{9,3,2}
Arrays.fill(num,88) // 全部都是99了
6.equals 比较两个数组元素内容是否完全一致
 boolean equals  = Arrays.equals(arr,arr2)
7.asList 将一组值，装换成list
//1. asList 方法，会将 (2,3,4,5,6,1)数据转成一个 List 集合
//2. 返回的 asList 编译类型 List(接口)
//3. asList 运行类型 java.util.Arrays#ArrayList, 是 Arrays 类的
// 静态内部类 private static class ArrayList<E> extends AbstractList<E> // implements RandomAccess, java.io.Serializable
List<Integer> asList = Arrays.asList(2,3,4,5,6,1);
```

### System类

```
1.System.exit 退出当前程序
2.System.arratcopy //适合底层使用
arratcopy(源数组，源数组起始位置，目标数组，目标数组起始位置，要复制数组元素数量)
3.System.currentTimeMillens:返回当前时间距离1970-1-1毫秒数
4.gc：运行垃圾回收机制 System.gc()

```

### BigInteger 和 BigDecimal 类

BigInteger适合保存比较大的整型(long 不否用的时候)

BigDecimal 适合保存精度更高 浮点数

```
1.add 加
bigInteger.add(bigInteger2);
2.subtract 减
3.multiply 乘
4.divide 除
```

### 日期类

```
1.Date
	Date d1 = new Date() 获取当前系统时间
	
2.SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E")	
String format = sdf.fotmat(d1);//format 将提起转换成指定格式的字符串
//1. 可以把一个格式化的 String 转成对应的 Date
//2. 得到 Date 仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转换
//3. 在把 String -> Date ， 使用的 sdf 格式需要和你给的 String 的格式一样，否则会抛出转换异常

String s = "1996 年 01 月 01 日 10:20:30 星期一";
Date parse = sdf.parse(s);
```

https://www.163.com/dy/article/I6Q1DNLI0553CV3H.html

#### 第二代日期类Calendar

//1. Calendar 是一个抽象类， 并且构造器是 private 

//2. 可以通过 getInstance() 来获取实例
 //3. 提供大量的方法和字段提供给程序员

//4. Calendar 没有提供对应的格式化的类，因此需要程序员自己组合来输出(灵活)
 //5. 如果我们需要按照 24 小时进制来获取时间， Calendar.HOUR ==改成=> Calendar.HOUR_OF_DAY

```
				System.out.println(c.get(Calendar.YEAR));
        System.out.println(c.get(Calendar.MONTH + 1));
        System.out.println( c.get(Calendar.DAY_OF_MONTH));
        System.out.println(c.get(Calendar.HOUR));
        System.out.println(c.get(Calendar.MINUTE));
        System.out.println(c.get(Calendar.SECOND));
```

#### 第三代日期类LocalDate

```

LocalDateTime ldt = LocalDateTime.now(); //LocalDate.now();//LocalTime.now()
//格式化代码
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"); String format = dateTimeFormatter.format(ldt);
        System.out.println("格式化的日期=" + format);
        System.out.println("年=" + ldt.getYear());
        System.out.println("月=" + ldt.getMonth());
        System.out.println("月=" + ldt.getMonthValue());
        System.out.println("日=" + ldt.getDayOfMonth());
        System.out.println("时=" + ldt.getHour());
        System.out.println("分=" + ldt.getMinute());
        
   LocalDate now = LocalDate.now(); //可以获取年月日    
   LocalTime now = LocalTime.now();//时间
   
   // plus和minus 可以对时间进行加减
   
   LocalDateTime a = ldt.plusDays(100)
   
   LocalDateTime a = ldt.plusYears(100)
   localDateTime b = ldt.minusMinutes(3456)     
        
```

DateTimeFormatter  格式日期类

DateTimeFormatter dtf = DateTimeFormatter.ofPatten("")

String strDate = def.format(Idt)







### Instant时间戳

```
				Instant now  = Instant.now();
        System.out.println(now);
        Date date = Date.from(now);
        System.out.println(date);
        Instant instant = date.toInstant();
```



当if判断时可以使用。!正确判断. 也可以直接判断错误

### 集合

特点：可以保存任意对象,使用方便、提供一系列方便操作对象的方法 add、remove、set、get等

使用集合添加 删除新元素的代码

集合框架体系⚠️

![image-20230612152852970](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230612152852970.png)

Collection接口实现类的特点

1.实现子类存放多个元素 ，元素可以是object

2.存放重复的元素。有些不可以

3.有些有序的 List 有些不是有序的 Set

4.没有直接的实现子类，是通过它的子接口Set和list来实现的

```
//1. 集合主要是两组(单列集合（单列数据） , 双列集合（双列数据）)
//2. Collection 接口有两个重要的子接口 List Set , 他们的实现子类都是单列集合 
//3. Map 接口的实现子类 是双列集合，存放的 K-V
ArrayList arrayList = new ArrayList();
arrayList.add("jack") 
arrayList.add("tom");
list.remove(0)//删除第一个元素
list.remove(true)//删除某个元素
list.contains() //查找元素是否存在
list.size() //元素个数
list.isEmpty()//判断是否为空
list.clear()//清空
list.addAll(list2)//添加多个元素

list.contains(list2)// 查找多个元素都存在
list.removeAll(list2)// 删除多个元素
HashMap hashMap = new HashMap();
hashMap.put("No1","北京");
hashMap.put("No2","上海");
```



#### Iterator(迭代器)

![image-20230613084001595](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230613084001595.png)

```
Collection col = new ArrayList();
Iterator iterator = col.iterator();
//老师教大家一个快捷键，快速生成 while => itit //显示所有的快捷键的的快捷键 ctrl + j

while (iterator.hasNext()) {
	Object obj = iterator.next(); 
	System.out.println("obj=" + obj);
}
//3. 当退出 while 循环后 , 这时 iterator 迭代器，指向最后的元素 // iterator.next();//NoSuchElementException
//4. 如果希望再次遍历，需要重置我们的迭代器
iterator = col.iterator();
  System.out.println("===第二次遍历===");
  while (iterator.hasNext()) {
  Object obj = iterator.next(); System.out.println("obj=" + obj);
}

```

使用 for循环增强 遍历对象方式

```
for (Object dog : list) {

	System.out.println("dog=" + dog); 

}
```

#### List接口

```
//1. List 集合类中元素有序(即添加顺序和取出顺序一致)、且可重复 [案例]
//2. List 集合中的每个元素都有其对应的顺序索引，即支持索引
//3.根据序号取出
//实现类有 ArrayList LinkedList 和Vector
```

常用方法

```
//void add(int index, Object ele):在 index 位置插入 ele 元素 
//在 index = 1 的位置插入一个对象
list.add(1, "韩顺平");
boolean addAll(int index, Collection eles):
从 index 位置开始将 eles 中的所有元素添加进来 List list2 = new ArrayList();
list2.add("jack");
list2.add("tom");
list.addAll(1, list2);
System.out.println("list=" + list);
Object get(int index):获取指定 index 位置的元素 
//说过
int indexOf(Object obj):返回 obj 在集合中首次出现的位置 System.out.println(list.indexOf("tom"));//2
int lastIndexOf(Object obj):返回 obj 在当前集合中末次出现的位置 list.add("韩顺平");
System.out.println("list=" + list); System.out.println(list.lastIndexOf("韩顺平"));
Object remove(int index):移除指定 index 位置的元素，并返回此元素 
list.remove(0);
System.out.println("list=" + list);
Object set(int index, Object ele):设置指定 index 位置的元素为 ele , 相当于是替换. 
list.set(1, "玛丽");
System.out.println("list=" + list);
List subList(int fromIndex, int toIndex):返回从 fromIndex 到 toIndex 位置的子集合 // 注意返回的子集合 fromIndex <= subList < toIndex
List returnlist = list.subList(0, 2);
```

List的三种遍历方式

```
Iterator iterator = list.iterator(); 
while (iterator.hasNext()) {
	Object obj = iterator.next(); System.out.println(obj);
}
System.out.println("=====增强 for====="); //2. 增强 for
for (Object o : list) {
System.out.println("o=" + o); }
  for(int i=0;i<list.size();i++){
  System.out.println(list.get(i))
}
```



ArrayList不带有synchronized 不支持线程同步 多线程不建议使用 

Vetor类带有synchronized



电影无问西东有一句台词，如果提前知道你将面对的人生，你是否还有勇气重来一遍？

我在很多地方引用过艾比克泰德的这句话，我们登上并非我们所选择的舞台，演出并非我们所选择的剧本

艾森豪威尔的母亲从小就对他说，人生就像打牌，无论你抓到一副多么烂的牌，都要把它打好。

也许棋手烂牌也会有精彩的结局。

堕落天使路西法这个魔鬼隐藏在每个人内心深处，凡动刀者，必死于刀下

生活远比戏剧更荒诞与沉重，但荒诞不是让我们绝望，而是让我们重新滋生勇气与信心。
