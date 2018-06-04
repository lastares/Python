```py
# -*- coding: utf-8 -*-

import scrapy
class mingyan(scrapy.Spider):
    name = 'my'
    # 参数化爬取
    def start_requests(self):
        url = 'http://lab.scrapyd.cn/'
        tag = getattr(self, 'tag', None)
        if(tag is not None):
            url = url + 'tag/' + tag
        yield scrapy.Request(url, callback=self.parse)


    def parse(self, response):
        mingyans = response.css('div.quote')
        next_page = response.css('li.next a::attr(href)').extract_first()

        for mingyan in mingyans:
            # 提取名言
            text = mingyan.css('.text::text').extract_first()
            # 提取作者
            author = mingyan.css('.author::text').extract_first()
            # 提取标签
            tags = mingyan.css('.tags .tag::text').extract()
            tags = ','.join(tags)

            # 爬取的语录文件 格式：作者-语录.txt
            filename = '%s-语录.txt' % author
            filename.encode('utf-8')
            f = open(filename, 'a+')
            f.write(text)
            f.write("\n")
            f.write('标签：' + tags)
            f.write("\n-----------------\n")
            f.close()
        # 判断是否有下一页
        if(next_page is not None):
            next_page = response.urljoin(next_page)
            yield scrapy.Request(next_page, callback=self.parse)

```



