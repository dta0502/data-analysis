# Python操作dict时避免出现KeyError的几种方法

在读取dict的key和value时，如果key不存在，就会触发KeyError错误，如：
```python
t = {
    'a': '1',
    'b': '2',
    'c': '3',
}
print(t['d'])
```
就会出现：
```python
KeyError: 'd'
```

## 第一种解决方法
首先测试key是否存在，然后才进行下一步操作，如：
```python
t = {
    'a': '1',
    'b': '2',
    'c': '3',
}
if 'd' in t:
    print(t['d'])
else:
    print('not exist')
```

# 第二种解决方法

利用dict内置的`get(key[,default])`方法，如果key存在，则返回其value,否则返回default;使用这个方法永远不会触发KeyError，如：
```python
    t = {
        'a': '1',
        'b': '2',
        'c': '3',
    }
    print(t.get('d'))
```
加上default参数：
```python
t = {
    'a': '1',
    'b': '2',
    'c': '3',
}
print(t.get('d', 'not exist'))
print(t)
```


## 第三种解决方法

利用dict内置的`setdefault(key[,default])`方法，如果key存在，则返回其value;否则插入此key，其value为default，并返回default;使用这个方法也永远不会触发KeyError，如：
```python
t = {
    'a': '1',
    'b': '2',
    'c': '3',
}
print(t.setdefault('d'))
print(t)
```
加上default参数：
```python
t = {
    'a': '1',
    'b': '2',
    'c': '3',
}
print(t.setdefault('d', 'not exist'))
print(t)
```







