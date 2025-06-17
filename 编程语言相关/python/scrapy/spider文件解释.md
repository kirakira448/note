
```python
import scrapy


class KaoshibaoSpiderSpider(scrapy.Spider):
    name = "kaoshibao_spider"
    allowed_domains = ["zaixiankaoshi.com"]
    start_urls = ["https://zaixiankaoshi.com"]

    def parse(self, response):
        pass
```

- name: 它定义了蜘蛛的唯一名称
- allowed_domains: 它包含了蜘蛛抓取的基本URL；
- start_urls: 蜘蛛开始爬行的URL列表；
- parse(): 这是提取并解析刮下数据的方法；