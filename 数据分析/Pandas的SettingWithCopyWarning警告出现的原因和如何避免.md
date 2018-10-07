# Pandas的SettingWithCopyWarning警告出现的原因和如何避免

这段时间一直在用pandas，今天运行前人代码发现报了一个warning：
```python
SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame 
See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
```

网上查了下，发现有这个问题的人还不少，但是感觉大家都没太说到点上，到底这个错误是如何产生的以及如何避免。不少方法基本上都是想办法绕过这个warning或者直接禁用掉warning提示，这样并不知道其中的原理，只是避而不见，确实不是一个好的变成习惯。后来上google上搜，看到了一个[youtube视频](https://www.youtube.com/watch?v=4R4WsDJ-KVc)和[一篇外文Blog](https://www.dataquest.io/blog/settingwithcopywarning/)解释得还是非常清楚的。Youtube视频解释的比较简略，blog解释的更详细了一些。 

现在总结如下：

## SettingWithCopyWarning出现的原因

### 链式赋值/Chained Assignment
SettingWithCopyWarning会在什么时候出现呢，简而言之就是在链式赋值的时候出现。 
以下例子数据以此为例：

```python
df1 = pd.DataFrame(np.random.random(20).reshape((10,2)), columns=list('AB'))
df1
```

<table>
<thead>
<tr>
  <th></th>
  <th>A</th>
  <th>B</th>
</tr>
</thead>
<tbody><tr>
  <td>0</td>
  <td>0.407007</td>
  <td>0.286344</td>
</tr>
<tr>
  <td>1</td>
  <td>0.140339</td>
  <td>0.036872</td>
</tr>
<tr>
  <td>2</td>
  <td>0.450920</td>
  <td>0.320719</td>
</tr>
<tr>
  <td>3</td>
  <td>0.783196</td>
  <td>0.987610</td>
</tr>
<tr>
  <td>4</td>
  <td>0.011362</td>
  <td>0.263995</td>
</tr>
<tr>
  <td>5</td>
  <td>0.968380</td>
  <td>0.628029</td>
</tr>
<tr>
  <td>6</td>
  <td>0.465733</td>
  <td>0.618144</td>
</tr>
<tr>
  <td>7</td>
  <td>0.441445</td>
  <td>0.426087</td>
</tr>
<tr>
  <td>8</td>
  <td>0.831295</td>
  <td>0.911736</td>
</tr>
<tr>
  <td>9</td>
  <td>0.447908</td>
  <td>0.653442</td>
</tr>
</tbody></table>


## 什么是链式
链式就是进行多次同类型的操作，比如`a = b = c = 4`就是一个链式操作。在这里的链式操作主要是指，对于一个pandas格式的表，选取两次或者以上次数的其中结果。 
比如选取其中A值小于0.3的行得到：

```python
df1[df1.A < 0.3]
```

结果如下：
<table>
<thead>
<tr>
  <th></th>
  <th>A</th>
  <th>B</th>
</tr>
</thead>
<tbody><tr>
  <td>1</td>
  <td>0.140339</td>
  <td>0.036872</td>
</tr>
<tr>
  <td>4</td>
  <td>0.011362</td>
  <td>0.263995</td>
</tr>
</tbody></table>


那么选取其中所有A<0.3的B列值可以写为：

```python
df1[df1.A < 0.3].B
```

得到：

```python
1 0.036872 
4 0.263995 
Name: B, dtype: float64
```

以上中，先选取左右`A<0.3`的行，其次再从中选取B列，上述操作将其分为两部，那么这样就是链式操作。

## 那么链式赋值呢？
如果此时要进行：选取其中所有`A<0.3`的B列值并将其赋值为1，如果进行：

```python
df1[df1.A < 0.3].B = 1
```

此时就会报错SettingWithCopyWarning的Warning 
如果此时再查看df1里面的值，会发现完全没有改变。 
【所以此时这个爆warning是非常有意义的，如果单纯的忽略掉则会导致程序错误。】

根据会提示用loc函数。 
用loc函数如下：

```python
df1.loc[df1.A<0.3, 'B'] = 1
```

运行完后再查看就会发现df1里面的对应着都变为1了。

## 出现的原因
官方的解释是，pandas这个机制设计如此，凡事出现链式赋值的情况，pandas都是不能够确定到底返回的是一个引用还是一个拷贝。所以遇到这种情况就干脆报warning

## 更隐蔽的链式赋值
有些时候比如将链式给拆解成为多步的时候，就是一些隐式的情况。 
比如：

```python
df2 = df1.loc[df1.A<0.3]
df2.loc[1,'B'] = 2
```

虽然这两步每步都用了loc，但是凡是把取值（GET）操作分为两步的，仍然是链式赋值的状态，所以仍然会报warning。 
不过再次查看df2发现df2的值确实已经改变过来了，查看df1的值，发现df1的值没有变。 
所以之前那次用loc取出的就是引用，这次就变成拷贝了。也就是说链式赋值是一个要避免的状态。 
如果明确说要用拷贝怎么办，就是如下：

```python
df2 = df1.loc[df1.A<0.3].copy()
```

## 假阴性
有些情况下，出现了链式拷贝但是不会报错，所以会出现假阴性【相对应的，也会出现假阳性，即报错了，但是实际上没有链式赋值出现，但是这种一般出现在早起pandas版本中，现在新版本应该不会有了】 
比如下面个：

```python
df1.loc[df1.A<0.3, ('A','B')].B = 3
df1
```

此时没有报warning，但是再查看df1发现仍然没有任何改变。

## 总结
这里总结一下pandas的这个问题：

- 避免任何形式的链式赋值，有可能会报warning也有可能不会报。而且即使报了，可能有问题，也可能没问题。
- 如果需要用到多级选取，则用loc
- 如果需要用到拷贝，则直接加copy()函数