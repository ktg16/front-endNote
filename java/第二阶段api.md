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

#### ArrayList

ArrayList不带有synchronized 不支持线程同步 多线程不建议使用 

![]()

![image-20230614095753336](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230614095753336.png)

源码分析请查看附录 



#### Vetor

Vetor类带有synchronized

![image-20230614102948210](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230614102948210.png)

#### LinkedList

1.LinkedList底层实现了双向链表和双端队列特点

2.可以添加任意元素（元素重复） 包括null

3.线程不安全

LinkedList的底层操作机制

![image-20230614084934951](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230614084934951.png)

```
//模拟一个简单的双向链表
Node jack = new Node("jack"); 
Node tom = new Node("tom"); 
Node hsp = new Node("老韩");
//连接三个结点，形成双向链表 //jack -> tom -> hsp
jack.next = tom;
tom.next = hsp;
//hsp -> tom -> jack 
hsp.pre = tom; 
tom.pre = jack;
 while (true){
            if(first == null){
                break;
            }
            System.out.println(first);
            first = first.next;
        }
        while (true){
            if(last  == null){
                break;
            }
            System.out.println(last);
            last = last.pre;
        }
```

LinkedList增删改查

```

//修改某个结点对象
linkedList.add(1);
linkedList.remove(2)
linkedList.set(1, 999);
linkedList.get(1)
System.out.println("===LinkeList 遍历迭代器===="); Iterator iterator = linkedList.iterator();
while (iterator.hasNext()) {
Object next = iterator.next(); System.out.println("next=" + next);
}
System.out.println("===LinkeList 遍历增强 for===="); 
for (Object o1 : linkedList) {
System.out.println("o1=" + o1); }
System.out.println("===LinkeList 遍历普通 for===="); 
for (int i = 0; i < linkedList.size(); i++) {
System.out.println(linkedList.get(i)); }
```



#### 实际开发中如何选择List

![image-20230613170734988](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230613170734988.png)

如何选择

1.改查。ArrayList

2.增删  LinkedList

3.大部分是查询。选择ArrayList  

4.一个模块使用的是ArrayList。另一个模块是LinkedList



#### Set

特点

```
//1. 以 Set 接口的实现类 HashSet 来讲解 Set 接口的方法
//2. set 接口的实现类的对象(Set 接口对象), 不能存放重复的元素, 可以添加一个 null 
//3. set 接口对象存放数据是无序(即添加的顺序和取出的顺序不一致)  没有索引
//4. 注意:取出的顺序的顺序虽然不是添加的顺序，但是他的固定.
Set  set = new HashSet();

        set.add("123");
        set.add(123);
        set.add(null);

        for (int i = 0; i < 10; i++) {
            System.out.println("0:"+set);
        }
        //遍历
        for(Object o:set){
            System.out.println(o);
        }
        Iterator iterator = set.iterator();
        while (iterator.hasNext()){
            Object obj = iterator.next();
            System.out.println("obj=" + obj);
        }
        set.size();
    }

```

Set接口类 HashSet

上面基本讲解了HashSet特点

Hash实际上是HashMap

有源码部分建议回头来看

```
使用Set需要使用重写 equals和 hashCode代码
 @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return sal == employee.sal && Objects.equals(name, employee.name) && Objects.equals(birthday, employee.birthday);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, sal, birthday);
    }
```





#### Map

源码解析视频

https://www.bilibili.com/video/BV1fh411y7R8/?p=532&spm_id_from=pageDriver&vd_source=75e113dec8efe1f136750d6e690b5075https://www.bilibili.com/video/BV1fh411y7R8/?p=532&spm_id_from=pageDriver&vd_source=75e113dec8efe1f136750d6e690b5075



```
//1. Map 与 Collection 并列存在。用于保存具有映射关系的数据:Key-Value(双列元素)
//2. Map 中的 key 和 value 可以是任何引用类型的数据，会封装到 HashMap$Node 对象中 //3. Map 中的 key 不允许重复，原因和 HashSet 一样，前面分析过源码.
//4. Map 中的 value 可以重复
//5. Map 的 key 可以为 null, value 也可以为 null ，注意 key 为 null,只能有一个，value 为 null ,可以多个
//6. 常用 String 类作为 Map 的 key
//7. key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到对应的 value
```

