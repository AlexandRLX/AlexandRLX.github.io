---
title: Python中的设计模式
author: c cm
layout: post
permalink: /pattern_design_in_python/
categories: python
tags: python
description:
---
## 0. iterator pattern

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

## 5. singleton pattern
传统的单例在python中并不常用，甚至是anti-pattern。为了避免创建一堆实例浪费memory，如果实在要用单例，Python中建议用module-level variables模拟单例模式。

```python
class OneOnly(object):    _singleton = None    def __new__(cls, *args, **kwargs):        if not cls._singleton:            cls._singleton = super(OneOnly, cls).__new__(cls, *args, **kwargs)        return cls._singleton
```

## 6. template pattern
```python
class TemplateClass(object):
    def do_process(self):
        self.step1()
        self.step2()
        self.step3()
    
    def step1():
        pass
        
    def step2():
        raise NotImplementedError
        
    def step3():
        pass

class Task1(TemplateClass):
    def step2():
        pass
        
class Task2(TemplateClass):
    def step2():
        pass
```

*Reference*  
[Python 3 Object-oriented Programming](https://book.douban.com/subject/4823621/)
