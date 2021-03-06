---
title: linux 常见问题总结
tags:
  - linux
  - 问题总结
categories:
  - - 操作系统
    - Linux
comments: true
abbrlink: 3467120238
date: 2021-11-02 00:00:00
---

## linux 配置静态 IP

1. 安装 ifconfig

```shell
	yum search ifconfig  => ifconfig 在 net-tools.x86_64 包中

	sudo yum install net-tools.x86_64
```
2. 查看 IP 信息
```shell
	ifconfig / ip addr  # 查看IP 和子网掩码
        enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.1.222  netmask 255.255.255.0  broadcast 192.168.1.255
            inet6 fe80::c597:178c:e00f:9029  prefixlen 64  scopeid 0x20<link>
            ether 08:00:27:50:18:58  txqueuelen 1000  (Ethernet)
            RX packets 4306  bytes 313127 (305.7 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 1243  bytes 225826 (220.5 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	route -n # 查看网关 GATEWAY
		[root@localhost etc]# route -n
        Kernel IP routing table
        Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
        0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 enp0s3
        172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
        192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 enp0s3

```

3. 修改配置文件

```shell
	vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
	
	TYPE="Ethernet"
    PROXY_METHOD="none"
    BROWSER_ONLY="no"
    DEFROUTE="yes"
    IPV4_FAILURE_FATAL="no"
    IPV6INIT="yes"
    IPV6_AUTOCONF="yes"
    IPV6_DEFROUTE="yes"
    IPV6_FAILURE_FATAL="no"
    IPV6_ADDR_GEN_MODE="stable-privacy"
    NAME="enp0s3"
    UUID="65348731-3dab-47ae-a462-49eb2d7e7035"
    DEVICE="enp0s3"
    ONBOOT="yes"
    #####静态IP改动部分开始#####
    # 动态 IP
    # BOOTPROTO="dhcp"
    # 静态 IP
    BOOTPROTO="static"
    IPADDR=192.168.1.222
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1
    DNS1=114.114.114.114
```

4. 添加 DNS 服务(首选DNS服务器和备选DNS服务器)

```shell
    vi /etc/resolv.conf

    # Generated by NetworkManager
    search localdomain
    nameserver 114.114.114.114
    nameserver 114.114.114.115                             
```

5. 重启网络服务

```
	service network restart

	systemctl network restart
```

## Deepin 配置 SSH 远程

1. 安装ssh服务

```SHELL
    sudo su
    apt-get install openssh-server
```

2. 修改配置文件

```shell
    vi /etc/ssh/sshd_config

    # Authentication:
    LoginGraceTime 2m
    #PermitRootLogin prohibit-password
    PermitRootLogin yes  # 允许 root 用户登录
    StrictModes yes
```

3. 重启SSH服务端

```shell
    sudo /etc/init.d/ssh start 
    或者 
    service ssh start
```

​    

​    
