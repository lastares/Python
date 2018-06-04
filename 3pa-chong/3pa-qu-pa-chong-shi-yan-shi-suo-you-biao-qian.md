```
# -*- coding: utf-8 -*-

import scrapy
class Tags(scrapy.Spider):
    name = 'tags'
    start_urls = [
        'http://lab.scrapyd.cn/'
    ]


    def parse(self, response):
        tags = response.css('.tags-list li a::text').extract()
        filename = 'tags.txt'
        for tag in tags:
            if(tag == '返回首页' or tag == 'SCRAPY中文网'):
                continue
            tag = tag.strip()
            with open(filename, 'a+') as f:
                f.write(tag + "\n")
                f.close()
```



