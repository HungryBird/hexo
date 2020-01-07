---
title: 模拟实现call和apply
date: 2020-01-07 16:29:13
tags:
- call
- apply
categories:
- javascript
---

<!--excerpt-->

call和apply都是经常使用的方法。

为了加深自己的理解，用js代码实现call和apply方法。

<!--more-->

call和apply唯一的不同就是传参类型不同，call传参的是一个参数列表。apply则要求是一个数组对象。

这里实现call之前先看看call是怎么用的。

<pre>
var name = 'win'
var obj = {name: 'obj'}
function foo(arg1, arg2) {
    console.log(arg1)
    console.log(arg2)
    console.log(this.name)
}
foo()   // 'win'
foo.call(obj, '1', '2')   // 1 2 'obj'
</pre>

>call() 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。

call的特点，改变调用函数this指向，立即执行。

要实现让this指向obj这个对象最简单的方法就是把foo变成obj的属性，即：
<pre>
var obj = {
    name: 'obj',
    foo(arg1, arg2) {
        console.log(arg1)
        console.log(arg2)
        console.log(this.name)
    }
}
obj.foo(1,2)   // 1 2 'obj'
</pre>

1. 先给对象添加属性，调用之后删除该属性
<pre>
Function.prototype.call1 = function(context) {
    // 为了避免覆盖context上已存在的属性，用Symbol作为属性名
    const fn = Symbol('fn');
    // foo.call() this === foo
    context[fn] = this;
    // 相当于执行obj.foo()
    context[fn]();
    delete context[fn]
}

foo.call1(obj)  // 'obj'
</pre>
2. 将参数传入foo内

<pre>
Function.prototype.call1 = function() {
    // 第一个参数是传入的对象
    const context = arguments[0];
    const arr = [];
    for(let i = 1; i < arr.length; i++) {
        arr.push(arguments[i]);
    }

    const fn = Symbol('fn');
    context[fn] = this;
    /** eval(string)
    * string为必须
    */
    eval(`context[fn](${arr})`);
    delete context[fn]
}
foo.call1(obj, 1, 2)  // 1 2 'obj'
</pre>

3. 当function有返回值时
<pre>
function foo() {
    return {
        name: this.name
    };
}
var f = foo.call(obj);
console.log(f)  // {name: 'obj'}
</pre>
因此需要给一个返回值
<pre>

</pre>
