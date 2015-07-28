#MongoDB
  
##问题
  
你需要与一个 MongoDB 数据库连接的接口。
  
##解决方案
  
###对于 Node.js

####安装

- 如果你的计算机中还没有 [MongoDB](http://www.mongodb.org/display/DOCS/Quickstart) ，需要安装。
  
- [安装本地 MongoDB 模块](https://github.com/christkv/node-mongodb-native)。

####保存记录
  
```
mongo = require 'mongodb'

server = new mongo.Server "127.0.0.1", 27017, {}

client = new mongo.Db 'test', server, {w:1}

# save() updates existing records or inserts new ones as needed
exampleSave = (dbErr, collection) ->
    console.log "Unable to access database: #{dbErr}" if dbErr
    collection.save { _id: "my_favorite_latte", flavor: "honeysuckle" }, (err, docs) ->
        console.log "Unable to save record: #{err}" if err
        client.close()

client.open (err, database) ->
    client.collection 'coffeescript_example', exampleSave
``` 
  
#### 查找记录
  
```
mongo = require 'mongodb'

server = new mongo.Server "127.0.0.1", 27017, {}

client = new mongo.Db 'test', server, {w:1}

exampleFind = (dbErr, collection) ->
    console.log "Unable to access database: #{dbErr}" if dbErr
    collection.find({ _id: "my_favorite_latte" }).nextObject (err, result) ->
        if err
            console.log "Unable to find record: #{err}"
        else
            console.log result # => {  id: "my_favorite_latte", flavor: "honeysuckle" }
        client.close()

client.open (err, database) ->
    client.collection 'coffeescript_example', exampleFind
```
  
#### 对于浏览器
  
一个[基于 REST 的接口](https://github.com/tdegrunt/mongodb-rest)在工程中，会提供基于 AJAX 的访问通道。
  
##讨论
  
这个方法将 save 和 find 分开进单独的实例，其目的是分散 MongoDB 指定的连接任务的关注点以及回收任务。[async 模块](https://github.com/caolan/async)可以帮助这样的异步调用。

