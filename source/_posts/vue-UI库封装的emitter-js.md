---
title: vue UI库封装的emitter.js文件
date: 2019-12-14 16:37:46
tags:
- emitter
- bug
categories:
- Vue
---
<!--excerpt-->
element-ui和iview等流行的Vue的UI库都有一个叫做emitter.js的文件。

emitter文件里有两个方法：

dispatch是寻找组件名为componentName的父级组件并执行eventName方法。

broacast是寻找组件名为componentName的子组件并执行eventName方法。

<!--more-->

源码如下(element-ui2.13.0):

````javascript
function broadcast(componentName, eventName, params) {
    this.$children.forEach(child => {
        var name = child.$options.componentName;

        if (name === componentName) {
            child.$emit.apply(child, [eventName].concat(params));
        } else {
            broadcast.apply(child, [componentName, eventName].concat([params]));
        }
    });
}
export default {
    methods: {
        dispatch(componentName, eventName, params) {
            var parent = this.$parent || this.$root;
            var name = parent.$options.componentName;

            while (parent && (!name || name !== componentName)) {
                parent = parent.$parent;

                if (parent) {
                    name = parent.$options.componentName;
                }
            }
            if (parent) {
                parent.$emit.apply(parent, [eventName].concat(params));
            }
        },
        broadcast(componentName, eventName, params) {
            broadcast.call(this, componentName, eventName, params);
        }
    }
};
````

当我直接复制粘贴改源码使用时，发现根本找不到要找的组件。

经过排查
````javascript
parent.$options.componentName   // 永远返回undefined
````
Vue获取组件名的方法
````javascript
this.$options.name
````
将
````javascript
parent.$options.componentName
````
改为
````javascript
parent.$options.name
````
便可正确获得组件




