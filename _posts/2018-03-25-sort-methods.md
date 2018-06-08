---
layout:     post
title:      "array sort methods"
subtitle:   " \"~~~~~\""
date:       2018-05-28 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

### 冒泡排序

```
let arr = [10, 4, 6, 19, 35, 43, 2]
function sortFn (arr) {
  if (arr.length <= 1) {
    return arr
  }
  let leftArr = []
  let rightArr = []
  let len = arr.length
  let conEl = arr.splice(Math.floor(len / 2), 1)
  for (let val of arr) {
    if (val <= conEl) {
      leftArr.push(val)
    } else {
      rightArr.push(val)
    }
  }
  return sortFn(leftArr).concat(conEl, sortFn(rightArr))
}
console.log(sortFn(arr))

```

### 快速排序

```
let arr = [10, 4, 6, 19, 35, 43, 2]
function sortFn (arr) {
  let len = arr.length
  for (let i = 0; i < len; i++) {
    for (let j = 0; j < len - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
      }
    }
  }
  return arr
}
console.log(sortFn(arr))

```



