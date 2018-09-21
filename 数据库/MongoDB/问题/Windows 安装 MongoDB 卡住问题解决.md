# Windows 安装 MongoDB 卡住问题解决

MongoDB 的安装过程比较简单，一路next就可以，

需要注意的是最后一步，勾选掉 `mongo db compass`，不安装，不然会因为一直下载这个工具，导致安装卡主。如下图


![1](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E6%95%B0%E6%8D%AE%E5%BA%93/MongoDB/%E9%97%AE%E9%A2%98/Windows%20%E5%AE%89%E8%A3%85%20MongoDB%20%E5%8D%A1%E4%BD%8F%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3-1.png)



`mongo db compass` 是个图形工具，可以方便直接管理 mongodb 数据，不过都是我们一般都是基于命令行工作，所以不需要
