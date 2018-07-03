---
layout:     post
title:      "js中的节流和防抖"
subtitle:   "throttle and debounce"
date:       2018-07-02 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

## 节流

>   无论触发多少次，都是每隔delay时间执行一次函数调用

    原理：事件触发时，检查定时器timer是否存在，如果不存在设置一个定时器timer，
    delay时间后执行函数调用，并在执行操作后清除定时器，
    如果定时器存在，则不执行函数调用

```
var throttle = function(fn,delay){
    var timer = null;
    return funtion(){
        var context = this;
        var args = arguments;
        if(!timer){
            timer = setTimeout(function(){
                fn.apply(context,args);
                timer = null;
            },delay);
        }
    }
}

```


## 防抖

>   时间间隔小于delay的多次触发函数调用，只在最后一次触发的delay时间后调用并执行函数

    原理：每一次时间间隔小于delay的事件被触发，都会清除当前的 timer 然后重新设置超时调用。 
    这就会导致每一次高频事件都会取消前一次的超时调用，导致事件处理程序不能被触发，
    只有当高频事件停止，最后一次事件触发的超时调用才能在delay时间后执行

```
let debounce = function(fn, delay) {
    let timer = null;
    return function() {
        let context = this;
        let args = arguments;
        clearTimeout(timer);
        timer = setTimeout(function() {
        fn.apply(context, args);
        }, delay);
    }
}

```