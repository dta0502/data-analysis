# Pandas DataFrame关于显示值省略的解决方法

转载于：[pandas中DataFrame关于显示值省略的解决方法](https://blog.csdn.net/xiaodongxiexie/article/details/70147683)

在使用DataFrame中有时候会遇到表格中的value显示不完全，像下面这样：

```python
import pandas as pd

longString = u'''真正的科学家应当是个幻想家；谁不是幻想家，谁就只能把自己称为实践家。人生的磨难是很多的，所以我们不可对于每一件轻微的伤害都过于敏感。在生活磨难面前，精神上的坚强和无动于衷是我们抵抗罪恶和人生意外的最好武器。'''
pd.DataFrame({'word':[longString]})
```

输出如下： 

![1](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90/Pandas%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/Pandas%20DataFrame%E5%85%B3%E4%BA%8E%E6%98%BE%E7%A4%BA%E5%80%BC%E7%9C%81%E7%95%A5%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/1.png)

可以看到，显示值长度为50个后就出现了省略了，这个因为DataFrame默认的显示长度为50，不过可以改默认设置：

```python
pd.set_option('max_colwidth',200)
pd.DataFrame({'word':[longString]})
```

![2](https://raw.githubusercontent.com/dta0502/data-analysis/master/%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90/Pandas%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/Pandas%20DataFrame%E5%85%B3%E4%BA%8E%E6%98%BE%E7%A4%BA%E5%80%BC%E7%9C%81%E7%95%A5%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/2.png)

通过设置就可以改变显示长度了。 
