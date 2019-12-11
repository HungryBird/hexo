---
title: javascript复习数据结构二：链表
date: 2019-12-10 15:02:59
tags:
- data structure
- linked list
categories:
- javascript
---
<!--excerpt-->
已知队列和栈的出口都是单向的，如果要移除中间元素就要移除一半的元素。
因此链表的出现让存储有序数据变得更加灵活。
<!--more-->
>单向链表的结构示意图

<kbd>head</kbd> => <kbd>data|next</kbd> => <kbd>data|next</kbd> => null

链表包括头部元素head和链表元素node。

头部元素永远指向第一个有效的链表元素，不是必须存在的元素。
链表元素包括data存储数据部分和next指向下一个链表元素的指针。最后一个链表元素的指针指向null。

实现这个数据结构时将提供以下几种方法：

|方法   |解释   |
|--|--|
|append(data) |链表尾部添加一个新元素   |
|insert(index, data) |链表插入指定位置插入新元素    |
|remove(data)   |从链表中移除指定元素   |
|removeAt(index)    |根据索引值移除元素 |
|indexOf(data)  |返回传参元素所在索引值不存在返回-1    |
|isEmpty()  |判断链表是否为空   |
|getSize()  |返回链表的长度 |
|print()    |打印链表的元素 |

**创建链表**

````javascript
function LinkedList() {
    // 初始化头部指针
    var head = null;
    // 链表长度默认值为0
    var length = 0;
    // 声明Node类
    function Node(data) {
        this.data = data;
        this.next = null;
    }
    this.append = function(data) {
        var node = new Node(data)
        , current;
        if(!head) {
            head = node;
        }
        else {
            // 找到第一个node
            current = head;
            // 找到最后一个node
            while(current.next) {
                current = current.next;
            }
            // 最后一个node的next指向新添加的node
            current.next = node;
        }
        // 更新链表长度
        length++;
    };
    this.insert = function(index, data) {
        // 检查是否越界
        if (index < 0 || index > length) {
            throw new RangeError('插入位置错误')
        }
        var node = new Node(data)
        , current = head    // 从第一个元素开始
        , previous
        , _index = 0;
        if (!head) {
            head = node;
        }
        else if(index === 0){
            node.next = head;
            head = node;
        }
        else {
            while(_index !== index) {
                previous = current;
                current = current.next;
                _index++;
            }
            previous.next = node;
            node.next = current;
        }
        length++;
    };
    this.removeAt = function(index) {
        if (index > length - 1 || index <= -1) return null;
        var current = head
        , previous
        , _index;
        if (index === 0) {
            head = current.next;
        }
        else {
            while(_index < index) {
                previous = current;
                current = current.next;
                _index++;
            }
            previous.next = current.next;
        }
        length--;
        return current.data;
    };
    this.indexOf = function(data) {
        if (!head) return -1;
        var current = head
        , _index = 0;
        while(current && current.data !== data) {
            current = current.next;
            _index++;
        }
        return current ? _index : -1;
    };
    this.remove = function(data) {
        var _index = this.indexOf(data);
        return this.removeAt(_index);
    };
    this.isEmpty = function () {
        return !head;
    };
    this.getSize = function() {
        var _index = 0
        , current = head;
        if (!head) return _index;
        while(current) {
            current.next = current;
            _index++;
        }
        return _index;
    };
    this.print = function() {
        console.log(JSON.stringify(head));
    };
}
````

>双向链表：比单向链表的node多了一个previous指向前一个node

>循环单向链表：单向链表最后一个node的next指向head

>循环双向链表：双向链表最后一个node的next指向head