# Windows 安装 MongoDB 卡住问题解决

MongoDB 的安装过程比较简单，一路next就可以，

需要注意的是最后一步，勾选掉 `mongo db compass`，不安装，不然会因为一直下载这个工具，导致安装卡主。如下图


![1](https://img-blog.csdn.net/2018091918200759?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



`mongo db compass` 是个图形工具，可以方便直接管理 mongodb 数据，不过都是我们一般都是基于命令行工作，所以不需要