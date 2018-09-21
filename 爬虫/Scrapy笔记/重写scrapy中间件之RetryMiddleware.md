# 重写scrapy中间件RetryMiddleware


在爬取得过程中难免会遇到各种错误，如timeout或者404。而且在用ip代理池时，不是所有的代理都是稳定的，所以对于失败的代理我们需要做一些处理，例如删除操作。而由于不稳定代理引起的请求我们需要重新发起。这时候就有必要重写RetryMiddleware，来实现一些自己想要的操作。



- 理解RetryMiddleware源码

- 重写RetryMiddleware

## 




RetryMiddleware部分源码

```python
class RetryMiddleware(object):

    # 当遇到以下Exception时进行重试
    EXCEPTIONS_TO_RETRY = (defer.TimeoutError, TimeoutError, DNSLookupError, ConnectionRefusedError, ConnectionDone, ConnectError, ConnectionLost, TCPTimedOutError, ResponseFailed, IOError, TunnelError)

    def __init__(self, settings):
        '''
        这里涉及到了settings.py文件中的几个量
        RETRY_ENABLED: 用于开启中间件，默认为TRUE
        RETRY_TIMES: 重试次数, 默认为2
        RETRY_HTTP_CODES: 遇到哪些返回状态码需要重试, 一个列表，默认为[500, 503, 504, 400, 408]
        RETRY_PRIORITY_ADJUST：调整相对于原始请求的重试请求优先级，默认为-1
        '''
        if not settings.getbool('RETRY_ENABLED'):
            raise NotConfigured
        self.max_retry_times = settings.getint('RETRY_TIMES')
        self.retry_http_codes = set(int(x) for x in settings.getlist('RETRY_HTTP_CODES'))
        self.priority_adjust = settings.getint('RETRY_PRIORITY_ADJUST')

    def process_response(self, request, response, spider):
        # 在之前构造的request中可以加入meta信息dont_retry来决定是否重试    
        if request.meta.get('dont_retry', False):
            return response

        # 检查状态码是否在列表中，在的话就调用_retry方法进行重试
        if response.status in self.retry_http_codes:
            reason = response_status_message(response.status)
            # 在此处进行自己的操作，如删除不可用代理，打日志等
            return self._retry(request, reason, spider) or response
        return response

    def process_exception(self, request, exception, spider):
        # 如果发生了Exception列表中的错误，进行重试
        if isinstance(exception, self.EXCEPTIONS_TO_RETRY) \
                and not request.meta.get('dont_retry', False):
            # 在此处进行自己的操作，如删除不可用代理，打日志等
            return self._retry(request, exception, spider)

```

## 重写RetryMiddleware

自己想要的操作在上面已经标出来了，只要在其中加入自己的代码就可以满足大部分要求。具体如下：

```python
class MyRetryMiddleware(RetryMiddleware):
    logger = logging.getLogger(__name__)

    def delete_proxy(self, proxy):
        if proxy:
            # delete proxy from proxies pool


    def process_response(self, request, response, spider):
        if request.meta.get('dont_retry', False):
            return response
        if response.status in self.retry_http_codes:
            reason = response_status_message(response.status)
            # 删除该代理
            self.delete_proxy(request.meta.get('proxy', False))
            time.sleep(random.randint(3, 5))
            self.logger.warning('返回值异常, 进行重试...')
            return self._retry(request, reason, spider) or response
        return response


    def process_exception(self, request, exception, spider):
        if isinstance(exception, self.EXCEPTIONS_TO_RETRY) \
                and not request.meta.get('dont_retry', False):
            # 删除该代理
            self.delete_proxy(request.meta.get('proxy', False))
            time.sleep(random.randint(3, 5))
            self.logger.warning('连接异常, 进行重试...')

            return self._retry(request, exception, spider)
```

其中_retry方法有如下作用： 
- 
1、对request.meta中的retry_time进行+1 

- 2、将retry_times和max_retry_time进行比较，如果前者小于等于后者，利用copy方法在原来的request上复制一个新request，并更新其retry_times，并将dont_filter设为True来防止因url重复而被过滤。


