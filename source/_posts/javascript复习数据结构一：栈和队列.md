---
title: javascript复习数据结构一：栈和队列
date: 2019-12-10 10:10:42
tags:
- data structure
- stack
- queue
categories: 
- javascript
---

<!--excerpt-->
js没有栈和队列数据结构，用Array可以很轻松的模拟出来。
在动手实现的情况下还能复习数据结构。
<!--more-->
>栈：栈就是一个薯片盒，每次拿薯片时只能从最上面的一块拿起。往里放薯片时最先放进去的只能最后拿出来。
>栈待添加元素和待删除元素都在栈顶，另一端则是栈底。

实现这个数据结构时将提供以下几种方法：

|方法   |解释   |
|--|--|
|push(item) |进栈   |
|pop()  |出栈   |
|isEmpty() |判空   |
|isMax() |判满   |
|peek() |返回栈顶   |
|clear() |清除栈   |
|getSize() |获得栈的长度   |
|print() |打印栈的元素   |

**创建栈**

````javascript
function Stack(max) {
    // js内数组的最大长度为Math.pow(2, 32) - 1
    var max = max || Math.pow(2, 32) - 1;
    var items = []; // 保存栈
    this.push = function(item) {
        if (items.length >= max) throw new RangeError('栈已满');
        items.push(item)
    };
    this.pop = function() {
        if (items.length === 0) throw new RangeError('栈为空');
        items.pop();
    };
    this.isEmpty = function isEmpty() {
        return items.length === 0;
    };
    this.isMax = function isMax() {
        return items.length === max;
    };
    this.peek = function peek() {
        return items[items.length - 1];
    };
    this.clear = function clear() {
        items = []
    };
    this.getSize = function getSize() {
        return items.length;
    };
    this.print = function print() {
        console.log(items.toString())
    };
}
````

>队列: 队列就是一条管道，先进先出，后进后出。添加的元素都在队列尾部，要移除的元素都在队列顶部。

实现这个数据结构时将提供以下几种方法：

|方法   |解释   |
|--|--|
|enqueue(item) |队列尾部添加一个或多个元素   |
|dequeue()  |队列头部删除一个元素，并返回被删除的元素   |
|isEmpty() |判空   |
|isMax() |判满   |
|font() |返回队列顶部   |
|getSize() |获得队列的长度   |
|print() |打印队列的元素   |

**创建队列**

````javascript
function Queue(max) {
    var items = [];
    var max = max || Math.pow(2, 32) - 1;
    this.enqueue = function() {
        var arr = Array.prototype.slice.call(arguments);
        arr.forEach(item => {
            items.push(item);
        })
    };
    this.dequeue = function() {
        if (items.length === 0) throw new RangeError('队列为空');
        return items.shift();
    };
    this.isEmpty = function() {
        return items.length === 0;
    };
    this.isMax = function() {
        return items.length === max;
    };
    this.font = function() {
        return items[0]
    };
    this.getSize = function() {
        return items.length;
    };
    this.print = function() {
        console.log(items.toString())
    }
}
````