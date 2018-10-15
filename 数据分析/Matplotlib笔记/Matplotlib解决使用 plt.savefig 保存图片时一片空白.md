# Matplotlib解决使用 plt.savefig 保存图片时一片空白

## 问题
当使用如下代码保存使用`plt.savefig`保存生成的图片时，结果打开生成的图片却是一片空白。
```python
import matplotlib.pyplot as plt

""" 一些画图代码 """
plt.show()
plt.savefig("filename.png")
```

## 原因
其实产生这个现象的原因很简单：在 `plt.show()` 后调用了 `plt.savefig()` ，在 `plt.show()` 后实际上已经创建了一个新的空白的图片（坐标轴），这时候你再 `plt.savefig()` 就会保存这个新生成的空白图片。

## 解决
知道了原因，就不难知道解决办法了，解决办法有两种：

- 在 `plt.show()`之前调用`plt.savefig()`

```python
import matplotlib.pyplot as plt

""" 一些画图代码 """
plt.savefig("filename.png")
plt.show()
```

- 画图的时候获取当前图像（这一点非常类似于 Matlab 的句柄的概念）

```python
# gcf: Get Current Figure
fig = plt.gcf()
plt.show()
fig1.savefig('tessstttyyy.png', dpi=100)
```



