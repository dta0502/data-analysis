# scrapy 输出csv文件数据之间有空行

## 问题描述
使用`scrapy crawl books -o books.csv`输出的文件中，数据之间是隔行输入的。


## 解决方案
[StackOverFlow参考](https://stackoverflow.com/questions/39477662/scrapy-csv-file-has-uniform-empty-rows)

To fix this in Scrapy 1.3, you can patch it by adding `newline=''` as parameter to `io.TextIOWrapper` in the `__init__ `method of the `CsvItemExporter` class in `scrapy.exporters`.
