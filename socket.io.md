美洽\IM



socket.io 实战

聊天机制：用户发送消息给**服务器**，服务器将消息发给**条件允许**的用户



## 一，构建步骤

1.服务端  npm i socket  客户端 npm i socket-client

2.创建一个socket文件 

3.main.js 导入  （刚开始做的时候这个点不会） **一定要记得  js文件要从main.js导入**

4.需要配置代理 

5.后台启动测试serve

## 二、基本语法

import { io } from "socket.io-client";

1.创建连接：const socket =io （地址）

2.发送消息 socket.emit(自定义消息类型，消息内容,接收到消息的回调函数)

服务器(.on)拿到消息再发送消息（.emit）

2-1私密发送消息 socket.emit(自定义消息类型，消息内容，room,接收到消息的回调函数) **需要携带room** （服务端使用）

服务端

```javascript
//拿到前端的数据
socket.on("message", (message, room) => {
        if (room === "") {
            socket.broadcast.emit("message-bc", message);
        } else {
            socket.to(room).emit("message-bc", message); //服务端接收到消息 在发给指定room的用户
        }
        console.log({ message });
    });
```

3.监听消息:socket.on(事件type类型，接收到消息的回调函数)

4.socket.broadcast.emit("message-bc", message);  发消息自己看不到 别人可以收到（服务器不给发送的user_id发消息）

**5.**加入聊天房间: socket.emit('join',room，回调函数 ()=>{})

服务端操作  

```javaScript
socket.on("join-room", (room, cb) => {

​    if (room === "") return;

​    socket.join(room);

​    cb(`Joined ${room}`); //返回的message

  });
```

客户端的下线

离线行为

默认情况下，在 Socket **未连接**时发出的任何事件都将被缓冲，直到重新连接。

- 使用Socket 实例的[connected](https://socket.io/docs/v4/client-socket-instance/#socketconnected)属性

```
if (socket.connected) {  socket.emit( */\* ... \*/* );} else {  *// ...*}
```



- 使用[可变事件](https://socket.io/docs/v4/emitting-events/#volatile-events)

```
socket.volatile.emit( */\* ... \*/* );
```

