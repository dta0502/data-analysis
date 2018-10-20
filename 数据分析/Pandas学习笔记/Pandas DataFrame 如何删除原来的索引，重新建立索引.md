# Pandas DataFrame 如何删除原来的索引，重新建立索引

## 删除行索引重排

```python
ser.reset_index(drop = True)

df.reset_index(drop = True)
```

## 直接修列索引

```python
df = pd.DataFrame(df,columns = ['One','Two','Three'])
```


