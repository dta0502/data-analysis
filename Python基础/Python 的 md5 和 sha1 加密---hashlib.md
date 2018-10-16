
# Python 的 md5 和 sha1 加密---hashlib

## md5 与 sha1
MD5的全称是`Message-Digest Algorithm 5（信息-摘要算法）`。128位长度。目前MD5是一种不可逆算法。具有很高的安全性。它对应任何字符串都可以加密成一段唯一的固定长度的代码。

md5的应用场景： 
- 加密网站注册用户的密码。（但去年的各大网站密码泄漏事件确实让人蛋疼……）
- 网站用户上传图片 / 文件后，计算出 MD5 值作为文件名。（MD5可以保证唯一性）
- key-value数据库中使用MD5值作为key。
- 比较两个文件是否相同。（大家在下载一些资源的时候，就会发现网站提供了MD5值，就是用来检测文件是否被篡改） 


SHA1的全称是`Secure Hash Algorithm（安全哈希算法）`。SHA1基于MD5，加密后的数据长度更长，它对长度小于264的输入，产生长度为160 bit的散列值。比MD5多32位。因此，比MD5更加安全，但SHA1的运算速度就比 MD5 要慢了。


```python
import hashlib

text = 'This is a md5 text.'

text_md5 = hashlib.md5(text.encode('utf-8'))
text_md5.hexdigest()
```




    '3343b9dffc0efbab68a57bba3f419a1b'




```python
text_sha1 = hashlib.sha1(text.encode('utf-8'))
text_sha1.hexdigest()
```




    'd76e2c3830efabb6c7986d9c71fcc040bfae5d6e'




```python
# 或者采用如下的方式进行散列
m = hashlib.md5()
m.update(text.encode('utf-8'))
m.hexdigest()
```




    '3343b9dffc0efbab68a57bba3f419a1b'



对要散列编码的文本，必须要重新指定编码，一般选择utf-8，详见[“TypeError: Unicode-objects must be encoded before hashing”](http://stackoverflow.com/questions/7585307/typeerror-unicode-objects-must-be-encoded-before-hashing) 。

## 大文件的哈希散列
上面说过可以用MD5来检测两个文件是否相同，但想想，如果是两个很大的文件，担心内存不够用，这时怎么办？

这就要使用`update`方法了。代码如下：


```python
def gen_md5(f):
    f_md5 = hashlib.md5()
    while True:
        data = f.read(1024)
        if not data:
            break
        f_md5.update(data)
    return f_md5.hexdigest()
```

一个更 Python 风格的实现：


```python
def md5(fname):
    hash_md5 = hashlib.md5()
    with open(fname, "rb") as f:
        for chunk in iter(lambda: f.read(4096), b""):
            hash_md5.update(chunk)
    return hash_md5.hexdigest()
```
