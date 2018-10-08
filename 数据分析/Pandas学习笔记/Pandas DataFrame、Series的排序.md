# Pandas DataFrame、Series的排序


## 库导入
```python
from pandas import DataFrame, Series
import numpy as np
```
## Series
- 按索引排序
```python
##### Series按索引排序 sort_index方法 返回新对象
obj = Series([1, 3, 2, 5, 6], index=list('dabce'))
obj.sort_index()
obj.sort_index(ascending=False)
```
- 按值排序
```python
##### Series按值排序 sort_values方法 返回新对象
obj.sort_values()
obj.sort_values(ascending=False)
```

## DataFrame
- 按索引排序
```python
frame = DataFrame(np.random.randn(4, 3), columns=list('dbe'),index=['Ut', 'Oh', 'Tex', 'Ore']) 
frame.sort_index() # 同frame.sort_index(axis=0) 
frame.sort_index(ascending=False)               
frame.sort_index(axis=1) 
frame.sort_index(axis=1, ascending=False) 
```
- 按值排序
```python
##### DataFrame按列排序
frame = DataFrame({'a': [1, 3, 1, 5], 'b': [2, 1, 4, 6]})
# sort_values方法
frame.sort_values(by=['a', 'b'], ascending=[True, True])
frame.sort_values(by=['a', 'b'], ascending=[True, False])
```