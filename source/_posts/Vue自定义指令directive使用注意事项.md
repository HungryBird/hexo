---
title: Vue自定义指令directive使用注意事项
date: 2019-11-27 12:16:58
tags:
- Vue
- directive
categories:
- web前端
- Vue
- javascript
---
<!--excerpt-->
当我们需要对原生标签添加底层操作的方法，或是不方便修改其他人封装的组建时，自定义指令给我们更大的开发自由度。

但是使用自定义指令时有几个要特别注意的地方。
<!--more-->

>注意事项1：

directive命名时不支持驼峰法，用驼峰法命名的directive无效。
>注意事项2：

input标签监听change事件应该用'input'代替'change'

具体代码：
```obj
<template>
    <input v-only-number>
</template>
<script>
    Vue.directive('only-number', {
        inserted: function(el) {
            el.addEventListener('input', function() {
                // todo
            })
        }
    })
</script>
```
>注意事项3：
自定义指令内无法直接获得vue实例，需要通过binding.value传递this。

具体代码：
```
<template>
    <input v-only-number="{set: this, name: 'bar'}" v-model="bar">
</template>
<script>
    export default: {
        data() {
            return {
                bar: '',
            }
        },
        directives('only-number', {
            inserted: function(el, binding) {
                el.addEventListener('input', function() {
                    const self = binding.value.set;
                    const name = binding.value.name;
                    self[name] = el.value;
                })
            }
        })
    }
</script>
```