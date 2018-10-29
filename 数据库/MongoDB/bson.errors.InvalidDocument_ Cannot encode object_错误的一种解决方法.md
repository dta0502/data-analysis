# bson.errors.InvalidDocument_ Cannot encode object_错误的一种解决方法

在Python中利用pandas库的`read_csv`函数读取CSV文件，文件中包含有数值型值，然后将其转换成字典存入Mongodb数据库中，但是在插入数据库中会报错：

```
bson.errors.InvalidDocument: Cannot encode object:
```

这是因为pandas库在读取数值型值时返回的结果不是整型或者浮点型，而是`numpy.int64`类型的一个对象，Mongodb是无法对一个对象进行编码存储的，所以这里需要对读取到的结果进行强制类型转换：

```python
vid = int(df['vid'][j])
```

