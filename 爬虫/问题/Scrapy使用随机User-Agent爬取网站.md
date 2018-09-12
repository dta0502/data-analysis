# Scrapy使用随机User-Agent爬取网站

在爬虫爬取过程中，我们常常会使用各种各样的伪装来降低被目标网站反爬的概率，其中随机更换User-Agent就是一种手段。

在scrapy中，其实已经内置了User-Agent中间件：
```python
class UserAgentMiddleware(object):
    """This middleware allows spiders to override the user_agent"""

    def __init__(self, user_agent='Scrapy'):
        self.user_agent = user_agent

    @classmethod
    def from_crawler(cls, crawler):
        o = cls(crawler.settings['USER_AGENT'])
        crawler.signals.connect(o.spider_opened, signal=signals.spider_opened)
        return o

    def spider_opened(self, spider):
        self.user_agent = getattr(spider, 'user_agent', self.user_agent)

    def process_request(self, request, spider):
        if self.user_agent:
            request.headers.setdefault(b'User-Agent', self.user_agent)
```
上面是scrapy自带的UserAgentMiddleware中间件，通过代码可以发现，如果我们没有在setting配置文件中设置headers的User-Agent，scrapy会把User-Agent设置为"Scrapy"。

## 原理
当我们通过 spider yield 一个 request 的时候，首先通过 spider middlewares 到达 scrapy engine，然后 engine 将 request 放到 scheduler 的队列中，通过 scheduler 调度队列中的 request ，scheduler 选中一个 request 后，将 request 通过 engine 传递给 downloader，在这之前，必然会经过 downloader middlewares，downloader 下载好之后，将 response 返回给 engine，engine 在将 response 返回给 spider，我们就可以在 spider 中调用 callback 进行解析，简单的流程大概就是这样。

那么，我们在将 request 提交给 downloader 进行下载之前，就需要将 User-Agent 进行变化，也就是每次都需要随机取一个 User-Agent 提交到 downloader 进行下载。在提交到 downloader 的时候，必然会经过 downloader middlewares，所以我们实现随机获取 User-Agent 的逻辑部分，可以在 downloader midllewares 这里实现。

## 第一种方法
可以把多个User-Agent作为一个配置在setting文件中
```python
user_agent_list = [
    "ua1",
    "ua2",
    "ua3",
]
```
然后再编写downloader midllewares
```python
class RandomUserAgentMiddleware(object):
    def __init__(self, crawler):
        super(RandomUserAgentMiddleware, self).__init__()
        self.user_agent_list = crawler.get("user_agent_list", [])

    @classmethod
    def from_crawler(cls, crawler):
        return cls(crawler)

    def process_request(self, request, spider):
        #方法1
        request.headers.setdefault("User-Agent", random.choice(self.user_agent_list))
        #方法2
        request.headers['User-Agent'] = random.choice(self.user_agent_list)
```
settings.py中的配置方法：
```python
DOWNLOADER_MIDDLEWARES = {
    'scrapy.contrib.downloadermiddleware.useragent.UserAgentMiddleware': None,
    'crawl_spider.middlewares.RandomUserAgentMiddleware': 543,
}
```
先把scrapy自带的UserAgentMiddleware置为None,再增加我们自己写的中间件便可，

这样做可以实现切换User-Agent的功能，但是第一需要自己维护一个大的`User-Agent list`在配置文件中，第二就是有局限性，毕竟维护的User-Agent不会有那么的大而全，所以这里介绍另一种方法。


## 第二种方法（推荐）
fake-useragent 这个库提供了我们随机选择useragent的功能。
感兴趣的同学可以深入研究下源码，源码很简单，这里只介绍怎么在scrapy中使用它。
```python
class RandomUserAgentMiddleware(object):
    def __init__(self, crawler):
        super(RandomUserAgentMiddleware, self).__init__()
        self.ua = UserAgent()
        self.ua_type = crawler.settings.get("RANDOM_UA_TYPE", "random")

    @classmethod
    def from_crawler(cls, crawler):
        return cls(crawler)

    def process_request(self, request, spider):
        def get_ua():
            return getattr(self.ua, self.ua_type)
        request.headers['User-Agent'] = get_ua()
```

首先我们在setting配置文件中设置一个变量`RANDOM_UA_TYPE`，它的功能是可以按照我们自己配置的值来选择useragent。
```python
# 随机选择UA
RANDOM_UA_TYPE = "random"
# 只选择ie的UA
RANDOM_UA_TYPE = "ie"
```
当然了，最终我们还要把我们的RandomUserAgentMiddleware中间件配置到setting中：
```python
DOWNLOADER_MIDDLEWARES = {
    'crawl_spider.middlewares.RandomUserAgentMiddleware': 543,
}
```
至此，完成了scrapy加随机User-Agent的需求。

