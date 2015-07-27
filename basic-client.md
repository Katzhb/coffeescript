# 基本客户端

## 问题

你想使用网络上提供的服务。

## 解决方案

创建一个基本的 TCP 客户机。
### 在 Node.js 中
```
net = require 'net'

domain = 'localhost'
port = 9001

connection = net.createConnection port, domain

connection.on 'connect', () ->
    console.log "Opened connection to #{domain}:#{port}."

connection.on 'data', (data) ->
    console.log "Received: #{data}"
    connection.end()
```

## 使用示例

可访问 [Basic Server](http://coffeescript-cookbook.github.io/chapters/networking/basic-server) ：
```
$ coffee basic-client.coffee
Opened connection to localhost:9001
Received: Hello, World!
```

## 讨论

最重要的工作发生在 *connection.on 'data'* 处理过程中，客户端接收到来自服务器的响应并最有可能安排对它的应答。

另请参阅 [Basic Server](http://coffeescript-cookbook.github.io/chapters/networking/basic-server)，[Bi-Directional Client](http://coffeescript-cookbook.github.io/chapters/networking/bi-directional-client) 和 [Bi-Directional Server](http://coffeescript-cookbook.github.io/chapters/networking/bi-directional-server) 。 

## 练习

- 根据命令行参数或配置文件为选定的目标域和端口添加支持。









