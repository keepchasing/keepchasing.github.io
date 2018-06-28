---
layout:     post
title:      "async await、Promise.all、generator yield的应用"
subtitle:   ""
date:       2017-06-25 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

## async await 

> 主要用于第二个promise要用到第一个的返回值的情况，可以以同步的代码形式处理异步操作

```

async function fn1(){
    console.log(new Date().getTime()) // 1530105904919
    let a = await new Promise((resolve,reject) => {setTimeout(() => {
            resolve(2)
        }, 2000);
    })
    let b = await new Promise((resolve,reject) => {setTimeout(() => {
            resolve(a+2)
        }, 2000);
    })
    console.log(new Date().getTime()) // 1530105908934
    console.log(b)
}
fn1();

```

## Promise.all

> 主要用于可以同步进行的异步操作

```
console.log(new Date().getTime()) // 1530105853429
let a =  new Promise((resolve,reject) => {setTimeout(() => {
        resolve(2)
    }, 2000);
})
let b =  new Promise((resolve,reject) => {setTimeout(() => {
        resolve(2)
    }, 2000);
})
Promise.all([a,b]).then((data) => {
    console.log(new Date().getTime()) // 1530105855434
    console.log(data[0] + data[1])
})

```

## generator yield

> yield可以中断执行 下面的例子用于生成一个裴波那切数列

```
let [pre,cur] = [0,1]
function* gen(){
    for(;;)
    {
        // [pre,cur] = [cur,pre+cur]
        // yield cur;
        yield new Promise((resolve,reject) => {
            setTimeout(() => {
                [pre,cur] = [cur,pre+cur];
                resolve(cur);
            },1000)
        })
    }
}
let arr = [0,1];
let g = gen();
for(let i = 0; i < 9; i++)
{
    // arr.push(g.next().value);
    g.next().value.then((res) => {
        arr.push(res);
        console.log(arr);
    })
}
console.log(arr);

```



