---
title: Create_VPN
date: 2018-12-26 21:24:00
tags:
---
***创建VPN连接***

一.安装浏览器插件
	hackbar、Header Edit、wappalzer、 proxy、server ip

二.在windows 2008上搭建vpn

搭建PPTP连接

>1.打开服务管理器--->添加角色---->勾选“网络策略和访问服务 ”------>下一步----->勾选"路由和远程访问服务"--->开始安装

> 2.角色中出现了“路由和远程访问”，现在是红色的，右键选择配置它，打开向导--->选择自定义配置-->服务里全选-->完成-->变成绿色

> 3.新增一个接口：ipv4-->NAT--->新建一个接口-->选择要使用的网卡--->接口类型选择“公用接口连接到Internet”,勾选“在此接口上启用NAT”

> 4.开始菜单-->管理工具-->网络策略服务器-->策略-->网络策略-->把里面的两项被组织的属性改成“授予访问权限”

> 5.服务器管理器-->配置-->本地用户和组-->添加一个用户-->填写用户名、密码、勾选“用户不能更改密码”和“密码永不过期”，去掉“下次登陆须更改密码”的勾，点创建。

> 6.开始菜单-->管理工具-->本地安全策略-->本地策略-->用户权限分配-->拒绝本地登陆，添加vpn用户--->拒绝通过远程桌面登陆,添加vpn用户。

> 7.连接VPN：在客户机创建一个新连接-->选择连接到工作区--->使用我的internet连接-->填写ip地址-->填写之前创建的VPN用户名和密码-->连接即可
	
三.docker：
    

> 安装docker：sudo apt-get install docker.io


> 安装加速器（可选）https://yeasy.gitbooks.io/docker_practice/install/mirror.html
    
> 或者在 /etc/docker/daemon.json 中写入
    {
        "registry-mirrors": ["https://registry.docker-cn.com"]
    }



>启动docker：sudo docker run --rm -it alpine /bin/sh



>在docker中启动ubuntu：sudo docker run --rm -it ubuntu /bin/sh

>在docker中启动centOS：sudo docker run --rm -it centos /bin/sh



四.VPN :PPTP   L2TP 

第一种连接方法：

>1.把镜像拉入虚拟机：

>2.docker pull mobtitude/vpn-pptp
然后创建一个文件chap-secrets，打开写入   name *  password * 并记住路径/vpn-k

>3.docker run -d --privileged --net host -v /root/chap-secrets:/ppp/chap-secrets mobtitude/vpn-pptp


第二种连接方法：
>1.docker pull hwdsl2/ipsec-vpn-server

>2.modprobe af_key

>3.VPN_IPSEC_PSK=ipsec-keydoc
VPN_USER=uname
VPN_PASSWORD=upass

>4.docker run --name vpn-docker --privileged --env-file /root/vpn.env -p 500:500/udp -p 4500:4500/udp -v /lib/modules:/lib/modules:ro  -d --privileged hwdsl2/ipsec-vpn-server


第三种方法：使用shadowsocks工具代理连接VPN
    
> 1.apt install shadowsocks先安装

> 2.修改配置文件  vi /etc/shadowsocks/config.json

    "server":"0.0.0.0",
    "server_port":8888,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"123456",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false,
    "workers": 1,
    "prefer_ipv6": false

> 3.（可选）开启BBR加速支持echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
lsmod | grep bbr
