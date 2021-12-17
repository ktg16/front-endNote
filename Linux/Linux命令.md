监控Linux系统状态

top 

ifconfig 查看当前ip和网络信息的





netstat -ntlp 查看端口服务



## nginx

Linux安装命令  是yum

安装nginx(服务器软件) yun install nginx

默认的网页放置地址

/usr/share/nginx/html/

输入命令

```
ls
```

发现是有文件的(需要删除)

删除index.html

```
rm -rf index.html
```

![image-20211214094504906](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211214094504906.png)

![image-20211214094927129](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211214094927129.png)

再新建一个session(SFTP)

![1639446796(1)](.\1639446796(1).png)

找到 /usr/share/nginx/html/ 路径

将要加入的index路径放进去即可