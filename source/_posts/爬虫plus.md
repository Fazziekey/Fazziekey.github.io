---
title: Beautiful Soup
toc: true
reward:
copyright: true
date: 2020-08-06 00:00:49
tags:
    - 爬虫
    - Statistic Analysis
categories:
    - 《栈溢出工程师》
---
在使用正则化匹配时无法去除标签，所以使用BeautifulSoup，BeautifulSoup可以很好的第三方用于解析网站，查找信息的包
<!--more-->
# Beautiful soup basic
## 安装Beautifulsoup
命令行或Anaconda Promote cd到`../Lib/site-package`

    pip install beautifulSoup4
    
## 基本使用方法 
### 找到标签
    from bs4 import BeautifulSoup
    soup = BeautifulSoup(html, features='lxml')
    print(soup.h1) #打印<h1>标签内容
    
    
### 查找链接
    
    all_href = soup.find_all('a')
    all_href = [l['href'] for l in all_href]
    print('\n', all_href)
    
## 根据CSS查找
CSS定义了class，可以根据class来查找想要的信息，对于以下html代码

    <head>
    ...
    <style>
    .jan {
        background-color: yellow;
    }
    ...
    .month {
        color: red;
    }
    </style>
    </head>
    <body>
    ...
    <ul>
        <li class="month">一月</li>
        <ul class="jan">
            <li>一月一号</li>
            <li>一月二号</li>
            <li>一月三号</li>
        </ul>
        ...
    </ul>
    </body>
  
  在python中查找
  
    
        soup = BeautifulSoup(html, features='lxml')
    # use class to narrow search
    month = soup.find_all('li', {"class": "month"})
    for m in month:
        print(m.get_text())
    
    """
    一月
    二月
    三月
    四月
    五月
    """
    
        jan = soup.find('ul', {"class": 'jan'})
    d_jan = jan.find_all('li')              # use jan as a parent
    for d in d_jan:
        print(d.get_text())
    
    """
    一月一号
    一月二号
    一月三号
    """
    
## BeautifulSoup使用正则表达式
### 利用正则表达选取图片
在网页中的图片都在这样一个**tag**中

    <td>
        <img src="https://.../.jpg">
    </td>
    
    
所以, 我们可以用 soup 将这些 <img> tag 全部找出来, 但是每一个 img 的链接(src)都可能不同. 或者每一个图片有的可能是 jpg 有的是 png, 如果我们只想挑选 jpg 形式的图片, 我们就可以用这样一个正则 r'.*?\.jpg' 来选取. 把正则的 compile 形式放到 BeautifulSoup 的功能中, 就能选到符合要求的图片链接了.

    soup = BeautifulSoup(html, features='lxml')
    
    img_links = soup.find_all("img", {"src": re.compile('.*?\.jpg')})
    for link in img_links:
        print(link['src'])
        
同样的，查找链接

    links = soup.find_all('a', {'href': re.compile('https://morvan.*')})
    for link in course_links:
        print(link['href'])

# 网络爬虫
爬虫会在网络中按照一定规律移动


在百度百科的爬虫词条，`<a href=https://baike.baidu.com/item/网络爬虫/5162711target='_blank' >`页面中所有的链接都以item开头，但不是所有词条，所有需要进一步筛选

    <a target="_blank" href="/item/%E8%9C%98%E8%9B%9B/8135707" data-lemmaid="8135707">蜘蛛</a>
    <a target="_blank" href="/item/%E8%A0%95%E8%99%AB">蠕虫</a>
    <a target="_blank" href="/item/%E9%80%9A%E7%94%A8%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E">通用搜索引擎</a>
    
## 制作爬虫

导入一些模块, 设置起始页. 并将 /item/... 的网页都放在 his 中, 做一个备案, 记录我们浏览过的网页.

    from bs4 import BeautifulSoup
    from urllib.request import urlopen
    import re
    import random


    base_url = "https://baike.baidu.com"
    his = ["/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711"]
接着我们先不用循环, 对一个网页进行处理, 走一遍流程, 然后加上循环, 让我们的爬虫能在很多网页中爬取. 下面做的事情, 是为了在屏幕上打印出来我们现在正在哪张网页上, 网页的名字叫什么.

    url = base_url + his[-1]
    
    html = urlopen(url).read().decode('utf-8')
    soup = BeautifulSoup(html, features='lxml')
    print(soup.find('h1').get_text(), '    url: ', his[-1])

    # 网络爬虫     url:  /item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711
    
接下来我们开始在这个网页上找所有符合要求的 /item/ 网址. 使用一个正则表达式(正则教程) 过滤掉不想要的网址形式. 这样我们找到的网址都是 `/item/%xx%xx%xx...` 这样的格式了. 之后我们在这些过滤后的网页中随机选一个, 当做下一个要爬的网页. 不过有时候很不幸, 在 sub_urls 中并不能找到合适的网页, 我们就往回跳一个网页, 回到之前的网页中再随机抽一个网页做同样的事.

    # find valid urls
    sub_urls = soup.find_all("a", {"target": "_blank", "href": re.compile("/item/(%.{2})+$")})
    
    if len(sub_urls) != 0:
        his.append(random.sample(sub_urls, 1)[0]['href'])
    else:
        # no valid sub link found
        his.pop()
    print(his)

    # ['/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711', '/item/%E4%B8%8B%E8%BD%BD%E8%80%85']
    
有了这套体系, 我们就能把它放在一个 for loop 中, 让它在各种不同的网页中跳来跳去.

    his = ["/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711"]
    
    for i in range(20):
        url = base_url + his[-1]

    html = urlopen(url).read().decode('utf-8')
    soup = BeautifulSoup(html, features='lxml')
    print(i, soup.find('h1').get_text(), '    url: ', his[-1])

    # find valid urls
    sub_urls = soup.find_all("a", {"target": "_blank", "href": re.compile("/item/(%.{2})+$")})

    if len(sub_urls) != 0:
        his.append(random.sample(sub_urls, 1)[0]['href'])
    else:
        # no valid sub link found
        his.pop()
这样我们就能观看我们的爬虫现在爬去了哪? 是不是爬到了和 网页爬虫 起始页完全不相关的地方去了.

    0 网络爬虫     url:  /item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711
    1 路由器     url:  /item/%E8%B7%AF%E7%94%B1%E5%99%A8
    2 服务等级     url:  /item/%E6%9C%8D%E5%8A%A1%E7%AD%89%E7%BA%A7
    ...
    17 呼损率     url:  /item/%E5%91%BC%E6%8D%9F%E7%8E%87
    18 服务等级     url:  /item/%E6%9C%8D%E5%8A%A1%E7%AD%89%E7%BA%A7
    19 呼损率     url:  /item/%E5%91%BC%E6%8D%9F%E7%8E%87
    


