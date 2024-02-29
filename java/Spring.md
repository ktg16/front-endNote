Spring

真实一点，好好学习努力赚钱，不要谈恋爱了

提供若干个项目 每个项目用于完成特定的功能

spring全家桶

Spring Framework系统架构

data Access 数据访问

Data Integration 数据集成

Web：web开发

Aop：面向切面编程

Aspects ： Aop思想实现

Core Container ：核心容器

Test：单元测试与集成测试

## 核心概念

### 控制反转。ioc

1.使用对象时。由主动new产生对象转换为由外部提供对象，此过程中对象创建控制权由程序转移到外部 

spring提供一个容器 IOC容器 充当Ioc思想中的外部

这一行为被称作 **Bean**

### di（denpendenvy injection）依赖注入

在容器中将有依赖关系的bean进行绑定di



1.删除使用new形式创建对象的代码

BookDao bookDao

不需要new形式来创建对象

1配置xml

常用

```

<bean id="bookService" class="com.itheima.service.impl.BookService">
        <!--    配置 service与dao的关系-->
<!--        name属性名称-->
        <property name="bookDao" ref="bookDao"></property>
    </bean>
    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl" ></bean>

```

### bean 作用范围说明

默认单例

表现层对象 业务层对象。数据层对象 工具对象 适合交给容器进行管理的bean

不适合 封装实体的域对象 domain

配置

![image-20230718142605711](/Users/duwenxuan/Library/Application Support/typora-user-images/image-20230718142605711.png)

bean生命周期

```
//初始化对应操作

//bean销毁前对应的操作
<bean id="bookService" class="com.itheima.service.impl.BookService" int-method="init" destroy-method = "destory" />
```

### 依赖注入方式

1.setter方式

提供一个set方法 如何用 property属性植入引用类型对象

简单类型 ref

引用类型 value

2.构造器注入

使用构造器形式注入

3.自动装配

```
<bean id="bookService" class="com.itheima.service.impl.BookService" autowire = "byType" />

```

4.集合注入

注入集合对象

### 数据源对象管理

容器

创建容器 获取bean。容器类层次结构。beanFactory

核心容器总结

### 注解

1.使用注解的形式修饰bean

```
<context />
@Reposity 仓库
@Controller//b
定义bean的作用范围

@scope（“singleton”）定义bean的作用范围
@autowired 自动装配  //需要按类型装配
@propertySource（文件,jdbcproperities）//不支持通配符
@Value（${name}）注入属性值 
```

2.纯注解开发

@configuration  配置类代表配置

@ComponentScan（“com.iteheima”） 扫描黑马

3.第三方bean管理  依赖注入



在某个类上使用@Component注解，表明当需要创建类时，这个被注解的类是一个候选类，就像是举手。

