
# Python中threading的join和setDaemon的区别及用法

Python多线程编程时，经常会用到`join()`和`setDaemon()`方法，今天特地研究了一下两者的区别。

## join()方法

主线程A中，创建了子线程B，并且在主线程A中调用了`B.join()`，那么，主线程A会在调用的地方等待，直到子线程B完成操作后，才可以接着往下执行，那么在调用这个线程时可以使用被调用线程的join方法。


### 原型

```python
join([timeout])
```

里面的参数时可选的，代表线程运行的最大时间，即如果超过这个时间，不管这个此线程有没有执行完毕都会被回收，然后主线程或函数都会接着执行的。

### 例子1


```python
import threading
import time

class MyThread(threading.Thread):
    def __init__(self,id):
        threading.Thread.__init__(self)
        self.id = id
    def run(self):
        x = 0
        time.sleep(10)
        print(self.id)

if __name__ == "__main__":
    t1=MyThread(999)
    t1.start()
    for i in range(5):
        print(i)
```

    0
    1
    2
    3
    4
    999
    

机器上运行时，4和999之间，有明显的停顿。解释：线程`t1 start`后，主线程并没有等线程t1运行结束后再执行，而是先把5次循环打印执行完毕（打印到4），然后`sleep(10)`后，线程t1把传进去的999才打印出来。

### 例子2

现在，我们把`join()`方法加进去(其他代码不变)，看看有什么不一样。


```python
import threading
import time

class MyThread(threading.Thread):
    def __init__(self,id):
        threading.Thread.__init__(self)
        self.id = id
    def run(self):
        x = 0
        time.sleep(10)
        print(self.id)

if __name__ == "__main__":
    t1=MyThread(999)
    t1.start()
    t1.join()
    for i in range(5):
        print(i)
```

    999
    0
    1
    2
    3
    4
    

机器上运行时，999之前，有明显的停顿。解释：线程`t1 start`后，主线程停在了`join()`方法处，等`sleep(10)`后，线程t1操作结束被join，接着，主线程继续循环打印。

## setDaemon()方法

主线程A中，创建了子线程B，并且在主线程A中调用了`B.setDaemon()`,这个的意思是，设置B为守护进程（**注意：表示你在说这个线程是不重要的**），要是主线程A执行结束了，就不管子线程B是否完成,一并和主线程A退出。这就是setDaemon方法的含义，这基本和join是相反的。**此外，还有个要特别注意的：必须在`start()`方法调用之前设置，如果不设置为守护线程，程序会被无限挂起。**


```python
import threading
import time

class MyThread(threading.Thread):
    def __init__(self,id):
        threading.Thread.__init__(self)
    def run(self):
        time.sleep(5)
        print("This is " + self.getName())

if __name__ == "__main__":
    t1=MyThread(999)
    t1.setDaemon(True)
    t1.start()
    print("I am the father thread.")
```

    I am the father thread.
    This is Thread-8
    

可以看出，子线程t1中的内容并未打出。解释：`t1.setDaemon(True)`的操作，将父线程设置为了守护线程。根据`setDaemon()`方法的含义，父线程打印内容后便结束了，不管子线程是否执行完毕了。

程序运行中，执行一个主线程，如果主线程又创建一个子线程，主线程和子线程就分兵两路，分别运行，那么当主线程完成想退出时，会检验子线程是否完成。如果子线程未完成，则主线程会等待子线程完成后再退出。但是有时候我们需要的是，只要主线程完成了，不管子线程是否完成，都要和主线程一起退出，这时就可以用setDaemon方法了。
