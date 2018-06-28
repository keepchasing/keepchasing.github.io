---
layout:     post
title:      "实现子元素高度与宽度相等，宽度相对于父元素等比缩放 且绝对居中于父元素的两种方式"
subtitle:   ""
date:       2017-06-25 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - css
---

## 方法一：通过padding属性实现


```
    <style>
        .box{width:40vw;height: 40vw;background-color: #f00;margin:2vw;float: left;}
        .sub-box{position:relative;left: 50%;top:50%;transform: translate(-50%,-50%);background-color: rgba(0,0,0,0.5);line-height: 20px;font-size: 16px;text-align: center;}
        .content-box{position: absolute; top:0;left:0;padding-top:20%;width: 100%;height: 80%;color:#fff;}
        .div1 .sub-box{width:50%;padding:25% 0;}
    </style>
    <div class="div1">
        <div class="box">
            <div class="sub-box">
                <div class="content-box">
                        我是一个通过padding属性实现高与宽相等且宽等于父元素50%的div，并通过transform绝对居中于父元素
                </div>
            </div>
        </div>
    </div>
```

## 方法二：通过vw长度单位实现

```

    <style>
        .box{width:40vw;height: 40vw;background-color: #f00;margin:2vw;float: left;}
        .sub-box{position:relative;left: 50%;top:50%;transform: translate(-50%,-50%);background-color: rgba(0,0,0,0.5);line-height: 20px;font-size: 16px;text-align: center;}
        .content-box{position: absolute; top:0;left:0;padding-top:20%;width: 100%;height: 80%;color:#fff;}
        .div2 .sub-box{width:20vw;height: 20vw;}
    </style>
    <div class="div2">
        <div class="box">
            <div class="sub-box">
                <div class="content-box">
                    我是一个通过单位vw实现高与宽相等且宽等于父元素50%的div，并通过transform绝对居中于父元素
                </div>
            </div>
        </div>
    </div>

```