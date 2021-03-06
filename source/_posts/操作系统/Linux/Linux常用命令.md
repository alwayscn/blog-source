---
title: linux 命令总结
tags:
  - linux
  - linux 命令
categories:
  - - 操作系统
    - Linux
comments: true
abbrlink: 1564283385
date: 2020-11-02 00:00:00
---

**[ 命令格式 ]**

- 命令 [ 选项 ][ 参数 ]
- 例： ls -la /home

### 目录处理命令

- ls
  - 原意： list
  - 功能： 显示目录文件
  - 选项： -a： 显示所有文件(all)，-l： 显示详细信息(long)
  - 参数： 路径（非必填）
  - 语法： ls -la /home
- cd
  - 原意： change directory
  - 功能： 切换目录
  - 参数： 路径
  - 语法： cd /home (绝对路径) 或者 cd admin (相对路径)
- pwd
  - 原意： print working directory
  - 功能： 显示当前目录
  - 语法： pwd
- mkdir
  - 原意： make directories
  - 功能： 创建空目录
  - 选项： -p： 递归创建(可以创建不存在的目录，如： /home/admin/document/work)
  - 参数： 目录名
  - 语法： mkdir -p [目录名]
- cp
  - 原意： copy
  - 功能： 复制文件或目录
  - 选项： -r： 复制目录，-p： 保留文件属性 copy(保留创建时间等)
  - 参数： [原文件或目录][目标目录]
  - 语法： cp -rp [原文件或目录][目标目录]
- mv

  - 原意： move
  - 功能： 剪切文件或者改文件名
  - 参数： [原文件或目录][目标目录] 或者 [原文件名][修改文件名]
  - 语法： mv [原文件或目录][目标目录]

- rm
  - 原意： remove
  - 功能： 删除文件或目录
  - 选项： -r： 删除目录，-f： 强制删除
  - 参数： 文件或目录
  - 语法： rm -rf [文件或目录] ==> 强制删除
- rmdir
  - 原意： remove empty directories
  - 功能： 删除空目录
  - 语法： rmdir [空目录]

### 文件处理命令

- touch
  - 功能： 创建空文件
  - 语法： touch [文件名]
- cat
  - 功能： 显示文件内容
  - 选项： -n 显示行号
  - 语法： cat [文件名]
- tac

  - 功能： 反向显示文件内容
  - 选项： -n 显示行号
  - 语法： tac [文件名]

- more
  - 功能： 分页显示文件内容
  - 语法： more [文件名]
  - 操作： 空格 => 换页; Enter => 换行; Q => 退出; （B => 上翻）
- ln
  - 原意： link
  - 功能： 创建软链接(快捷方式)或硬链接(复制文件，文件内容动态变化)
  - 选项： -s： 创建软链接
  - 语法： ln -s [原文件或目录][目标文件或目录] ==> 软链接; ln [原文件或目录][目标文件或目录] ==> 硬链接;
- less
  - 功能： 分页显示文件内容
  - 语法： less [文件名]
  - 操作： 空格 => 换页; Enter => 换行; Q => 退出; B => 向上翻页
- head
  - 功能： 显示文件前面几行
  - 选项： -n： 指定行数
  - 语法： head -n 10 [文件名]
- tail
  - 功能： 显示文件后面几行
  - 选项： -n： 指定行数; -f： 动态显示文件末尾的内容
  - 语法： tail -n 10 [文件名]

### 文件搜索命令

- find

  - 功能： 文件搜索
  - 语法： find [搜素范围][匹配条件] [搜素内容]
  - 例： find /home -name log.md (搜素 log.md 文件)
    > [ 匹配条件 ]
    >
    > - name： 名称搜素
    > - size： 文件大小搜素(按块搜素，1 块 = 0.5k，00M = 204800 块)
    >
    > * +n(+204800) 大于 204800
    > * -n
    > * n 等于
    >
    > - type： 文件类型

- grep

  - 功能： 在文件中搜索字符串匹配的行并输出
  - 选项： -i 不区分大小写; -v 排除指定字符串
  - 语法： grep -iv [指定字符串][文件]

- locate
  - 功能： 在文件资料库中查找文件
  - 语法： locate [文件名]
