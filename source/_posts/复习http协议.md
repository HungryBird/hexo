---
title: 复习http协议
date: 2019-12-02 22:59:31
tags: http
categories: 网络
---
<!--excerpt-->
**目录**

* 什么是http协议
* http协议的组成部分
* http协议的特点
* http和https的区别
<!--more-->
>什么是HTTP协议？

HTTP协议全称Hyper Text Transfer Protocol，翻译过来就是超文本传输协议，位于TCP/IP四层模型当中的应用层。

http协议主要应用于客户端和服务端进行通信。

>http协议的组成部分。

前端发出http请求，http请求报文分为三部分：

1. 请求行

   1.1 请求方法

   1.2 请求路径

   1.3 请求协议及版本号

2. 请求头

    2.1 Content-Length: 请求主体长度。

        2.1.1 Content-Length > 实际主体长度：服务端读取到消息结尾后, 会等待下一个字节, 无响应直到超时。
        2.1.2 Content-Length < 实际主体长度：首次请求主体内容会被截取，再次请求会抛出异常。
    2.2 Transfer-Encoding: chunked： 当Content-Length长度不确定时使用该键值对，Content-Length会被忽略。

    2.3 Content-type: 将数据回发到服务器时的编码类型

        2.3.1 application/x-www-form-urlencoded：当用get方法时，数据用？分割，键值对用&连接。
        当用post方法时，浏览器把form数据封装到http body中。
        2.3.2 multipart/form-data：当表单使用type=file控件时用这个值代替2.3.1。

    （注意：请求头结束之后要和请求主体空一行）

3. 请求主体

服务端返回的响应报文同样分为三个部分：
1. 响应行

   1.1 响应协议

   1.2 响应状态码

   1.3 状态描述

2. 响应头
3. 响应主体