---
title: Locust 性能测试
comments: true
tags:
  - 软件测试
  - 性能测试
  - locust
categories:
  - - 软件测试
    - 性能测试
abbrlink: 519960898
date: 2021-08-29 00:00:00
---

## Locust 安装及运行

- 创建虚拟环境，并进入

```shell
$ pip install locustio==0.14.6  (0.14.6 版本安装)
$ pip install locust  (最新版本安装)
$
$ 报错： error: Microsoft Visual C++ 14.0 is required. Get it with "Build Tools for Visual Studio": https://visualstudio.microsoft.com/downloads/ Tools"
$ 解决： http://go.microsoft.com/fwlink/?LinkId=691126
$ 导入win32com模块还失败，执行下面命令
$	python -m pip install pypiwin32
```

- 脚本运行

```shell
$ locust -f ***.py
	运行成功：
$ (locust_0) D:\Locust\locust_0\src>locust -f locust0-template.py
$ [2020-08-16 21:16:56,219] Yii/INFO/locust.main: Starting web monitor at http://*:8089
$ [2020-08-16 21:16:56,219] Yii/INFO/locust.main: Starting Locust 0.14.6
	
```

- 浏览器访问

```shell

本机访问： localhost:8089  
远程访问： ip / 域名：8089
	Number of total users to simulate： 模拟的总数量 20/200/2000
	Hatch rate (users spawned/second)： 每秒增加多少个用户 
	Host： 被测的服务器的 IP和端口 / 域名（http://8.129.219.235:8808）

```
## Locust 运行模式

#### Web 界面启动 (单进程)
> 参数：
>	--web-host: HOST
>   --web-port: PORT

```shell

	locust --web-host=127.0.0.1 --web-port=8088 -f .\\1000_user_load_query.py

```

#### 命令行启动 (单进程)
> 参数：
>    --headless : 禁用 Web 界面，且立即开始负载测试 需要 -u 和 -t 被指定
> 	 --host : 地址 http://192.168.40.1:8090 (https://www.baidu.com)
>    --csv : 保存执行结果  --csv=result
> 	 -u/--users : 虚拟用户数
> 	 -r/--spawn-rate : 每秒孵化数（每秒增加用户数）
>    -t/--run-time ： 运行时间（h, m, s, 1h30m）
> 	

```shell

    locust -f 1000_user_load_query.py --headless --host=http://192.168.40.1:8090 --csv=./result/result  --u 200 -r 20 -t 60s

```

#### 分布式运行（多进程）
> 角色： 
>    1. 主机： --master; 只负责管理不运行脚本
>    2. 从属主机(执行机)： --worker --master-host=主机 IP
> 	
> 注意：  
>    1. 执行机必须有主机脚本的副本
> 	 2. 同一台机子执行, 处理器的核心数就是执行机的最大数量
> 	参数：
> 	--master : 
> 	--web-host: 访问 IP
>	--web-port: 端口号
>       --master-bind-host : 要绑定的主机名，IP; 仅在 master 时使用,可以不使用             
>       --master-bind-port : 要绑定的主机端口号; 仅在 master 时使用,可以不使用
> 	--expect-workers : 执行机数量 仅在 headless 时使用
> 
>   --worker : 如果 master 和 worker 不在同一台机器上， worker 需要指定 --master-host 参数
>   --master-host : 运行 master 时设置的 host                   
>   --master-port : 运行 master 时设置的 port


- Web 界面启动
```shell

# 主机启动
	locust -f 1000_user_load_query.py --master --web-host=192.168.40.1

# 从机启动（每次启动一个执行机）
	locust -f .\\1000_user_load_query.py --worker --master-host=主机 IP  

```
## FastHttpUser 和 HttpUser
> FastHttpUser
> HttpUser

## Locust + geventhttpclient
> geventhttpclient

## SequentialTaskSet 和 TaskSet
> SequentialTaskSet
> TaskSet


## Locust 多进程 数据共享
> 


## Locust 运行 Go 语言

> 使用 Locust + Go 实现性能测试， 比 py 脚本性能提高到 5 - 10 倍
> 待研究。。。。。。