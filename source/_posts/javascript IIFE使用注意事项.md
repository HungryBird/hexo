---
layout: 'page:title'
title: javascript IIFE使用注意事项
date: 2019-11-24 02:11:37
tags:
- javascript
- IIFE
- js
categories:
- web前端
- javascript
---
<!--excerpt-->
IIFE（ 立即调用函数表达式）是一个在定义时就会立即执行的  JavaScript 函数。

实现IIFE有多种方法，但是需要获得IIFE的返回值时，每一种实现方法返回的值可能都会不一样。
<!--more-->
>已知IIFE的8种实现方式 

1. `(function(){}())` 
2. `(function(){})()`
3. `!function(){}()`
4. `[function(){}()]`
5. `+function(){}()`
6. `-function(){}()`
7. `void function(){}()`
8. `~function(){}()`
   
>！注意事项
* 返回值变更
1. 转换成boolean值后取反
2. 转成数组，数组元素为返回值本身
3. 返回值被转换成数字类型
4. 同5但是数字类型取反
5. 始终返回undefined
6. 返回值先是被转换为数字类型,当值为NaN时，返回-1。不为NaN时值取反并-1。