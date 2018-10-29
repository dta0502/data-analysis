# MongoDB字段删除

## 字段删除
使用`update`命令，`update`命令格式：

```bash
db.collection.update(criteria,objNew,upsert,multi)
```

参数说明：

- `criteria`：查询条件。
- `objNew`：`update`对象和一些更新操作符。
- `upsert`：如果不存在`update`的记录，是否插入`objNew`这个新的文档，true为插入，默认为false，不插入。
- `multi`：默认是false，只更新找到的第一条记录。如果为true，把按条件查询出来的记录全部更新。

例如要把User表中`address`字段删除

```bash
db.User.update({},{$unset:{'address':''}},false, true)
```



