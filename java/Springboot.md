Springboot 打包 运行可以快速运行。供前端使用

#### Idea中隐藏指定文件或指定类型文件

setting -> file types -> ignored files. And folders

输入要隐藏的文件名 支持*号通配符

回车确认添加

内置服务器

tomact 

jetty

undertow

#### rest开发

表现形式状态转换

传统风格资源描述形式

```
http://localhost/user/getById?id = 1
http://localhost/user/saveUser
```

Rest 风格描述形式

```
http://localhost/user/1
http://localhost/user
```

优点。隐藏资源的访问行为

书写简化



@RequestMapping 方法注解  设置当前控制器方法请求访问路径

value 请求访问路径

method http请求动作 标准动作

写在类开头

```
@ResponseBody  //用来返回JSON数据或者是XML数据
@RequestBody //接受json数据用于接受路径参数（请求体） 使用{参数名称} 描述路径参数
```

@getMapping @postMapping @PutMapping @DeleteMapping 方法注解



@GetMapping("/{id}")

value：请求访问路径

#### 复制工程

1.复制对应工程 并修改工程名称

2.删除与idea相关配置文件 仅保留src目录 与pom.xml文件

3.修改文件 artifactId与新工程 模块名相同

#### 配置文件

1.resources -> application.properties

2. resources 新建 application.yml. (1.主要写这个)

   ```
   server:
   port:81
   
   logging:  查日志							
   level
    root: info
   ```

3.新建 application.yaml

加载优先级 1 2 3

.yml 数据序列化格式（冒号后面要有空格）

1.易阅读 2.脚本语言交互 3.数据为核心 重数据格式

​		读取yaml数据

@Value("${country}")

private String country1；



##### 读取 yml全部属性

@Aurowired //自动装配。所有配置信息装配到对象

private Environment env;



//读取yml的一部分 

定义为spring管控的bean(必须被Spring管控)

@Compont

指定加载的数据

@ConfigurationProperties("datasource") //绑定配置信息到封装类

# 整合第三方技术

学习其思想

1.junit

精准的配置springBoot的启动类

2.mybatis    

选择mysql。mybatis

1.导入对应starter

2.配置相关信息（数据源相关信息）

dao包数据层 数据库相关操作 数据访问。

domain 实体类

container 控制层

service 在此层做相应的业务逻辑处理。

web包 一般存放 servlet filter

impl包 放置接口的实现类

3.domain

4。接口连接

@mapper

@Select

3.mybatis-plus

操作mysql

4.spring整合 Druid

数据连接池

```
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.6</version>
</dependency>
```

```
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/new_schema?serverTimezone=UTC
      username: root
      password: 88888888
```

5.ssm 整合案列

手工导入 starter坐标 

配置数据源与myBatisPlus对应的配置

开发Dao接口继承BaseMapper

制作测试类测试Dao功能是否有效

看springbooy项目

### mp开启日志





问题： 服务器一些问题

​			nginx部署项目；

​			jar部署

个人发展问题： 

veo

发展方向
