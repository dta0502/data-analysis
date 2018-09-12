# XPath无法匹配tbody标签

## 问题描述
我在用XPath匹配元素的时候，发现老是出错，后来发现是`<tbody>`标签上有文章。

## 问题分析
我使用Chrome的元素审查对网页进行分析来得到XPath路径，但是**Chrome会对网页源码进行加工，在`<table>`标签中，如果源码中没有写`<tbody>`标签，在元素审查和查看网页源代码中还是会将`<tbody>`强行添加上**。

当然，若源代码中没有`<tbody>`，而我们信任Chrome而把它添进XPath的话，是不会匹配出想要的结果的。

我们可以通过
```python
print(response)
```
对源代码进行检查，确定有没有`<tbody>`标签后，再得出XPath。
