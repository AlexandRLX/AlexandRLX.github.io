---
title: Pattern Design in Python
author: c cm
layout: post
permalink: /pattern_design_in_python/
categories: python
tags: python
description:
---

## 1. decorator pattern
```python
@wrapper_fun
def some_fun(para):
    pass
```


## 2. observer pattern
```python
class Core(object):    def __init__(self):        self.observers = []        self._cnt = 0
    def attach(self, observer):        self.observers.append(observer)
    @property    def count(self):        return self._cnt
            @count.setter    def count(self, value):        self._cnt = value        self._update_observers()
    
    def _update_observers(self):        for observer in self.observers:            observer()

class Observer(object):
    def __init__(self, core):
        self.core = core

    def __call__(self):
        pass

def __main__():
    c = Core()
    o = Observer(c)
    c.attach(o)
```

## 3. strategy pattern
```python
class Abstraction(object):
    def some_method(self):
        raise NotImplementedError

class Implementation1(Abstraction):
    def some_method(self):
        pass

class Implementation2(Abstraction):
    def some_method(self):
        pass

def __main__():
    i = Implementation1()
    i.some_method()
```

```python
class Implementation1(object):
    def __call__(self):
        pass

class Implementation2(object):
    def __call__(self):
        pass

def __main__():
    Implementation1()
```

## 4. state pattern
```python
class Context(object):
    def __init__(self):
        self.state = TransState()
    
    def process():
        self.state.process(self)

class State(object):
    def process(context):
        pass

class TransState(State):
    def process(context):
        if some_condition:
            context.state = State1()
        else:
            context.state = State2()
        pass

class State1(State):
    def process(context):
        context.state = TransState()
        pass

class State2(State):
    def process(context):
        context.state = TransState()
        pass
```
