# scrapy 爬网站 显示 Filtered offsite request to 错误

查看日志 发现报
```
2018-09-12 00:27:58 [scrapy.spidermiddlewares.offsite] DEBUG: Filtered offsite request to 'book.douban.com': <GET https://book.douban.com/top250?start=25>
```

官方对这个的解释，是你要request的地址和allow_domain里面的冲突，从而被过滤掉。可以停用过滤功能。
```python
yield Request(url, callback=self.parse_item, dont_filter=True)
```