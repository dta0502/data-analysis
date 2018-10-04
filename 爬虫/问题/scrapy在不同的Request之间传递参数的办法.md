# scrapy在不同的Request之间传递参数的办法

## scrapy在不同的抓取级别的Request之间传递参数的办法


下面的范例中，`parse_item`方法通过`meta`向`parse_details`方法中传递参数`item`，这样就可以在`parse_details`方法中获取到这个参数的值。


注意：`meta={'item': item}`中如果有多个参数，则每个参数间用英文逗号隔开，例如：`meta={'item': item,'item2': item2}`



```python

class MySpider(BaseSpider):  
    name = 'myspider'  
    start_urls = (  
        'http://example.com/page1',  
        'http://example.com/page2',  
        )  
  
    def parse(self, response):  
        # collect `item_urls`  
        for item_url in item_urls:  
            yield Request(url=item_url, callback=self.parse_item)  
  
    def parse_item(self, response):  
        item = MyItem()  
        # populate `item` fields  
        yield Request(url=item_details_url, meta={'item': item},  
            callback=self.parse_details)  
  
    def parse_details(self, response):  
        item = response.meta['item']  
        # populate more `item` fields  
        return item  


```


[代码片段来自于: http://www.sharejs.com/codes/python/6398](http://www.sharejs.com/codes/python/6398)