- which
  - 功能： 搜索命令所在目录及别名信息
  - 语法： which [命令]
- whereis
  - 功能： 搜索命令所在目录以及帮助文档路径
  - 语法： whereis [命令]

### 帮助命令

- man
  - 功能： 获取帮助信息
  - 语法： man [命令或帮助文件]
- help
  - 功能： 获取 shell 内置命令的帮助信息
  - 语法： help [内置命令]

### 权限管理命令

- chmod
  - 原意： change mode
  - 功能： 改变文件或目录的权限
  - 语法： chmod [ugoa+-=rwx][文件或目录]
  - 例： chmod u-r [文件或目录] => 对文件的所属者去掉 r 权限
  - 语法： chmod [mode = 777][文件或目录] => 给文件设置所有的用户拥有全部的权限
  - 例： chmod 764 [文件或目录]
  - 执行权限： 所有用户

> **[ u，g，o，a 分别代表用户 ]**
>
> - u： User 所属者
> - g： Group 用户组
> - o： Other 其他用户
> - a： all 所有人
>
> **[ r，w，x 分别代表权限 ]**
>
> - r： read 读权限
>   - 用数字表示 4
> - w： write 写权限
>   - 用数字表示 2
> - x： 执行权限
>   - 用数字表示 1
> - 每一个文件或目录都会用 rwxrwxrwx 来显示 ugo 三者的权限(顺序不可变)
> - 例： rwxrw-r-- 指的是 u 拥有所有的权限，g 拥有读写的权限，o 只拥有>读的权限
>   - 用数字表示： 764（4+2+1，4+2，4）

- chown
  - 原意： change file ownership
  - 功能： 改变文件或目录的所属者
  - 语法： chown [用户][文件/目录]
  - 执行权限： root
- umask
  - 命令英文原意： the user file-creation mask
  - 显示、设置文件的缺省权限(默认权限)
  - 执行权限： 所有用户
  - 语法： umask [-S] -S 以 rwx 形式显示新建文件的缺省权限

### 用户管理命令

- useradd
  - 功能： 添加新用户
  - 执行权限： root
- passwd
  - 功能： 修改密码
- who
  - 功能： 查看登录用户信息
- w
  - 功能： 当前用户详细信息

### 压缩解压命令

- tar
  - 功能： 打包文件或目录
  - 说明： **结合 gzip 命令**
  - 语法： tar -zcf 新的文件名.tar.gz [目标文件或目录] ==>直接打包压缩
  - 解压： tar -zxf 文件名.tar.gz
- zip
  - 功能： 压缩文件或目录
  - 选项： -r 压缩目录
  - 语法： zip [新的文件名][目标文件或目录]
  - 解压： unzip [压缩文件名.zip]
- bzip2
  - 功能： 打包文件()
  - 选项： -k 保留原文件
  - 说明： **结合 tar 命令使用**
  - 语法： tar -cjf 新的文件名.tar.bz2 [目标文件或目录] ==>直接打包压缩
  - 解压： tar -xjf 文件名.tar.bz2

### 网络命令

- ping
  - 功能： 测试网络连通性
  - 语法： ping [ip 地址]
- last
  - 功能： 列出目前和过去登入系统的用户信息
  - 语法： last
- traceroute
  - 功能： 显示数据包到主机间的路径
  - 语法： traceroute [ip 地址 或 域名]
- netstat
  - 功能： 显示网络相关信息
  - 语法： netstat
- steup
  - 功能： 配置网络
  - 语法： steup
- write
  - 功能： 给用户发信息
  - 语法： write [用户名]
- wall
  - 功能： 发广播信息
  - 语法： wall
- mail
  - 功能： 发送电子邮件
  - 语法： mail [用户名]

### 关机重启命令

- shutdown [选项] now(时间)
  - -c 取消
  - -h 关机
  - -r 重启
- 其他关机
  - halt
  - poweroff
  - init 0
- 其他重启
  - reboot
  - init 6
- 扩展

* 0 --> 关机
* 1 --> 单用户
* 2 --> 不完全多用户，不含 nfs 服务
* 3 --> 完全多用户
* 4 --> 未分配
* 5 --> 图形界面
* 6 --> 重启
