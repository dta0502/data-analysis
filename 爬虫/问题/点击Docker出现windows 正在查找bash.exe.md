# 点击Docker出现windows 正在查找bash.exe

## 问题描述
Window10下安装`DockerToolbox`时，安装成功后，双击桌面的`Docker Quickstart Terminal`快捷方式，会出现以下弹框： 
![1](https://img-blog.csdn.net/20180916113230635?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

可以猜测到时快捷方式所指定的路径不对（因为本人在安装Docker前已经安装好git了，原因就出在这）。

## 解决方法
右键点击这个图标，点击属性，出现下面的图：

![2](https://img-blog.csdn.net/20180916113251736?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

在`目标`这一个选项处需要填写正确的 `Git bash.exe`文件位置来启动`docker start.sh`文件。我的git安装在D:\Git下，Docker Toolbox安装在C盘。所以我这里写的是：
```bash
D:\Git\bin\bash.exe –login -i “C:\Program Files\Docker Toolbox\start.sh”
```

大家可以根据自己的安装配置来调整这块的执行语句。

修改完毕点击引用、确定，再双击图标即可。