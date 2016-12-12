---
title: python连接kafka
author: c cm
layout: post
permalink: /python_kafka_client/
categories: python
tags:
description:
---

调研了[相关client](https://cwiki.apache.org/confluence/display/KAFKA/Clients#Clients-Python)后，选了git上更新频率和关注人数比较占优势的[kafka-python](https://github.com/dpkp/kafka-python)。

```
>>> pip install kafka-python
```

基本语法如下，更多见[doc](http://kafka-python.readthedocs.io/en/master/usage.html)

```python
>>> from kafka import KafkaConsumer
>>> consumer = KafkaConsumer('some_topic', bootstrap_servers=["host:port"])
>>> for msg in consumer:
        print(msg)
```