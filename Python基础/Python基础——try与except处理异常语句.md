# Python基础——try与except处理异常语句

## try/except介绍
默认情况下，在程序段的执行过程中，如果没有提供try/except的处理，脚本文件执行过程中所产生的异常消息会自动发送给程序调用端，如python shell，而python shell对异常消息的默认处理则是终止程序的执行并打印具体的出错信息。这也是在python shell中执行程序错误后所出现的出错打印信息的由来。
 
## try/except完整格式
python中`try/except/else/finally`语句的完整格式如下所示：
```python
try:
     Normal execution block
except A:
     Exception A handle
except B:
     Exception B handle
except:
     Other exception handle
else:
     if no exception,get here
finally:
     print("finally")   
```

## 捕获所有异常
```python
try:
	…
except Exception as e :
	print(e) # 其中e就是异常信息
```

## try/finnally
如果一段代码必须执行，也就是无论异常是否产生都要需要执行，那么此时需要使用finally，比如关闭文件，释放锁等。


