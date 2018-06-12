---
layout:     post
title:      "javascript中this的指向问题"
subtitle:   "this指向及this指向变更"
date:       2018-04-05 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

### ES6中

>  箭头函数的 this 始终指向函数定义时的this，通过查找作用域链决定this指向，如果箭头函数被非箭头函数包含，则this绑定的是最近一层非箭头函数的this，否则为undefined


### ES5中

> this 永远指向最后调用它的那个对象

### this指向变更的方法

```
  _this = this //将this赋值给一个变量 后续操作使用_this

```


```
 var a ={
    c : 5,
    fn : function (a,b) {
        console.log( a + b + this.c)
    }
}
var b = a.fn;

// b(1,2) //NaN
// b.call(a,1,2) // 8
 b.apply(a,[1,2]) // 8

```


