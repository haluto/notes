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
```
或者
```
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
**insert()**
若集合不存在则会创建集合
```
db.<collection>.insert({})
```
**save()**
若集合不存在则会创建集合，指定_id则修改已存在的文档
```
db.<collection>.save({})
```
### 插入单个文档
**insertOne()**
```
db.<collection>.insertOne({})
```
### 插入多个文档
**insertMany()**
```
db.<collection>.insertMany([{},{},{}])
```
### 更新文档
**update()**

* query: update的查询条件，类似sql update查询内where后面的。
* update: update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的。
* upsert: 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
* multi: 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
* writeConcern: 可选，抛出异常的级别。

```
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
**remove()**
* query:（可选）删除的文档的条件。
* justOne:（可选）如果设为 true 或 1，则只删除一个文档。
* writeConcern:（可选）抛出异常的级别。
```
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
```
db.<collection>.find()
```
**条件判断**
* (>) 大于 - $gt
* (<) 小于 - $lt
* (>=) 大于等于 - $gte
* (<= ) 小于等于 - $lte
|   操作   |          格式          |                   范例                    |  RDBMS中的类似语句  |
| :------: | :--------------------: | :---------------------------------------: | :-----------------: |
|   等于   |    {<key>:<value>}     |   db.col.find({"by":"xx教程"}).pretty()   | where by = 'xx教程' |
|   小于   | {<key>:{$lt:<value>}}  | db.col.find({"likes":{$lt:50}}).pretty()  |  where likes < 50   |
| 小于等于 | {<key>:{$lte:<value>}} | db.col.find({"likes":{$lte:50}}).pretty() |  where likes <= 50  |
|   大于   | {<key>:{$gt:<value>}}  | db.col.find({"likes":{$gt:50}}).pretty()  |  where likes > 50   |
| 大于等于 | {<key>:{$gte:<value>}} | db.col.find({"likes":{$gte:50}}).pretty() |  where likes >= 50  |
|  不等于  | {<key>:{$ne:<value>}}  | db.col.find({"likes":{$ne:50}}).pretty()  |  where likes != 50  |

**AND条件**
```
db.col.find({key1:value1, key2:value2}).pretty()
```
**OR条件**
```
db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```
**$type操作符**
例：如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：
```
db.col.find({"title" : {$type : 2}})
```
|          Type          | Value | Descriptions  |
| :--------------------: | :---: | :-----------: |
|         Double         |   1   |               |
|         String         |   2   |               |
|         Object         |   3   |               |
|         Array          |   4   |               |
|      Binary data       |   5   |               |
|       Undefined        |   6   |    已废弃     |
|       Object id        |   7   |               |
|        Boolean         |   8   |               |
|          Date          |   9   |               |
|          Null          |  10   |               |
|   Regular Expression   |  11   |               |
|       JavaScript       |  13   |               |
|         Symnol         |  14   |               |
| JavaScript(with scope) |  15   |               |
|     32-bit integer     |  16   |               |
|       Timestamp        |  17   |               |
|     64-bit integer     |  18   |               |
|        Min key         |  255  | Query with -1 |
|        Max key         |  127  |               |

### 查找单个文档
```
db.<collection>.findOne()
```

# MongoDB文件系统（GridFS)

## 列出DB中的文件
**list <prefix>**
prefix为文件名的开头部分，用于过滤。
```
mongofiles -d <dbname> list
```
**search <string>**
string为文件名中任意一段符合的内容，用于过滤。
```
mongofiles -d <dbname> search <string>
```
## 本地文件存储到DB文件系统
**put**
```
mongofiles -d <dbname> put <db_filename> --local <local_filename>
```
## DB文件系统中读取文件到本地
**get**
```
mongofiles -d <dbname> get <db_filename> --local <local_filename>
```
**get_id**
在mongodb shell下，执行
```
db.fs.files.find()
```
可得到文件所在的文档，ObjectId就是文档的_id。注意要完整的id，比如 'ObjectId("5b07c24f71cb4653a87a90db")'
```
mongofiles -d <dbname> get_id "<ObjectId>"
```
## 删除DB文件系统中的文件
**delete**
```
mongofiles -d <dbname> delete <filename>
```
**delete_id**
```
mongofiles -d <dbname> delete_id "<ObjectId>"
```

