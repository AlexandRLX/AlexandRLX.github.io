---
title: Python参数传递
author: c cm
layout: post
permalink: /python_parameter_passing/
categories: 
tags: python
description:
---

Python参数传递方式: call by sharing，means that each formal parameter of the function gets a copy of each reference in the arguments.

```python
def f(a, b):
    a += b
    return a
```

```
>> a = (1, 2)
>> b = (3, 4)
>> f(a, b)
(1, 2, 3, 4)
>> a, b
>> (1, 2), (3, 4)
```

ref: Fluent Python