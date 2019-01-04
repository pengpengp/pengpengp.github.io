---
title: linux exam
date: 2018-12-08 13:40:43
tags:
---
Linux基础知识试卷

一、选择题
1. 下面哪个Linux命令可以一次显示一页内容？(C)
A. pause暂停
B. cat   读取文件内容
C. more  分页显示
D. grep   查找字符
2. 统计当前目录(或文件)所占磁盘空间的大小命令是：(B)
A. df /    查看指定分区大小
B. du /    查看根目录文件大小
C. du     查看当前目录大小
D. df     查看所有分区大小
5. 怎样更改一个文件的权限设置？(B)
A. attrib     
B. chmod    改权限
C. change    
D. file
6. 假如您需要找出 /etc/my.conf 文件属于哪个包 (package) ，您可以执行： 
A. rpm -q /etc/my.conf      查询软件包 +软件包名称
B. rpm -requires /etc/my.conf  
C. rpm -qf /etc/my.conf查看某个文件属于哪个软件包，可以是普通文件或可执行文件，跟文件的绝对路径
D. rpm -q | grep /etc/my.conf  查询是否安装了某个软件
13.在使用了shadow口令的系统中，/etc/passwd和/etc/shadow两个文件的权限正确的是：（C）
A. -rw-r----- , -r--------
B. -rw-r--r-- , -r--r--r--
C. -rw-r--r-- , -r--------
D. -rw-r--rw- , -r-----r--
14．下面哪个参数可以删除一个用户并同时删除用户的主目录？(C)
A. rmuser -r
B. deluser –r       deluser   --remove-home
C. userdel -r
D. usermgr -r
17．如果你的umask设置为022，缺省的你创建的文件的权限为：(D)
A. ----w--w-
B. -w--w----
C. r-xr-x---
D. rw-r--r—
root的缺省unmask是022，一般用户是002。
例如：unmask为022的用户创建了一个新文件，那么新文件的权限644，而目录则为755。如果用户的umask为000，则创建的文件权限为666，目录权限为777，
运行umask命令可以查看用户自己的umask值。
18．在一条命令中如何查找一个二进制命令 Xconfigurator 的路径？(D)
A. apropos Xconfigurator    用来通过关键字查找定位手册页的名字和描述。
B. find Xconfigurator         查文件
C. where Xconfigurator       whereis
D. which Xconfigurator
20．运行一个脚本，用户不需要什么样的权限？（B）
A. read                   
B. write
C. execute
D. browse on the directory
23．在 bash 中, 在一条命令后加入"1>&2" 意味着：（B）0—标准输入、1---标准输出、2---标准错误输出
A. 标准错误输出重定向到标准输入
B. 标准输入重定向到标准错误输出
C. 标准输出重定向到标准错误输出
D. 标准输出重定向到标准输入
24．下面哪条命令可以把f1.txt复制为f2.txt?（C）
A. cp f1.txt | f2.txt          
B. cat f1.txt | f2.txt
C. cat f1.txt > f2.txt
D. copy f1.txt | f2.txt
25．显示一个文件最后几行的命令是： （B）
A. tac
B. tail
C. rear
D. last
31.使用ln命令将生成了一个指向文件old的符号链接new，如果你将文件old删除，是否还能够访问文件中的数据？       （A）
A. 不可能再访问
B. 仍然可以访问
C. 能否访问取决于文件的所有者
D. 能否访问取决于文件的权限
37.如何在文件中查找显示所有以"*"打头的行？
A. find \* file   *没有效果
B. wc -l * < file    wc –l数一下文件内容行数
C. grep -n * file      
D. grep ‘^\*’ file   grep -n '^[a-z]'以a-z开头 grep '\a$'以a结尾
. (小数点)：代表『一定有一个任意字节』的意思；grep -n 'g..d'
* (星号)：代表『重复前一个字符， 0 到无穷多次』的意思，为组合形态
grep -n 'g.*g'搜索g开头g结尾的行
\表示匹配字符
38.在ps命令中什么参数是用来显示所有用户的进程的？（A）
A. a                  所有用户
B. b
C. u              某个用户 –u root
D. x               与a搭配，显示完整进程
40.如何显示Linux系统中注册的用户数（包含系统用户）？（D）
A. account -l
B. nl /etc/passwd |head             显示头十行
C. wc --users /etc/passwd  
D. wc --lines /etc/passwd        显示用户数
42.命令 kill 9 的含义是：           (A)
A. kills the process whose PID is 9.
B. kills all processes belonging to UID 9.
C. sends SIGKILL to the process whose PID is 9.
D. sends SIGTERM to the process whose PID IS 9.
43.如何删除一个非空子目录/tmp？（D）
A. del /tmp/*        
B. rm -rf /tmp         删除tmp目录
C. rm -Ra /tmp/*       R与r相同 a未知
D. rm -rf /tmp/*       删除tmp目录内容
48.在Linux系统中的脚本文件一般以什么开头？（B）
A. $/bin/sh
B. #!/bin/sh
C. use /bin/sh
D. set shell=/bin/sh
49.下面哪种写法表示如果cmd1成功执行，则执行cmd2命令？（A）
A. cmd1&&cmd2
B. cmd1|cmd2        把cmd1结果导入cmd2执行
C. cmd1;cmd2
D. cmd1||cmd2
51.Linux中，提供TCP/IP包过滤功能的软件叫什么？（C）
A. rarp
B. route     路由
C. iptables   防火墙
D. filter
53.在vi中退出不保存的命令是？（A）
A. :q           退出
B. :w         保存
C. :wq         保存退出
D. :q!         强退
55.使用什么命令检测基本网络连接？（A）
A. ping           
B. route
C. netstat         连接状态
D. ifconfig        网卡信息
56.下面哪个协议使用了二个以上的端口？（B）
A. telnet           23
B. FTP         20、21
C. ssh             22
D. HTTP           80
59.如何在Debian系统中安装rpm包？(D)alien是包转换工具
A. alien pkgname.rpm     alien –I    .rpm
B. dpkg --rpm pkgname.rpm     dpkg –I   .rpm
C. dpkg --alien pkgname.rpm     
D. alien pkganme.rpm ; dpkg -i pkganme.deb  
　
60.在安装软件时下面哪一步需要root权限？(D)
A. make
B. make deps
C. make config
D. make install          install需要
61.什么命令用来只更新已经安装过的rpm软件包？（B）
A. rpm -U *.rpm     强行安装
B. rpm -F *.rpm     只更新
C. rpm -e *.rpm      卸载
D. rpm -q *.rpm      查询包
64.下面哪个命令可以压缩部分文件：（C）
A. tar -dzvf filename.tgz *    特殊文件
B. tar -tzvf filename.tgz *   查询包内容
C. tar -czvf filename.tgz *     打包压缩
D. tar -xzvf filename.tgz *     解压缩
67.对于Apache服务器，提供的子进程的缺省的用户是：（D）
A. root
B. apached
C. httpd
D. nobody
69.apache的主配置文件是：（A）
A. httpd.conf
B. httpd.cfg
C. access.cfg
D. apache.conf
77.通过Makefile来安装已编译过的代码的命令是：（D）
A. make          编译
B. install
C. make depend
D. make install	安装
Configure检测安装平台是否具备所需条件
78.什么命令解压缩tar文件？（B）
A. tar -czvf filename.tgz
B. tar -xzvf filename.tgz
C. tar -tzvf filename.tgz
D. tar -dzvf filename.tgz
84.命令 netstat -a 停了很长时间没有响应，这可能是哪里的问题？（B）
A. NFS.
B. DNS.  
C. NIS.
D. routing.
85.ping使用的协议是：（D）
A. TCP
B. UDP
C. SMB
D. ICMP
86.下面哪个命令不是用来查看网络故障的？（B）
A. ping 
B. init
C. telnet 
D. netstat
87.拨号上网使用的协议通常是：（A）
A. PPP 网络安全系统认证（Authentication）、授权（Authorization）和计费（Accounting）
B. UUCP  文件传输协议
C. SLIP  Serial Line Internet Protocol，串行线路网际协议 拨号
D. Ethernet
88.TCP/IP中，哪个协议是用来进行IP自动分配的？（C）
A. ARP       局域网通信
B. NFS   Network File System）即网络文件系统---freeBSD
C. DHCP
D. DNS     域名解析
90.下面哪个功能用来生成一个文件的校验码？(A)？D
A. md5          密文
B. tar        
C. crypt        crypt 库
D. md5sum    md5sum aaa.txt > checksum/aaa.md5  生成校验文件
93.如何停止一台机器的telnet服务？（A）
A. Put NONE in /etc/telnet.allow  白名单 sshd:192.168.220.1    in.telnetd:192.168.220.1
B. Put a line 'ALL:ALL' in /etc/hosts.deny     黑名单
C. Comment the telnet entry in /etc/inittab     配置启动模式
D. Comment the telnet entry in /etc/xinetd.conf      用来管理多种轻量级Internet服务  xinetd.conf代替原来的inetd.conf

二、操作题：
1.假设你是系统管理员，需要增加一个新的用户账号zheng，为新用户设置初始密码，锁定用户账号uly，并删除用户账号chang。 
答：	
Useradd zheng 
Password zheng
usermod -s /sbin/nologin wangshibo    
 userdel chang


2.若给需要将/home/zheng目录下的所有文件打包压缩成/tmp/zheng.tar.gz，你准备怎么做？当需要从压缩包中恢复时，又该如何处理？
答：
Tar  –zcvf     /tmp/zheng.tar.gz  /home/zheng/*  
Tar –zxvf   zheng.tar.gz
3.介绍什么是桥接，什么是nat？
答：
桥接是把虚拟机模拟成同网中的一台设备
Nat 是路由模式，把虚拟机模拟成另一个网段的设备并路由到本网段
[完整试题及答案1](https://baijiahao.baidu.com/s?id=1600811597383089586&wfr=spider&for=pc)


[完整试题及答案2](https://blog.csdn.net/hermito/article/details/51018243)
