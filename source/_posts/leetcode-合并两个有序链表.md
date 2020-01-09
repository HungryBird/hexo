---
title: 'leetcode:合并两个有序链表'
date: 2020-01-09 23:36:37
tags:
- leetcode
- ListNode
categories:
- javascript
- 数据结构
---

合并两个有序列表：
难度：easy

>实例
````
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
````
测试用例：
````
[1,2,4]
[1,3,4]
````
看到测试用例我是很懵逼的，正确的数据结构应该是这样
````
{
    val: 1,
    next: {
        val: 2,
        next: {
            val: 4,
            next: null
        }
    }
}
{
    val: 1,
    next: {
        val: 3,
        next: {
            val: 4,
            next: null
        }
    }
}
````
解题过程及思路
````javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    // 当其中一个链表的next为空时，直接返回另一个有序链表
    if(l1===null) return l2;
    if(l2===null) return l1;
    
    if(l1.val<=l2.val){
        // 返回比较后的链表
        l1.next=mergeTwoLists(l1.next,l2);
        return l1;
    }else{
        l2.next=mergeTwoLists(l1,l2.next);
        return l2;
    }
};
````