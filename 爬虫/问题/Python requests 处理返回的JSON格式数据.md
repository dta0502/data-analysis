# Python requests 处理返回的JSON格式数据

参考：[JSON 响应内容](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html)

Requests 中也有一个内置的 JSON 解码器，助你处理 JSON 数据：

```python
>>> import requests

>>> r = requests.get('https://api.github.com/events')
>>> r.json()
[{u'repository': {u'open_issues': 0, u'url': 'https://github.com/...
```

如果 JSON 解码失败， `r.json()` 就会抛出一个异常。例如，响应内容是 `401 (Unauthorized)`，尝试访问 `r.json() `将会抛出` ValueError: No JSON object could be decoded `异常。

需要注意的是，成功调用` r.json()` 并**不**意味着响应的成功。有的服务器会在失败的响应中包含一个 JSON 对象（比如 `HTTP 500` 的错误细节）。这种 JSON 会被解码返回。要检查请求是否成功，请使用 `r.raise_for_status() `或者检查 `r.status_code` 是否和你的期望相同。
