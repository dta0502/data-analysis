# Python中DataFrame常见操作：取行、列、切片、统计特征值:

```python
#  -*- coding: utf-8 -*-
import numpy as np
import pandas as pd

data = pd.DataFrame(np.arange(16).reshape(4,4),index = list("ABCD"),columns=list('wxyz'))
print(data)
print(data[0:2])       #取前两行数据
print('+++++++++++++')

print(len(data))              #求出一共多少行
print(data.columns.size)      #求出一共多少列
print('+++++++++++++')

print(data.columns)        #列索引名称
print(data.index)       #行索引名称
print('+++++++++++++')

print(data.iloc[1])             #取第2行数据
print('+++++++++++++')

print(data['x'])      #取列索引为x的一列数据
print(data.loc['A'])      #取第行索引为”A“的一行数据，
print('+++++++++++++')

print(data.loc[:,['x','z']])          #表示选取所有的行以及columns为a,b的列；
print(data.loc[['A','B'],['x','z']])     #表示选取'A'和'B'这两行以及columns为x,z的列的并集；
print('+++++++++++++')

print(data.iloc[1:3,1:3])              #数据切片操作，切连续的数据块
print(data.iloc[[0,2],[1,2]])              #即可以自由选取行位置，和列位置对应的数据，切零散的数据块
print('+++++++++++++')

print(data[data>2])       #表示选取数据集中大于0的数据
print(data[data.x>5])       #表示选取数据集中x这一列大于5的所有的行
print('+++++++++++++')

a1 = data.copy()
print(a1[a1['y'].isin(['6','10'])])    #表显示满足条件：列y中的值包含'6','8'的所有行。
print('+++++++++++++')

print(data.mean())           #默认对每一列的数据求平均值；若加上参数a.mean(1)则对每一行求平均值；
print(data['x'].value_counts())    #统计某一列x中各个值出现的次数：
print('+++++++++++++')

print(data.describe()) #对每一列数据进行统计，包括计数，均值，std，各个分位数等。
```


下面是输出的结果：

```python
    w   x   y   z
A   0   1   2   3
B   4   5   6   7
C   8   9  10  11
D  12  13  14  15
   w  x  y  z
A  0  1  2  3
B  4  5  6  7
+++++++++++++
4
4
+++++++++++++
Index(['w', 'x', 'y', 'z'], dtype='object')
Index(['A', 'B', 'C', 'D'], dtype='object')
+++++++++++++
w    4
x    5
y    6
z    7
Name: B, dtype: int32
+++++++++++++
A     1
B     5
C     9
D    13
Name: x, dtype: int32
w    0
x    1
y    2
z    3
Name: A, dtype: int32
+++++++++++++
    x   z
A   1   3
B   5   7
C   9  11
D  13  15
   x  z
A  1  3
B  5  7
+++++++++++++
   x   y
B  5   6
C  9  10
   x   y
A  1   2
C  9  10
+++++++++++++
      w     x     y   z
A   NaN   NaN   NaN   3
B   4.0   5.0   6.0   7
C   8.0   9.0  10.0  11
D  12.0  13.0  14.0  15
    w   x   y   z
C   8   9  10  11
D  12  13  14  15
+++++++++++++
   w  x   y   z
B  4  5   6   7
C  8  9  10  11
+++++++++++++
w    6.0
x    7.0
y    8.0
z    9.0
dtype: float64
13    1
5     1
9     1
1     1
Name: x, dtype: int64
+++++++++++++
               w          x          y          z
count   4.000000   4.000000   4.000000   4.000000
mean    6.000000   7.000000   8.000000   9.000000
std     5.163978   5.163978   5.163978   5.163978
min     0.000000   1.000000   2.000000   3.000000
25%     3.000000   4.000000   5.000000   6.000000
50%     6.000000   7.000000   8.000000   9.000000
75%     9.000000  10.000000  11.000000  12.000000
max    12.000000  13.000000  14.000000  15.000000
```
