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
```





















电影无问西东有一句台词，如果提前知道你将面对的人生，你是否还有勇气重来一遍？

我在很多地方引用过艾比克泰德的这句话，我们登上并非我们所选择的舞台，演出并非我们所选择的剧本

艾森豪威尔的母亲从小就对他说，人生就像打牌，无论你抓到一副多么烂的牌，都要把它打好。

也许棋手烂牌也会有精彩的结局。

堕落天使路西法这个魔鬼隐藏在每个人内心深处，凡动刀者，必死于刀下

生活远比戏剧更荒诞与沉重，但荒诞不是让我们绝望，而是让我们重新滋生勇气与信心。
