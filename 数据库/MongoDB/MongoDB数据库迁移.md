# MongoDB数据库迁移

## MongoDB数据导入与导出

### 1、导出工具：mongoexport
1)概念：

mongoDB中的mongoexport工具可以把一个collection导出成JSON格式或CSV格式的文件。可以通过参数指定导出的数据项，也可以根据指定的条件导出数据。

2)语法：

```bash
mongoexport -d dbname -c collectionname -o file --type json/csv -f field
```

参数说明：
```
-d ：数据库名
-c ：collection名
-o ：输出的文件名
--type ： 输出的格式，默认为json
-f ：输出的字段，如果-type为csv，则需要加上-f "字段名"
```

3)示例：

```bash
sudo mongoexport -d mongotest -c users -o /home/python/Desktop/mongoDB/users.json --type json -f "_id,user_id,user_name,age,status"
```

### 2、数据导入：mongoimport
1)语法：

```bash
mongoimport -d dbname -c collectionname --file filename --headerline --type json/csv -f field
```

参数说明：

```
-d ：数据库名
-c ：collection名
--type ：导入的格式默认json
-f ：导入的字段名
--headerline ：如果导入的格式是csv，则可以使用第一行的标题作为导入的字段
--file ：要导入的文件
```
 
2)示例：

```bash
sudo mongoimport -d mongotest -c users --file /home/mongodump/articles.json --type json
```

## MongoDB备份与恢复
### 1、MongoDB数据库备份
1)语法：

```bash
mongodump -h dbhost -d dbname -o dbdirectory
```

参数说明：

```
-h： MongDB所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017
-d： 需要备份的数据库实例，例如：test
-o： 备份的数据存放位置，例如：/home/mongodump/，当然该目录需要提前建立，这个目录里面存放该数据库实例的备份数据。
```

2)实例：

```
sudo rm -rf /home/momgodump/
sudo mkdir -p /home/momgodump
sudo mongodump -h 192.168.17.129:27017 -d itcast -o /home/mongodump/
```

### 2、MongoDB数据库恢复
1)语法：

```bash
mongorestore -h dbhost -d dbname --dir dbdirectory
```

参数或名：

```
-h： MongoDB所在服务器地址
-d： 需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2
--dir： 备份数据所在位置，例如：/home/mongodump/itcast/
--drop： 恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用！
```

2)实例：

```bash
mongorestore -h 192.168.17.129:27017 -d itcast_restore --dir /home/mongodump/itcast/
```

