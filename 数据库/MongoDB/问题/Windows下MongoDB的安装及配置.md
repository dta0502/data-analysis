# Windows下MongoDB的安装及配置

转载于：[windows下MongoDB的安装及配置](https://blog.csdn.net/heshushun/article/details/77776706)


## 一、登录Mongodb官网[https://www.mongodb.com/download-center#community](https://www.mongodb.com/download-center#community) 下载  安装包。

## 二、安装MongoDB

下载后的安装包：

安装比较简单，中间主要是选择“Custom”自定义 安装路径修改下：`D:\software\MongoDB`
然后不断“下一步”，安装至结束。

安装比较容易。**难点在启动Mongodb的服务以及将MongoDB设置成Windows服务，加配置文件在windows的“服务”中找到。**

## 三、先创建数据库文件的存放位置

在MongoDB下创建data，在data下再创建db：`D:\software\MongoDB\data\db`

因为启动mongodb服务之前需要必须创建数据库文件的存放文件夹，否则命令不会自动创建，而且不能启动成功。

## 四、启动MongoDB服务
- 1.打开cmd命令行
- 2.进入`D:\software\MongoDB\bin`目录（注意：先输入d:进入d盘，然后输入`cd D:\software\MongoDB\bin`）
- 3.输入如下的命令启动mongodb服务：`mongod --dbpath D:\software\MongoDB\data\db` 即是在第三步创建的数据库存放文件路径下启动。
- 4.在浏览器输入`http://localhost:27017` （27017是mongodb的端口号）查看，若显示：
```
It looks like you are trying to access MongoDB over HTTP on the native driver port.
```
则表示，连接成功。如果不成功，可以查看端口是否被占用。但是在本地windows“服务”中，是没有配
置上mongodb 服务的，可以打开“服务”看下

![1](https://img-blog.csdn.net/20180913161533219?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## 五、配置本地windows mongodb 服务

这样可设置为 开机自启动，可直接手动启动关闭，可通过命令行`net start MongoDB`启动。该配置会大大方便。
### 1.先在data文件下创建一个新文件夹log（用来存放日志文件）
### 2.在Mongodb文件夹下新建配置文件`mongo.config` 

可能很多人都不会创建`.config`配置文件。那给大家介绍下简单的方法：
先创建一个`mongo.txt`文件，再打开，点击”另存为“，将底下的文件类型更改为”全部类型“，并更改文件名称为`mongo.config`。这样就可以创建一个`.config`的配置文件了。

### 3.用记事本打开`mongo.config`  ，并输入：
```
dbpath=D:\software\MongoDB\data\db
logpath=D:\software\MongoDB\data\log\mongo.log
```

### 4.用管理员身份打开cmd:

### 5.配置windows服务：

cmd先跳转到 `D:\software\MongoDB\bin`目录下。输入：
```
mongod --config "D:\software\Mongodb\mongo.config" --install --serviceName "MongoDB"
```
即根据刚创建的`mongo.config`配置文件安装服务，名称为`MongoDB`。
完成后，再次查看本地的服务。
![2](https://img-blog.csdn.net/20180913162052307?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果成功的话，会发现本地服务多了”MongoDB"服务。

可以通过：“开机自启动，可直接手动启动关闭，命令行net start MongoDB 启动”。开启后，可以正常连接了。可以用pycharm等IDE连接，
