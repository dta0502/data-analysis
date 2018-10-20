
## MongoDB 安装

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

#下面命令针对ubuntu16.04版本，在其他ubuntu版本系统请查看MongoDB官网
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

sudo apt-get update

sudo apt-get install -y mongodb-org
```

安装完成后，在终端输入以下命令查看MongoDB的最新版本：

```bash
mongo -version
```

## 启动、重新启动和关闭mongodb命令

```bash
sudo service mongod start

sudo service mongod stop

sudo service mongod restart
```

### 查看是否启动成功

```bash
sudo cat /var/log/mongodb/mongod.log
```

在 `mongod.log` 日志中若出现如下信息，说明启动成功

```
[initandlisten] waiting for connections on port 27017
```

## MongoDB 卸载

删除 MongoDB 包

```bash
sudo apt-get purge mongodb-org*
```

删除 MongoDB 数据库和日志文件

```bash
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

## MongoDB 使用

### shell命令模式 

输入mongo进入shell命令模式，默认连接的数据库是test数据库，命令如下：

```bash
mongo
```

### 常用操作命令：

- `show dbs`：显示数据库列表 
- `show collections`：显示当前数据库中的集合（类似关系数据库中的表table） 
- `show users`：显示所有用户 
- `use yourDB`：切换当前数据库至yourDB 
- `db.help()` ：显示数据库操作命令 
- `db.yourCollection.help()` ：显示集合操作命令，yourCollection是集合名



