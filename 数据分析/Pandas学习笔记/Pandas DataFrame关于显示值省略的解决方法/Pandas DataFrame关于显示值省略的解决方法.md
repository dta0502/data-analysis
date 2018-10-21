# Pandas DataFrame关于显示值省略的解决方法

转载于：[pandas中DataFrame关于显示值省略的解决方法](https://blog.csdn.net/xiaodongxiexie/article/details/70147683)

在使用DataFrame中有时候会遇到表格中的value显示不完全，像下面这样：

```python
import pandas as pd

longString = u'''真正的科学家应当是个幻想家；谁不是幻想家，谁就只能把自己称为实践家。人生的磨难是很多的，所以我们不可对于每一件轻微的伤害都过于敏感。在生活磨难面前，精神上的坚强和无动于衷是我们抵抗罪恶和人生意外的最好武器。'''
pd.DataFrame({'word':[longString]})
```

输出如下： 

![1](https://img-blog.csdn.net/20181021161957164?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

可以看到，显示值长度为50个后就出现了省略了，这个因为DataFrame默认的显示长度为50，不过可以改默认设置：

```python
pd.set_option('max_colwidth',200)
pd.DataFrame({'word':[longString]})
```

![2](https://img-blog.csdn.net/2018102116205259?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R0YTA1MDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

通过设置就可以改变显示长度了。 
