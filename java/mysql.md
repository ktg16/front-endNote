mysql的使用

### 数据模型

关系型数据库：由多张相互连接的二维表组成的数据

mysql -uroot  -p

根据原型+需求文档。 项目中数据库所需要的操作

 1.数据库设计

2.数据库操作（java）

3.数据库优化

https://juejin.cn/post/6844904196383195144#heading-2

https://juejin.cn/post/6844904037536514062#heading-8

https://juejin.cn/post/6847902223616180238#heading-3

不错的笔记

https://juejin.cn/post/6952389513255747592#heading-8

#### ddl语句

数据定义语言，用来操作数据库、表、列等； 常用语句

很多语法都重复。不过多重写了

select database(); 查看当前使用的数据库

为防止错误的数据被插入到数据表，MySQL中定义了一些维护数据库完整性的规则；这些规则常称为表的约束。常见约束如下：

### 约束条件	说明

PRIMARY KEY	主键约束用于唯一标识对应的记录（一般id使用）
FOREIGN KEY	外键约束
NOT NULL	非空约束
UNIQUE	唯一性约束。唯一
DEFAULT	默认值约束，用于设置字段的默认值
以上五种约束条件针对表中字段进行限制从而保证数据表中数据的正确性和唯一性。换句话说，表的约束实际上就是表中数据的限制条件。	
字段

auto increment(ai) 字段自增

### DML 数据操作语言



1.给表插入值时。需要给值传入更新时间与创建时间。直接设置为 now()即可

### DQL数据库的操作

#### 数据查询语言 select



查询多个字段。 select 字段1 字段2 字段3。from 表名

查询所有字段。  select * from 表名

设置别名。 select 字段1 [as 别名1], 字段2

去除重复记录 select distinct 字段列表 from 表名；

#### 条件查询 where

查询null。 where job is null/is not null；

不等于  where password <> '123456' / !='123456 '

查询范围 where entry between '2000-01-01' and '2010-01-01 '

查询范围 且 性别为女

where entry between '2000-01-01' and '2010-01-01 '  and gender =2；

查询 很多并列条件。or

where job =2 or job= 3 or job =4 / where job in(2,3,4)

查询两个字的信息。where name like '__';

查询 姓张信息。where name like '张%'；（模糊查询）

![image-20230711164641932](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230711164641932.png)

#### 聚合函数 count(*)

![image-20230711171117780](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230711171117780.png)

select max(id) from tb_emp;

Select avg(id) from tb_emp; 



#### -- 分组查询 group by

select gender，count(*) from tb_emp  group by gender;

gender是分组字段。count(*)//统计数量

 select job,count(*) from tb_emp where entry date <='2015-01-01' by job having count( *)>2;

![image-20230711172850966](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230711172850966.png)

分组之后。查询字段一般为聚合函数和分组字段。查询其他字段无任何意义

执行顺序 where > 聚合函数 > having 

分组后条件查询  having by

#### 排序查询 order by

select * from tb_emp order by entrydate asc;（可省略） 升序排序/降序排序

select * from tb_emp order by entry date , update desc;

#### 分页查询（limit）

select * from tb_emp limit 0,5;

select * from tb_emp limit 5,5（每页展示5条） 第二页员工数据。 

select * from tb_emp limit 10,5

#### 案例查询

1.表格查询 

姓名 模糊匹配（like）

性别。入职日期 分页 倒序

select * from tb_emp where name like '%张%'（代表任意字符） and gender =1  and entrydate between '2000-01-01' and '2010-01-01 ' order by  update_time desc(排序方式)   limit 0，10（分页） ；

2.员工性别统计

select * if(gender  = 1，‘男性员工’，‘女性员工’) ,count(*)  from tb_emp group by gender;

2-2 员工职位信息统计

case 表达式 when 值1   then 结果1 when 值2 then 值2  else.... end

// 值修改成表达式



select (case job when 1 then '班主任' when 2 then '讲师' when 3 then '学生主管' when 4 then '教研主管' else ‘未分配职位’ end) from tb_emp group by job



### 多表设计

一对多的设计

部门表与员工表。

父表与子表

### 多表查询

内链接

隐式内链接: select. 字段列表 from 表1，表2  where 条件。。（表名.dept_id  = 表名.id）；//用于

显式内链接: select  字段列表 from 表1[inner] join表2 on 连接条件

外链接

左外链接： select 字段列表 from 表1 left[outer]（关键字outer可省略）  join 表2 on 连接条件..；

右外链接:   select 字段列表。from 表1 right[outer] join 表2 on 连接条件

左外连接和右外连接的区别：
左外连接也称左连接。以左表为基表，在FROM子句中使用关键字“LEFT OUTER JOIN”或关键字“LEFT JOIN”来连接两张表。
右外连接也称右连接。以右表为基表，在FROM子句中使用关键字“RIGHT OUTER JOIN”或关键字“RIGHT JOIN”来连接两张表。
————————————————
版权声明：本文为CSDN博主「花开盛夏^.^」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_45639224/article/details/127212857

子查询（嵌套查询）

标量子查询

列子查询

行子查询

select * from tb_emp where( entry date,job)  = (select entrydate ,job from tb_emp where name = 'weiyixiao ')

表查询

查询入职日期xxx 之后员工信息及其部门信息



select e.*,d.name   from （select * from where entrydate > '2006-01-01' ）e, tb_dept d where e.dept_id = d.id//作为临时表

e是临时表

e,d是简写



#### 案例2

联查

select s.name,s.price,d.name,d.price,sd.copies  from  setmeal s ， setmeal_dish sd , dish d where s.id  = sd.setmeal_id and d.id = sd.dish_id and s.name = '套餐A' 

### 事务

介绍: 一组操作的集合 这组操作要么全部成功 要么全部失败

开启事务： start transaction; /begin;

提交事务： commit

回滚事务：rollback

四大特性 ： 原子性 一致性。隔离性 持久性

### 索引

帮助数据库高效获取数据的数据结构

提升效率做有效的操作

创建索引

create index idx_sku on tb_sku(sn); 	表名(字段)

优点: 1.提升效率做有效的操作,降低数据库的io成本

2.通过索引列对数据进行排序。降低数据排序的成本

缺点： 占用存储空间 提高查询效率 降低 inset update delete效率