```
//map方法
Map map = new HashMap();
      1.  map.put("邓超","12345");
        map.put("邓超",45);
       2. map.remove("邓超");
        map.put("孙俪",333);
        map.put("hsp",333);
			3.	map.get("邓超")
        Object val =  map.get("鹿晗");
        //获取元素个数
        map.size();
        //判断是否0
        map.isEmpty();
        //containsKey 查找键是否存在
        map.containsKey("hsp");
        // clear清除
        map.clear();
```

map遍历方法

```
        //通过key获取val
        Set keyset = map.keySet();
        //增强for
        for(Object o:keyset){
            System.out.println(o+"-"+map.get(o));
        }
        //2.迭代器
        Iterator iterator = keyset.iterator();

        while (iterator.hasNext()){
            Object key = iterator.next();
            System.out.println(key+"-"+map.get(key));
        }
        // 把所有values取出
        Collection values = map.values();
        for(Object o :values){
            System.out.println(o);
        }
        //迭代器取出value
        Iterator iterator1 = values.iterator();
        while (iterator1.hasNext()){
            Object value = iterator1.next();
            System.out.println(value);
        }
        //entrySet获取k-v
        Set entrySet = map.entrySet();
        for (Object set:entrySet){
            Map.Entry m = (Map.Entry) set;
            System.out.println(m);
        }
        while (iterator.hasNext()){
// Map.entrySet() 这个方法返回的是一个Set<Map.Entry<K,V>>，Map.Entry 是Map中的一个接口，
//他的用途是表示一个映射项（里面有Key和Value），而Set<Map.Entry<K,V>>表示一个映射项的Set。
//Map.Entry里有相应的getKey和getValue方法，即JavaBean，让我们能够从一个项中取出Key和Value。
            System.out.println(iterator.next()+"sss");
            Map.Entry entry = (Map.Entry) iterator.next();
            Emp emp = (Emp) entry.getValue();
            if(emp.getSal() > 18000) {
                System.out.println(emp); }
        }
```

hashtable

1.键和值都不能为null。

2.使用方法与hashmap一致

3.线程安全

#### 集合的选择

![image-20230619135427059](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230619135427059.png)

treeMap。treeSet

```
TreeMap treeMap = new TreeMap(new Comparator() {//使用一个比较器
  @Override
  public int compare(Object o1, Object o2) {
  //按照传入的 k(String) 的大小进行排序
  //按照 K(String) 的长度大小排序
  //return ((String) o2).compareTo((String) o1); 
  return ((String) o2).length() - ((String) o1).length();
} });
```

#### Collections工具类

1.collections 是一个操作Set List map等集合的工具类

2.存在一系列静态的方法对集合元素进行排序 查询 修改

排序操作。均为static方法



reverse(List) 反转List元素的顺序

shuffle(List)对List集合元素进行随机排序

sort。升序

sort(List,Comparator): 根据指定Comparator产生的顺序对List集合元素怒进行排序

swap(List,int,int) 将制定list集合中的i处元素和j处元素进行交换



Collections.max(list)  返回给定集合中的最大元素

max(list,Comparator)

min(list) 返回最小元素



Frequency(list,object)  返回指定集合中指定元素出现次数



Copy(List dest,List src);   将内容复制到dest中

 replaceAll(List list，Object oldVal，Object newVal)  使用新值替换List对象的所有旧值

Collections.replaceAll(list, "tom", "汤姆");









![image-20230619165246530](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230619165246530.png)

泛型的好处

1.编译时，检查添加元素的类型 提高安全性

2.减少了类型转换的次数。提高效率

3.不提示编译警告















电影无问西东有一句台词，如果提前知道你将面对的人生，你是否还有勇气重来一遍？

我在很多地方引用过艾比克泰德的这句话，我们登上并非我们所选择的舞台，演出并非我们所选择的剧本

艾森豪威尔的母亲从小就对他说，人生就像打牌，无论你抓到一副多么烂的牌，都要把它打好。

也许棋手烂牌也会有精彩的结局。

堕落天使路西法这个魔鬼隐藏在每个人内心深处，凡动刀者，必死于刀下

生活远比戏剧更荒诞与沉重，但荒诞不是让我们绝望，而是让我们重新滋生勇气与信心。

证书

https://www.sohu.com/a/573939453_120174355

上线应用商店需要研究



1、什么时候把程序跑起来，手机还给他。   ===》 这个原计划好像就是最近了
2、什么时候上线应用商店。                        ===》 这个没计划，2个月或者明天以后再说？ 
3、什么时候上线语音通话功能。                 ===》这个你看着编吧。。。
4、什么时候上线设备功能。                        ===》 这个工作量好像不小，估计有个20来个页面的样子，主要还得调蓝牙
