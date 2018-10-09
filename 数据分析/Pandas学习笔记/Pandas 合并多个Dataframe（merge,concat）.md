# Pandas 合并多个Dataframe（merge,concat）

## pd.merge()

在数据处理的时候经常会遇到多个表单的合并问题，比如一个表单有`user_id`和`age`这两个字段，另一个表单有`user_id`和`sex`这两个字段，要把这两个表合并成只有`user_id`、`age`、`sex`三个字段的表。

普通的拼接是做不到的，因为user_id每一行之间不是对应的。pandas中有个merge函数可以做到这个实用的功能。

```python
df = pd.merge(df1, df2, how='left', on='user_id')
```

用法很简单，说一下后两个参数就可以了，`how=""`参数表示以哪个表的key为准，上面的`how="left"`表示以表df1为准，而key也就是`on=""`的参数

`how="left"`就是说，保留`user_id`字段的全部信息，不增加也不减少，但是拼接的时候只把df2表中的与df1中`user_id`字段交集的部分合并上就可以了，如果df2中出现了某个`user_id`在df1中没有出现，就抛弃掉这个样本不作处理。

如果要进行多key合并:

```python
df = pd.merge(df1, df2, how='left', on=['user_id','sku_id'])
```
## pd.concat()
但是如果想仅进行简单的“拼接”而不是合并呢，要使用concat函数：

```python
df = pd.concat([df_user, dummies_sex, dummies_age, dummies_level], axis=1 )
```
这样可以保留这些表单的全部信息，参数`axis=1`表示列拼接，`axis=0`表示行拼接。

要保证每个表单的行数是相同的，并且每一行对应的key也是相同的，列拼接才变得有意义。


