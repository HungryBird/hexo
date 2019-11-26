---
title: hexo使用笔记二：menu通过i18n映射成中文
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
将theme变量内menu的key通过i18n映射成中文 

通过全局变量_的`__('Menu.' + foo)`方法映射成中文

具体代码：

    <% for(const key in theme.menu) { %>
        <%- __('Menu.' + key) %>
    <% } %>

hexo文档内没有特别详细的说明文档，待日后研究。