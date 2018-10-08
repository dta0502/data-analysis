# Pandas Series转换为DataFrame

## 说明
虽然Series有一个`to_frame()`方法，但是当Series的index也需要转变为DataFrame的一列时，这个方法转换会有一点问题。所以，下面我采用将Series对象转换为list对象，然后将list对象转换为DataFrame对象。

## 实例
这里的month为一个series对象：
```python
type(month)
pandas.core.series.Series
```
它的index为月份，values为数量，下面将这两列都转换为DataFrame的columns。
```python
import pandas as pd

dict_month = {'month':month.index,'numbers':month.values}
df_month = pd.DataFrame(dict_month)
```

