拒绝拖延

## 简介

Nginx是一款轻量级的Web服务器、反向代理服务器，由于它的内存占用少，启动极快，高并发能力强，在互联网项目中广泛应用。（专为性能优化而开发）

Nginx只是**一个静态文件服务器或者http请求转发器**，它可以把静态文件的请求直接返回静态文件资源，把动态文件的请求转发给后台的处理程序，例如php-fpm、apache、tomcat、jetty等，这些后台服务，即使没有nginx的情况下也是可以直接访问的（有些时候这些服务器是放在防火墙的面，不是直接对外暴露，通过nginx做了转换）。

对于前端来说 Node.js 不陌生了，Nginx 和 Node.js 的很多理念类似，**HTTP 服务器、事件驱动、异步非阻塞等**，且 Nginx 的大部分功能使用 Node.js 也可以实现，但 Nginx 和 Node.js 并不冲突，都有自己擅长的领域。Nginx 擅长于**底层服务器端资源的处理（静态资源处理转发、反向代理，负载均衡等）**，Node.js 更擅长上层具体业务逻辑的处理，两者可以完美组合，共同助力前端开发。

https://juejin.cn/post/6844904144235413512  掘金地址



 一般的访问流程是客户端直接向目标服务器发送请求并获取内容，

## 正向代理与反向代理

 反向代理（Reverse Proxy）对应的是正向代理（Forward Proxy）

**正向代理：** 一般的访问流程是客户端直接向目标服务器发送请求并获取内容，使用正向代理后，客户端改为向代理服务器发送请求，并指定目标服务器（原始服务器），然后由代理服务器和原始服务器通信，转交请求并获得的内容，再返回给客户端。正向代理隐藏了真实的客户端，为客户端收发请求，使真实客户端对服务器不可见；

(不能够直接去获得www.gogle.com,通过代理服务器来代替)



**反向代理：**与一般访问流程相比，使用反向代理后，直接收到请求的服务器是代理服务器，然后将请求转发给内部网络上真正进行处理的服务器，得到的结果返回给客户端。反向代理隐藏了真实的服务器，为服务器收发请求，使真实服务器对客户端不可见。一般在处理跨域请求的时候比较常用。现在基本上所有的大型网站都设置了反向代理。



## 负载均衡

一般情况下，客户端发送多个请求到服务器，服务器处理请求，其中一部分可能要操作一些资源比如数据库、静态资源等，服务器处理完毕后，再将结果返回给客户端。

请求爆发式增长的情况下，单个机器性能再强劲也无法满足要求了，这个时候集群的概念产生了，**单个服务器解决不了的问题，可以使用多个服务器，然后将请求分发到各个服务器上，将负载分发到不同的服务器**，这就是**负载均衡**，核心是「分摊压力」。Nginx 实现负载均衡，一般来说指的是**将请求转发给服务器集群。**



## 动静分离

一般来说，都需要将动态资源和静态资源分开，由于 Nginx 的高并发和静态资源缓存等特性，经常将静态资源部署在 Nginx 上。如果请求的是静态资源，直接到静态资源目录获取资源，**如果是动态资源的请求，则利用反向代理的原理，把请求转发给对应后台应用去处理，从而实现动静分离。**



## **nginx配置高可用集群**

## Nginx的一些常用指令

```
ifconfig  查看ip
nginx -t // 检查nginx的配置是否ok
nginx -s reload 重新加载
nginx -s stop
vim nginx.conf 查看文件 i 修改
:wq 保存
ps -ef|grep nginx nginx进程

sbin/nginx -t -c conf/nginx.conf # 检测配置文件是否正常
sbin/nginx -s reload -c conf/nginx.conf # 修改配置后平滑重启
sbin/nginx -s quit # 优雅关闭Nginx，会在执行完当前的任务后再退出
sbin/nginx -s stop # 强制终止Nginx，不管当前是否有任务在执行

```



## 开启 gzip 压缩

## 2.1安装nginx（虚拟机必须关闭防火墙或者把端口暴露出来）

ll 查看文件内容

1.用连接工具(xshell)远程连接操作系统（需要创建虚拟机）

2.安装依赖 （4个依赖包）

3.解压 压缩包 解压之后才能够安装

4.编译之前  创建nginx临时目录  如果不创建 在启动nginx的过程会报错

5.在nginx目录 输入命令进行配置  目的是为了创建 **makefile文件**

```
./configure \
--prefix=/usr/local/nginx \
--pid-path=/var/run/nginx/nginx.pid\
--lock-path=/var/locl/nginx.lock\
--error-log-path=/var/log/nginx/error.log\
--http-log-path=/var/log/nginx/accrss.log\
--with-http_gzip_static_module\
--http-client-body-temp-path=/var/temp/nginx/client\
--http-proxy-temp-path=/var/temp/nginx/proxy\
--http-fastcgi-temp-path=/var/temp/nginx/fastcgi\
--http-uwsgi-temp-path=/var/temp/nginx/uwsgi\
--http-scgi-temp-path=/var/temp/nginx/scgi
; 
指定nginx 安装目录
指向nginx的pid
锁定安装文件 防止被恶意篡改或者误操作
错误日志
http日志
启用gzip模块  在线实时压缩输出流数据流
设定客户端请求的临时目录
设定http代理临时目录等。。。
temp-path 设定临时的目录
```

设置一些临时目录



6.通过makefile来进行make 编译

```
make
```

8.安装

```
make install
```

9. 进入sbin目录查看nginx 是否安装

   sbin目录下的nginx

   访问ip  

以上内容暂时不用

nginx 的端口被占有如何解决

重启nginx

### Nginx的进程

master进程  管理（可以监控worker 指派工作）

worker进程  工作

### Nginx.conf的配置结构 

配置文章  https://juejin.cn/post/6844903741678698510

1.main全局配置 

2.event 配置工作模式以及连接数

3.http模块相关配置

include 导入（提高模块性）

accerss_log  xxx 记录在xxx里

sendfile 发送文件 默认on

tcp_nopush当数据包一定大小再送

keepalive_timeout 超时时间

​	server 虚拟机配置

​		location 路由规则

​		upstream 集群 内网服务器