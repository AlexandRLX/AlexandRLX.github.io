---
title: Bokeh Server
author: c cm
layout: post
permalink: /bokeh_server/
categories: python
tags:
description:
---
Bokeh是我第三爱的画图工具，第一是R下的ggplot，第二是[plotly](https://plot.ly)。

Bokeh提供了[server](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html)框架，能很速度地搭起一个基于数据的dashboard。

可以从[示例代码](https://github.com/bokeh/bokeh/tree/master/examples/app)开始入手。

启动方式有两种：

```
bokeh serve --show sliders.py
bokeh serve --show slider_dir\
```

最基本的结构：

```python
def get_dataset()
def make_plot()
def update_plot()

index_select = Select(value=index, title='Index', options=indexes)
source_data = get_dataset(some_data, index)
plot = make_plot(source_data)
controls = column(index_select)

index_select.on_change('value', update_plot)
curdoc().add_root(row(plot, controls))
curdoc().title = "Some Title"
```
