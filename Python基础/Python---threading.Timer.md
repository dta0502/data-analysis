
# Python---threading.Timer

## 一、Timer类基本介绍
这个类表示一个动作应该在一个特定的时间之后运行 — 也就是一个计时器。Timer是Thread的子类， 因此也可以使用函数创建自定义线程。

```python
class threading.Timer(interval, function, args=[], kwargs={}) 
```

创建一个timer，在interval秒过去之后，它将以参数`args`和关键字参数`kwargs`运行function 。

## 二、简单例子


```python
from threading import Timer

def fun():
    print("hello, world")

if __name__=='__main__':
    t = Timer(5.0, fun)
    t.start() # 5秒后, "hello, world"将被打印
```

    hello, world
    

## 三、取消线程执行
- Timer通过调用它们的start()方法作为线程启动。
- Timer通过调用cancel()方法（在它的动作开始之前）停止。**停止timer，并取消timer动作的执行。这只在timer仍然处于等待阶段时才工作。**
- Timer在执行它的动作之前等待的时间间隔可能与用户指定的时间间隔不完全相同。




```python
from threading import Timer

def fun():
    print("hello, world")

if __name__=='__main__':
    t = Timer(5.0, fun)
    t.start() # 开始执行线程，但是不会打印"hello, world"
    t.cancel() # 因为cancel取消了线程的执行，所以fun()函数不会被执行
```
