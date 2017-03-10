---
title: ElasticSearch 搜索101
author: c cm
layout: post
permalink: /elasticsearch_101/
categories:
tags:
description:
---

## ElasticSearch是啥

> 多年前，一个叫做Shay Banon的刚结婚不久的失业开发者，由于妻子要去伦敦学习厨师，他便跟着也去了。在他找工作的过程中，为了给妻子构建一个食谱的搜索引擎，他开始构建一个早期版本的Lucene。  
直接基于Lucene工作会比较困难，所以Shay开始抽象Lucene代码以便Java程序员可以在应用中添加搜索功能。他发布了他的第一个开源项目，叫做“Compass”。  
后来Shay找到一份工作，这份工作处在高性能和内存数据网格的分布式环境中，因此高性能的、实时的、分布式的搜索引擎也是理所当然需要的。然后他决定重写Compass库使其成为一个独立的服务叫做Elasticsearch。  
第一个公开版本出现在2010年2月，在那之后Elasticsearch已经成为Github上最受欢迎的项目之一，代码贡献者超过300人。一家主营Elasticsearch的公司就此成立，他们一边提供商业支持一边开发新功能，不过Elasticsearch将永远开源且对所有人可用。
Shay的妻子依旧等待着她的食谱搜索……

## 搜索基本语法
可以在
```
http://host:9200/_plugin/head/
```
里测试。

基本语法：  

```
{"query": {"match": {"index": "things to be matched"}}}
```

```
{"query": {"match_phrase": {"index": "things to be exact matched"}}}
```

## Python API
首先安装[elasticsearch-py](https://elasticsearch-py.readthedocs.io/en/master/)。

```
pip install elasticsearch
```

在python中最简单的用法示例：

```python
import elasticsearch
es = elasticsearch.Elasticsearch(host="")
res = es.search(
    index="some_index", 
    body={"query": {"match_phrase": {}}},
    size=20)
for hit in res['hits']['hits']:
    print(hit)
```
elasticsearch搜索返回结果一般默认5/10个，如果想要更多结果，可以增大size。或者加上scroll参数，多次取数。

```python
res = es.earch(
    index="some_index",
    scroll="2m",
    search_type="scan",
    size=10,
    body={"query_all":{}}
)
scroll_id = res['_scroll_id']
total_hits = res['hits']['total']

while (total_hits > 0):
    res = es.scroll(scroll_id = scroll_id, scroll="2m")
    scroll_id = res['_scroll_id']
    total_hits = res['hits']['total']
```


ref: [ES权威指南中文版](https://es.xiaoleilu.com)
