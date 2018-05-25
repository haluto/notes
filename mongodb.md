MongoDB常用命令，详细可参考[菜鸟教程](http://www.runoob.com/mongodb/mongodb-tutorial.html)以及[MongoDB官网教程](https://docs.mongodb.com/manual/tutorial/).

[TOC]

# 数据库操作

## db操作
### 显示所有db
```
show dbs
```
### 切换/创建db
```
use <dbname>
```
### 删除db
```
db.dropDatabase()
```

## collection操作
### 显示所有集合
```
show tables
# or
show collections
```
### 创建集合
```
db.createCollection(name, options)
```
### 删除集合
```
db.<collection>.drop()
```

## 文档操作
### 插入文档
```c
db.<collection>.insert({})

//若集合不存在则创建
```
```c
db.<collection>.save({})

//若集合不存在则创建，指定_id则修改已存在的文档
```
### 插入单个文档
```
db.<collection>.insertOne({})
```
### 插入多个文档
```
db.<collection>.insertMany([{},{},{}])
```
### 更新文档
```c
/*
  query: update的查询条件，类似sql update查询内where后面的。
  update: update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
  upsert: 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
  multi: 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
  writeConcern: 可选，抛出异常的级别。
*/
db.<collection>.update(
  <query>,
  <update>,
  {
    upsert: <boolean>,
    multi: <boolean>,
    writeConcern: <document>
  }
)
```
### 删除文档
```c
/*
  query:（可选）删除的文档的条件。
  justOne:（可选）如果设为 true 或 1，则只删除一个文档。
  writeConcern:（可选）抛出异常的级别。
*/
db.<collection>.remove(
  <query>,
  {
    justOne: <boolean>,
    writeConcern: <document>
  }
)
```
### 删除单个文档
```
db.<collection>.deleteOne({})
```
### 删除多个文档
```
db.<collection>.deleteMany({})
```
### 查找文档
```c
db.<collection>.find()
/*
操作        格式                     范例                                        RDBMS中的类似语句
等于        {<key>:<value>}          db.col.find({"by":"菜鸟教程"}).pretty()     where by = '菜鸟教程'
小于        {<key>:{$lt:<value>}}    db.col.find({"likes":{$lt:50}}).pretty()   where likes < 50
小于或等于   {<key>:{$lte:<value>}}   db.col.find({"likes":{$lte:50}}).pretty()  where likes <= 50
大于        {<key>:{$gt:<value>}}    db.col.find({"likes":{$gt:50}}).pretty()   where likes > 50
大于或等于   {<key>:{$gte:<value>}}   db.col.find({"likes":{$gte:50}}).pretty()  where likes >= 50
不等于      {<key>:{$ne:<value>}}    db.col.find({"likes":{$ne:50}}).pretty()    where likes != 50
AND条件：
db.col.find({key1:value1, key2:value2}).pretty()
OR条件：
db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()

//-------------------------------------------------------------
(>) 大于 - $gt
(<) 小于 - $lt
(>=) 大于等于 - $gte
(<= ) 小于等于 - $lte
//-------------------------------------------------------------
$type操作符
Double: 1                 String:    2        Object: 3            Array: 4                      Binary data: 5
Undefined: 6(已废弃)       Object id: 7        Boolean: 8           Date: 9                       Null: 10
Regular Expression: 11    JavaScript: 13      Symbol: 14           JavaScript(with scope): 15
32-bit integer: 16        Timestamp: 17       64-bit integer: 18   Min key: 255(Query with -1)   Max key: 127

例：如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：
db.col.find({"title" : {$type : 2}})
*/
```
### 查找单个文档
```
db.<collection>.findOne()
```


