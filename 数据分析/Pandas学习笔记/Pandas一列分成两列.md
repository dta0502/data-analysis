# Pandas一列分成两列

## 分割成一个包含两个元素列表的列
对于一个已知分隔符的简单分割（例如，用破折号分割或用空格分割） `.str.split()`方法就足够了 。 它在字符串的列（系列）上运行，并返回列表（系列）。

```python
>>> import pandas as pd
>>> df = pd.DataFrame({'AB': ['A1-B1', 'A2-B2']})
>>> df

      AB
0  A1-B1
1  A2-B2
>>> df['AB_split'] = df['AB'].str.split('-')
>>> df

      AB  AB_split
0  A1-B1  [A1, B1]
1  A2-B2  [A2, B2]
```
## 分割成两列，每列包含列表的相应元素

下面来看下如何从：`分割成一个包含两个元素列表的列`至`分割成两列，每列包含列表的相应元素？`。

```python
>>> df['AB'].str[0]

0    A
1    A
Name: AB, dtype: object

>>> df['AB'].str[1]

0    1
1    2
Name: AB, dtype: object
```

因此，可以得到：
```python
>>> df['AB'].str.split('-', 1).str[0]

0    A1
1    A2
Name: AB, dtype: object

>>> df['AB'].str.split('-', 1).str[1]

0    B1
1    B2
Name: AB, dtype: object
```

可以通过如下代码将pandas的一列分成两列：
```python
>>> df['A'], df['B'] = df['AB'].str.split('-', 1).str
>>> df

      AB  AB_split   A   B
0  A1-B1  [A1, B1]  A1  B1
1  A2-B2  [A2, B2]  A2  B2
```