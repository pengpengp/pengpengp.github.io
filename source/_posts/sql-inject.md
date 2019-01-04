---
title: '''sql_inject'''
date: 2018-12-28 20:05:18
tags: sql注入
---

> 流程：

> 1.前期沟通

> 2.信息搜集（四五天）

> 3.威胁建模：根据信息进行分析攻击点（一天）

> 4.渗透测试：根据分析进行攻击

> 5.后渗透测试：根据测试结果进行更多尝试

> 6.写报告

​	

	    www.exploit-db.com
	    https://www.somd5.com/
	    https://blog.csdn.net/u012278016/article/details/81772566

扫描工具：

* 测网站漏洞工具：	

  ​	AWVS（通过爬虫进行网站漏洞测试）的安装

  ​	网站漏洞扫描https://butian.360.cn/Register/补天公益

  ​	啊d-->ASP网站

  ​	sql注入工具
  		sqlmap

* 综合平台类：

  BurpSuite、Metasploit

* 搜集域名信息

  //子域名：news.baidu.com这种
  	子域名挖掘：subDomainsBrute、子域名挖掘机

* 端口扫描：NMAP---功能强大，隐蔽

  安装vc扩展、npcap组件，增加环境变量
  	扫描指定ip：	nmap ip
  	原理：只发送SYN，不建立连接
  	nmap -Pn  强制为激活的主机，进行强制扫描
  	nmap -sn  主机发现
  	nmap	-sn -oX 	Desktop/report.mxl报告输出到文件
  	nmap -sS	半开放扫描（默认方式）
  	nmap -p 80	指定扫描端口
  	nmap -O	ip	探测操作系统版本
  	nmap -A		详细信息
  	nmap -iL 目录 根据ip列表进行扫描
  	nmap -iL 目录 --webxml 文件名    把结果以xml形式>输出		到文件

* python环境安装

  1.安装python2.7
  	2.在家目录下创建.pip文件夹，把源文件移动进去
  	3.执行pip install requests

* 字典生成工具

  pentest.db工具
  	解压，在目录中用cmd执行pip install lxml
  	使用 python pen.py
  	帮助	python pen.py --help

* 爆破工具

  *BurpSuite
  	*hydra***   hydra -l用户名 -p密码字典 
  	-s指定非默认端口
  	-e ns空密码试探
  	-f成功后立刻停止
  	例子：hydra -l root -P 目录 -s 3308  -e ns -t 5 		114.115.175.102 mysql