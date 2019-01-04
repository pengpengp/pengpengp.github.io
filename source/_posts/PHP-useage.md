---
title: PHP_useage
date: 2018-12-23 17:36:45
tags:
---
    *** php用法 ***
文件包含	include(‘文件名’)	require(‘文件名’)
	
* 用法1.包含头信息---每个页面头部都是一样的
	
* 用法2.包含账号密码的配置文件
	
* 用法3.包含远程文件
    include "http://www.baidu.com";

注意：远程文件任何后缀都可以打开
（图片木马的制作执行）

* 区别:include出错会继续执行，程序开始时候包含；require出错终止，在执行到require代码时才包含进来

* //伪协议常用  https://www.leavesongs.com/PENETRATION/php-filter-magic.html

* cookie
	setcookie(‘user’,'admin'，time()+3600)设置一个cookie
	$_COOKIE['user']获取一个cookie

* 如何放置cookie伪造？
	setcookie('id','',time()-1)清空COOKIE

* session----全局变量
    session_start()启动session功能

例子PHP用session做验证：
	session_start();

	$_SESSION['name']="za";
	
	验证
		if(isset($_SESSION['name'])){
    echo "欢迎";
    }
	session_destory（）	删除session创建的文件
	
	
	//header("location:a.php");跳转
** PHP中的文件上传：
    <!-- <form enctype="multipart/form-data" method="post" >
    	<input type="file" name="Filedata">
    	<input type="submit">
		</form> -->
	
	
	接收：$_FILES;

**  mysql **
* 往表中插入数据：
	insert into 表名称(字段1，字段2...) value(字段1的值，字段2的值...)

    例子：insert into news(title,content) value('标题','内容‘)；

* 查询数据：
	select 字段名1,字段名2,...,字段名n from 表名称
	
	select username,password from user where id =1;单条件
	
	select * from stu where number=31100 and name=hu;多条件用and连接
	
	select 字段1，字段2，字段n from 表名 limit 0,1；用limit加限制条件 从0开始读1条
	
	limit a,b  limit---限制读取记录   a---索引  b----记录数
	
* 更新：
	update 表名 set 字段1=新值1，字段2=新值2 条件；
	
	
* 删除表：
	delete from 表名 条件；一定要加好条件，否则都删了
	
	delete from 表名；清空一个表
	
* like子句：
	通配符：
		*表示任意的字符
		%表示任意的字符
		？表示任意一个字符
		select * from 表名  where name like '%sd';
* union***	联合查询
		select * from 表1 union select * from 表2；把表1和表2内容放在一起展示
		注意：表1和表2中字段个数要保持一致，否则会报错
		
* order by 条件***    根据条件排序
		select * from user where city ='beijng' order by name;
		ASC（升序） 或DESC（降序）默认升序
		order by 1\2\3.。。 根据第几列来排序，如果超过列数就会报错*****
		
* group by 根据一个或多个列对结果进行分组，常和count sum、AVG组合使用
		select name，count（*）from  emply by name；根据名字来给表分组；
		
* 删除字段：
		alter table 表名  drop 字段名；在表中将某个字段删除
		
* 增加字段：
		alter table 字段名 add 字段名 字段类型
		
* 改字段：
		alter table to modify 字段名 字段类型;
		
* 改表名：
		alter table 原表名 rename to  新表名;
		

* 导入数据：
		方法1.mysql -uroot -p 密码 < 要导入的数据（注意：.sql中要自动创建数据库，如果runoob.sql中不会自动创建数据库，需要用第二种方法）
		
		方法2.登录mysql，use数据库，source 路径文件
		
		方法3.mysqlimport -uroot -p --local database_name dump.txt dump.txt（注意：dump.txt不会创建数据库时，需要database_name）
		
* 导出数据：
		方法1.select * from 表名 into outfile 文件路径；
    
* 注释****注入
		#（%23） --  注释当前行
		/*  */      中间注释
		
* 查询用户连接数
		select connection_id();
		
* 替换字符		
	例子
		select insert('ichunqiu',1,1,'kk');结果是kkchunqiu
		
* 截取字符串
	例子
		select LEFT("helloworld",5);结果是hello
		select LEFT（被截取的字符串，左截取长度）;
		select RIGHT 同理
		
	截取
		select substring()/mid()/substr()都是三个参数，第一个：被截取的字符串，第二个：开始的位置，第三个：截取的长度

* 2个报错函数***  一般情况下要放在条件后面
		
		1.extractvalue(XML_document，XPath_string)；
		例子：
		select * from news where tid=1 and extractvalue(1,concat(0x7e,(select user()),0x7e));
		两个参数（1，拼接的第二个报错参数）
		
		2.UPDATEXML (XML_document, XPath_string, new_value); 
		updatexml（1，拼接参数，1）；
		
* 去重函数	
		select distinct title from news;不显示重复函数
		
* 把查询结果连接在一起
		group_concat(DISTINCT field) from table_name where conditions;

* PHP连接mysql数据库
		方法1：使用mysqli扩展连接(面向对象)
		方法2：使用mysql扩展（php低于5.5）
		
		方法3：使用PDO技术（面向对象的，防止sql注入）