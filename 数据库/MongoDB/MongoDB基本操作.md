# MongoDB基本操作

## 查询文档
MongoDB 查询数据的语法格式如下：
```
db.collection.find(query, projection)
```

- `query` ：可选，使用查询操作符指定查询条件
- `projection` ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。

如果你需要以易读的方式来读取数据，可以使用`pretty()`方法，语法格式如下：
```
db.col.find().pretty()
```
`pretty()`方法以格式化的方式来显示所有文档。


## count查询记录条数
使用`count()`方法查询表中的记录条数，例如，下面的命令查询表col的记录数量：
```
db.col.find().count()
```
当使用`limit()`方法限制返回的记录数时，默认情况下`count()`方法仍然返回全部记录条数。 例如，下面的示例中返回的不是5，而是col表中所有的记录数量：
```
db.col.find().skip(10).limit(5).count();
```
如果希望返回限制之后的记录数量，要使用`count(true)`或者count`(非0)`：
```
db.col.find().skip(10).limit(5).count(true)
```

## 删除数据
删除mongodb集合中的数据可以使用`remove()`函数。`remove()`函数可以接受一个查询文档作为可选参数来有选择性的删除符合条件的文档。

`remove()`函数不会删除集合本身，同时，原有的索引也同样不会被删除。

删除文档是永久性的，不能撤销，也不能恢复的。因此，在执行`remove()`函数前先用`find()`命令来查看下是否正确，是个比较好的习惯啦。

### 1. 删除`"ban_friends_id":"BAN121113"`数据

```
db.test_ttlsa_com.remove({"ban_friends_id":"BAN121113"})
```

### 2. 删除所有数据

```	
> db.test_ttlsa_com.count()
2
> db.test_ttlsa_com.remove({})
> db.test_ttlsa_com.count()
0
```

### 3.  删除集合

```
> show collections
system.indexes
test_ttlsa_com
> db.test_ttlsa_com.drop()
true
> show collections
system.indexes
```

### 4. 删除整个数据库

```	
> show dbs
local   0.078125GB
ttlsa_com       0.203125GB
> db
ttlsa_com
> db.ttlsa_com.getDB()
ttlsa_com
> show collections
system.indexes
> db.dropDatabase()
{ "dropped" : "ttlsa_com", "ok" : 1 }
> db
ttlsa_com
> show dbs
local   0.078125GB
```

在执行删除整个数据库前，要谨慎，执行db命令查看当前的使用的数据库，可确保误删除，造成数据的丢失，是个不错的习惯啦。




