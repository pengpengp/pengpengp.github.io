---
title: 'http_request '
date: 2018-12-24 21:44:39
tags:
---
*** 一.http基础：
* URL：http://admin:123@www.baidu.com：80/new/index.php？id=1#
	*协议  + http基础认证  +域名 	+端口  +路径  +文件名  +参数  +锚部分

* URL编码****
        ‘’	--%27
        “”	--%22
        #	--%23
        空格	--%20
        %	--%25

* GET\POST请求结构

        GET请求
        GET  /HTTP基础/123.txt   /HTTP/1.1
        hOST:192.168.11.111:8000
        Accept：*/*
        换行

        POST请求
        POST /HTTP基础/123.txt   /HTTP/1.1
        hOST:192.168.11.111:8000
        Accept：*/*
        换行
        id=123&password=123

* 请求方法：
        GET
        HEAD  用于捕获报头
        PUT		iis put方法漏洞（自己研究）
        DELETE	请求删除
        CONNECT
        OPTIONS	允许客户端查看服务器支持的方法

* *状态码   302临时重定向（location）
        301永久跳转		百度看一下区别
        
        400
        403 禁止访问
        404	Not Found
        405  不允许
        
        5xx  服务器问题（代码）

* 练习：用wireshark抓http数据包

** 二.总结请求头：
* Host：表示服务器监听的端口号；

* User-Agent：请求所使用的浏览器

* Accept：可接受的响应类型 	例子：Accept: text/plain（当作文本不处理）     text/html （调用HTML解析器进行解析）

* Accept-language：可接受的相应语言清单 例子：
zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2

* Accept-Encoding：	可接受的响应的编码方式	例子：gzip, deflate

* Cache-Control：指定当前的请求/回复中，是否使用缓存

* Pragma：只用于客户端发送的请求中。客户端会要求所有的中间服务器不返回缓存的资源。
如果所有的中间服务器都以实现http/1.1为标准，那么直接使用Cache-Control:no-cache即可，如果不是的话，就要包含两个字段

* Connection：处理完这次请求后是否断开连接还是继续保持连接	例子：close

* Referer：客户机通过这个头告诉服务器，它是从哪个资源来访问服务器的（防盗链）

* Cookie：客户机通过这个头可以向服务器带数据


*****三.重点：  五层模型、tcp三次握手 、 四次挥手 、wireshark、http请求\响应的行、头、空行、内容 、burpSuite代理，看数据包	


