# Pandas DataFrame添加一行

这里采用`append()`函数。

## 添加一行
```python
>>> res = pd.DataFrame(columns=('lib', 'qty1', 'qty2'))
>>> res = res.append([{'qty1':10.0}], ignore_index=True)
>>> print(res.head())

   lib  qty1  qty2
0  NaN  10.0   NaN
```

## 合并两个DataFrame
这里需要注意的是`ignore_index`参数。

### ignore_index = False
```python
>>> df = pd.DataFrame([[1, 2], [3, 4]], columns=list('AB'))

   A  B
0  1  2
1  3  4
>>> df2 = pd.DataFrame([[5, 6], [7, 8]], columns=list('AB'))
>>> df.append(df2)

   A  B
0  1  2
1  3  4
0  5  6
1  7  8

```

### ignore_index = True
```python
>>> df.append(df2, ignore_index=True)

   A  B
0  1  2
1  3  4
2  5  6
3  7  8
```

