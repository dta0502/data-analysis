# Python安装scrapy报错 Python.h 没有那个文件或目录

## 错误说明
安装scrapy的时候报错，其实这个错误是一个间接，由其依赖引起。

```bash
build/temp.linux-x86_64-2.7/twisted/test/raiser.o 
twisted/test/raiser.c:4:20: fatal error: Python.h: 没有那个文件或目录 
include “Python.h” 
^ 
compilation terminated. 
error: command ‘x86_64-linux-gnu-gcc’ failed with exit status 1
```

![1](Python安装scrapy报错 Python.h 没有那个文件或目录.png)


## 解决方案

安装python-dev，这是Python的头文件和静态库包: 

```bash
sudo apt-get install python3.5-dev
```
需要注意的是：对于每个Python版本都有对应的python-dev包，所以命令不尽相同。 

然后pip安装scrapy成功。

参考链接：https://blog.csdn.net/jasonLee_lijiaqi/article/details/80421657