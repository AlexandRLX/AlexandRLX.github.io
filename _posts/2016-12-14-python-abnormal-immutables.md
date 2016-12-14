---
title: Python immutables异常行为
author: c cm
layout: post
permalink: /python_abnormal_immutables/
categories: 
tags: python
description:
---

```python
from copy import copy
>>> a = [1, 2, 3]
>>> b = a[:]
>>> a is b  # 1
>>> copy(a) is a  # 2
>>> c = (1, 2, 3)
>>> d = c[:]
>>> e = (1, 2, 3)
>>> c is d  # 3
>>> copy(c) is c  # 4
>>> c is e  # 5
>>> f = "ABC"
>>> g = "ABC"
>>> f is g  # 6
>>> copy(f) is f  # 7
>>> h = f[:]
>>> f is h  # 8
```

答案是F F T T F T T T 你猜对了吗？
