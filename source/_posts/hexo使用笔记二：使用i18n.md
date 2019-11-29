---
title: hexo使用笔记二：使用i18n
date: 2019-11-27 00:11:42
tags:
- hexo
- hexo router
- hexo theme
- lodash
categories:
- blog
- 博客
- note
---
<!--excerpt-->
之前在做别的项目一直没有机会使用i18n，趁着自己用hexo开发一个博客这次一定要用上i18n。
<!--more-->
我在languages文件夹下添加了zh-CN.yml，将自定义主题下的_config.yml的menu对象里的key都映射成了中文。

````
Menu:
  Home: 首页
  Archives: 归档
  About: 关于
  Contact: 联系
````

我将根目录的_config.yml的languages设为zh-CN。

在导航标签内使用了如下代码：
```
<% for(const key in theme.menu) { %>
    <%- __('Menu.' + key) %>
<% } %>
```
__()方法会从zh-CH.yml找到传入的key的值并返回value。
>！注意：根目录下的_config.yml如果设一个默认值将会引用theme目录下languages文件夹里的default.yml文件。