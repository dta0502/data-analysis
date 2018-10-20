

# MongoDB复制collection（表）---[参考](http://www.ibloger.net/article/2614.html)

MongoDB的可以直接复制数据库，但是对于数据库里的表却没有直接的复制语句。在项目中遇到数据放错collection了情况就很棘手，现在将方法总结如下：

## 使用工具Studio 3T for MongoDB
- 选择一个数据库中的Collections集合，然后按住 Ctrl+C 复制快捷键会弹出如下帮助框。
- 点击 Ctrl+V 粘贴快捷键，重命名一下复制的名称即可。


## 使用工具Robo 3T
- 在Collection中，右键选择复制Collection 
- 然后重命名即可


## 利用foreach方法在shell里直接运行
```
db.test（复制源表）.find().forEach(function(x){db.target（目的表）.insert(x)})
```
## 在Java里操作，代码如下
```java
import org.bson.Document;
import com.mongodb.MongoClient;
import com.mongodb.client.FindIterable;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoCursor;
import com.mongodb.client.MongoDatabase;
public class DBtransfer {
        public static void main(String[] args) {
              MongoClient client = new MongoClient( "000.00.00.000", XXXXX); //数据库地址
              MongoDatabase database = client.getDatabase( "XXX" );  //数据库名
              MongoCollection<Document> collection = database .getCollection("XXXX" ); //要转移数据的表名
              MongoCollection<Document> collection2 = database .getCollection("XXXX" );//放入的表名
              FindIterable<Document> findIterable = collection .find(); //iterator——迭代
              MongoCursor<Document> mongoCursor = findIterable .iterator();  //游标
              while (mongoCursor .hasNext()){
                     Document d  = mongoCursor .next(); //遍历每一条数据
                     collection2 .insertOne(d );
                    // System.out.println( mongoCursor.next() );
              }
              System. out .println("转移成功" );
//            System.out.println(collection.find().toString());
       }
}
```
## 克隆collection

### 1）克隆远程colletion，使用cloneCollection命令完成将远程的collection复制到本地。

命令格式：`db.runCommand({cloneCollection:"集合",from:"原机器",copyIndexes:false}),copyIndexes:是否复制索引`

例子：132.42.33.175上test库t1表上有一条数据

```bash
> db.t1.find()
{ "_id" : ObjectId("4fd9a4bf186cb1b6ac95907d"), "name" : "liangzhangping", "addr" : "beijing" }
```

132.42.33.190上test库上t1表有两条条数据
```bash
> db.t1.find()
{ "_id" : ObjectId("4fd9c517dcde2d0e33d08c76"), "name" : "liangzhangping", "age" : 28 }
{ "_id" : ObjectId("4fda1795a3d56c6a40f2bc26"), "name" : "liangzhangping", "addr" : "jiangxi" }
```

现在将132.42.33.175上test库t1表的数据克隆到132.42.33.190上test库上t1表上，操作如下：

a、登录132.42.33.190机器上执行：
```bash
> db.runCommand({cloneCollection:"test.t1",from:"132.42.33.175:28010"})
{ "ok" : 1 }
```

b、查看验证
```bash
> db.t1.find()
{ "_id" : ObjectId("4fd9c517dcde2d0e33d08c76"), "name" : "liangzhangping", "age" : 28 }
{ "_id" : ObjectId("4fda1795a3d56c6a40f2bc26"), "name" : "liangzhangping", "addr" : "jiangxi" }
{ "_id" : ObjectId("4fd9a4bf186cb1b6ac95907d"), "name" : "liangzhangping", "addr" : "beijing" }
```

### 2）克隆本地collection，MongoDB没有提供命令进行本地复制，但我们可以写一个循环插入的方法完成，

参考上述3的循环插入代码