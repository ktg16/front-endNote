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



电影无问西东有一句台词，如果提前知道你将面对的人生，你是否还有勇气重来一遍？

我在很多地方引用过艾比克泰德的这句话，我们登上并非我们所选择的舞台，演出并非我们所选择的剧本

艾森豪威尔的母亲从小就对他说，人生就像打牌，无论你抓到一副多么烂的牌，都要把它打好。

也许棋手烂牌也会有精彩的结局。

堕落天使路西法这个魔鬼隐藏在每个人内心深处，凡动刀者，必死于刀下

生活远比戏剧更荒诞与沉重，但荒诞不是让我们绝望，而是让我们重新滋生勇气与信心。
