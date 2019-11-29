---
title: hexo使用笔记一：自定义路由页面
date: 2019-11-26 16:17:03
tags:
- hexo
- hexo router
- hexo theme
categories:
- blog
- 博客
- note
---
<!--excerpt-->
hexo默认的路由只有'/'和'/archives'，但是我想添加一个about路由该怎么办呢？
于是利用搜索引擎找到了添加路由的方法。
<!--more-->
首先在命令行输入hexo n page "about"指令。

成功之后可以在根目录的source下发现多了一个about文件夹，打开之后是index.md这个文件。
于是我在导航栏新增加了/about这个路径之后发现浏览器报错。

`each is not a function`

原来是我在index.ejs里用page.post.each方法渲染文章列表。

跳转到about路径之后只有一个独立的文章变量。

因此添加了if(page.posts && page.posts.length)判断语句解决了不同路由引发的报错。