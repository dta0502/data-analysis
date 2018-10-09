# Python更改pip源至国内镜像，显著提升下载速度

在使用Python的时候经常需要安装各种模块，而pip是很强大的模块安装工具，但是由于国外官方pypi经常被墙，导致不可用，所以我们最好是将自己使用的pip源更换一下，这样就能解决被墙导致的装不上库的烦恼。

网上有很多可用的源，例如
- 豆瓣：[http://pypi.douban.com/simple/](http://pypi.douban.com/simple/)
- 清华：[https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple)


最近使用得比较多并且比较顺手的是清华大学的pip源，它是官网pypi的镜像，每隔5分钟同步一次，地址[https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple)

 

## 临时使用：

可以在使用pip的时候加参数`-i https://pypi.tuna.tsinghua.edu.cn/simple`

例如：
```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple gevent
```
这样就会从清华这边的镜像去安装gevent库。

 

## 永久修改，一劳永逸：

- linux下，修改 `~/.pip/pip.conf `(没有就创建一个)， 修改` index-url`至`tuna`，内容如下：

```bash
 [global]
 index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```
 

- windows下，直接在user目录中创建一个pip目录，如：`C:\Users\xx\pip`，新建文件`pip.ini`，内容如下

```bash
 [global]
 index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```


