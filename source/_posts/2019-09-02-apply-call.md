---
layout:     post
title:      "web前端开发之实现bind,call,apply"
subtitle:   "web前端开发之实现bind,call,apply"
date:       2019-09-02
author:     "90neoculture"
catalog:    true
categories: 
    - 前端
    - js
tags:
    - 前端
    - js
    - 原生js
---


### 1.实现call

call()方法调用一个函数，其具有一个指定的this值和分别地提供的参数（参数的列表）。
也就是说使用call方法，你可以指定被调用函数的this值，并且给他传参数。

```javascript
Function.prototype.myCall = function(context, ...parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }

  let fn = Symbol()
  context[fn] = this
  context[fn](...parameter);
  delete context[fn]
}
```

### 2.实现apply

apply()方法调用一个函数，其具有一个指定的this值，以及作为一个数组（或类数组对象）提供的参数。 注意：call()方法的作用和 apply() 方法类似，只有一个区别，就是 call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组。
apply和call方法的区别就在于，call是传参数列表，apply是传一个数组。

```javascript
Function.prototype.myApply = function(context, parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }

  let fn = Symbol()
  context[fn] = this
  context[fn](parameter);
  delete context[fn]
}
```

### 3.实现bind
bind（）方法创建一个新函数，在调用时，将其this关键字设置为提供的值，并在调用新函数时提供任何前面提供的给定参数序列。

```javascript
Function.prototype.myBind = function (context,...innerArgs) {
  var me = this
  return function (...finnalyArgs) {
    return me.call(context,...innerArgs,...finnalyArgs)
  }
}
```





