---
title: timedelta求和
author: c cm
layout: post
permalink: /sum_timedelta/
categories: 
tags: python
description:
---

```python
>>> from datetime import timedelta
>>> td1 = timedelta(10)
>>> td2 = timedelta(20)
>>> td1 + td2
datetime.timedelta(30)
>>> sum([td1, td2])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'datetime.timedelta'
>>> sum([td1, td2], timedelta())
datetime.timedelta(30)
```

直接sum失败的原因是[sum](https://docs.python.org/3/library/functions.html#sum)默认从int: 0开始往上加，通过增加初始值timedelta()即可搞定。