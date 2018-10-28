# MongoDB排序错误：Sort operation used more than the maximum 33554432 bytes of RAM

## 错误描述
我用如下命令查询某一个键的最大值：

```bash
db.video_info.find().sort({'vid':-1})
```

出现如下错误：

```
Error: error: {
        "ok" : 0,
        "errmsg" : "Executor error during find command: OperationFailed: Sort operation used more than the maximum 33554432 bytes of RAM. Add an index, or specify a smaller limit.",
        "code" : 96,
        "codeName" : "OperationFailed"
}

```


## 分析解决问题
**排序操作使用超过最大33554432个字节的RAM，添加索引或指定较小的限制。**

这是由于**mongodb排序的时候会把数据加载到内存中，在这里排序的数据量太大导致超过了32M的默认排序内存**。

由于我这里仅仅需要查询最大值，所以我采用提示的第二种方案，命令后面加一个`limit`。

```bash
db.video_info.find().sort({'vid':-1}).limit(1)
```
 

