---
layout:     post
title:      "Function.prototype.bind实现"
subtitle:   "改变函数作用域内this 并返回一个新函数"
date:       2018-06-29 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

## .bind实现

```
    Function.prototype.rewriteBind = function() {
        var self = this;
        var context = [].shift.apply(arguments);
        var args = [].slice.apply(arguments);
        return function() {
            // 将传入的上下文context作为新函数的this 并组合两次分别传入的参数，作为新函数的参数
            return self.apply(context, [].concat.apply(args, [].slice.apply(arguments))); 
        }
    };

    var _this = {test: "test"};
    var test = function () {
        console.log(this) 
        console.log(arguments)
    };
    test.rewriteBind(_this,123,345)(234); // {test: "test"} { '0': 123, '1': 345, '2': 234 }
    test.rewriteBind('',123)(234); // [String: ''] { '0': 123, '1': 234 }
    test(123); // global { '0': 123 }

```