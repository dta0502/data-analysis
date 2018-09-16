# windows10下成功安装docker splash及遇到问题的解决方案

在windows10 下安装docker:

## 1.进入官方网站安装：[https://docs.docker.com/docker-for-windows/install/](https://docs.docker.com/docker-for-windows/install/)

![1](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E7%88%AC%E8%99%AB/%E9%97%AE%E9%A2%98/windows10%E4%B8%8B%E6%88%90%E5%8A%9F%E5%AE%89%E8%A3%85docker%20splash%E5%8F%8A%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-1.png)


注：仔细阅读文档，会发现：运行 Docker for Windows 仅支持win10专业版 。所以可以查看自己的电脑是否是win10专业版的，（一般自己的笔记本都是家庭版的）

如果是win10专业版的，可以按照文档一步一步安装即可。可参考[https://my.oschina.net/ykbj/blog/1595328](https://my.oschina.net/ykbj/blog/1595328)

## 2.win10 家庭版安装docker: 依赖于 Oracle Virtual Box 安装则可以安装 Docker Toolbox 

安装路径下载：[https://docs.docker.com/toolbox/overview/#whats-in-the-box](https://docs.docker.com/toolbox/overview/#whats-in-the-box)

![2](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E7%88%AC%E8%99%AB/%E9%97%AE%E9%A2%98/windows10%E4%B8%8B%E6%88%90%E5%8A%9F%E5%AE%89%E8%A3%85docker%20splash%E5%8F%8A%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-2.png)

## 3.下载安装

国内可以使用阿里云的镜像来下载，下载地址：[http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/](http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/)

小扩展：
```
docker toolbox 是一个工具集，它主要包含以下一些内容：

Docker CLI 客户端，用来运行docker引擎创建镜像和容器
Docker Machine. 可以让你在windows的命令行中运行docker引擎命令
Docker Compose. 用来运行docker-compose命令
Kitematic. 这是Docker的GUI版本
Docker QuickStart shell. 这是一个已经配置好Docker的命令行环境
Oracle VM Virtualbox. 虚拟机
```
下载完成之后直接点击安装，安装成功后，桌边会出现三个图标，入下图所示：

![3](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E7%88%AC%E8%99%AB/%E9%97%AE%E9%A2%98/windows10%E4%B8%8B%E6%88%90%E5%8A%9F%E5%AE%89%E8%A3%85docker%20splash%E5%8F%8A%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-3.png)


点击 Docker QuickStart 图标来启动 Docker Toolbox 终端。

如果系统显示 User Account Control 窗口来运行 VirtualBox 修改你的电脑，选择 Yes。


**注意会出现的问题：一直连接不上：**

解决方式：

需要到[https://github.com/boot2docker/boot2docker/releases](https://github.com/boot2docker/boot2docker/releases)下载最新的，

并复制到`C:\Users\Administrator\.docker\machine\cache`目录下

可参考：[https://blog.csdn.net/rickyit/article/details/72772552](https://blog.csdn.net/rickyit/article/details/72772552)

docker启动成功：

![4](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E7%88%AC%E8%99%AB/%E9%97%AE%E9%A2%98/windows10%E4%B8%8B%E6%88%90%E5%8A%9F%E5%AE%89%E8%A3%85docker%20splash%E5%8F%8A%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-4.png)


注意：这里docker默认的ip是：`192.168.99.100`

## 4.拉取镜像splash

执行命令：
```bash
$ docker pull scrapinghub/splash
```

## 5.启动容器：

执行命令：
```bash
$ sudo docker run -p 8050:8050 -p 5023:5023 scrapinghub/splash
```
表示:Splash现在在端口`8050（http）`和`5023（telnet）`上的0.0.0.0处可用。

## 6.启动成功
在浏览器上输入：`192.168.99.100：8050`\
显示splash web的页面：

![5](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E7%88%AC%E8%99%AB/%E9%97%AE%E9%A2%98/windows10%E4%B8%8B%E6%88%90%E5%8A%9F%E5%AE%89%E8%A3%85docker%20splash%E5%8F%8A%E9%81%87%E5%88%B0%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-5.png)
