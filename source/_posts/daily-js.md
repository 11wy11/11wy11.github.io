---
title: 日常知识点整理——js基础
date: 2019-06-13 11:43:50
tags: 
    - js
categories: 日常
---

正则表达式

<!--more-->

使用正则表达式 提取网址协议，域名，IP, 端口等参数

```
var url = "http://192.168.1.111:8888/#/statistic/htmel/dkdkd/dksdkldsl.html";
var patt = /(\w+):\/\/([^/:]+):(\d*)\/#\/(\S+)/;
arr = url.match(patt);
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i])
}
var index = arr[arr.length - 1];
// var arrIndex = index.split("/")
var arrIndex = index.match(/(\w+)/g);
for (let i = 0; i < arrIndex.length; i++) {
  console.log(arrIndex[i])
}
```

