---
title: docker
comments: true
tags:
  - docker
  - 容器
categories:
  - - 前沿技术
    - Docker
abbrlink: 4065722285
date: 2020-10-17 00:00:00
---
## Docker 安装

1. 通过 uname -r 命令查看你当前的内核版本
    ```shell
    $ uname -r
    ```


2. root权限更新Yum包
    ```shell
    $ yum update
    ```

3. 卸载旧版本：（如果安装过旧版本的话）
(旧版名称是docker , 最新社区版 docker-engine， 目前已改名为docker-ce )

    ```shell
    $ yum -y remove docker docker-common docker-selinux docker-engine
    ```

4. 设置Yum源：（本文以Yum安装为例子进行安装）

- 安装 yum-utils , 使用 yum-config-manager 工具设置Yum源, 后面两个是 devicemapper驱动依赖

    ```shell
    $ yum install -y yum-utils device-mapper-persistent-data lvm2
    ```

- 执行以下命令，添加docker的yum源
    ```shell
     $ yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
     # 此处可能会报错 （原因是国内访问不到docker官方镜像的缘故）
     Loaded plugins: fastestmirror（镜像）
     adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
     grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
     Could not fetch/save url https://download.docker.com/linux/centos/docker-ce.repo to file /etc/yum.repos.d/docker-ce.repo: 
     [Errno 14] curl#35 - "TCP connection reset by peer
    
     # 解决方法 ： 使用阿里源访问
    $ yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    ```

5. 查看所有仓库中docker版本，并选择特定版本安装：(此处我们查看社区版 docker-ce)
    ```shell
    $ yum list docker-ce --showduplicates | sort -r
    ```

6. 配置镜像加速器（必须要配置，否则会出现访问镜像并不稳定 ，而且下载缓慢等问题）
- 注册阿里云账号 ，登陆该网址自行注册 ( https://www.aliyun.com/?utm_content=se_1010377 )
- 进入阿里云控制台如图 ( https://cr.console.aliyun.com/#/accelerator )
- 执行命令 :
    ```shell
    
    $ mkdir -p /etc/docker
    $ tee /etc/docker/daemon.json <<-'EOF'
    > { 
    >    "registry-mirrors": ["输入你自己控制台此处的地址"]
    > }
    EOF
    $  systemctl daemon-reload    （导入操作）
    ```

7. 安装docker (此处我们安装社区版 docker-ce)
    ```shell
    
    $ yum install docker-ce (这样写默认安装最新版本)
    $ yum install  docker-ce-<VERSION_STRING> (指定安装版本) 
    #例： yum install docker-ce-18.03.1.ce
    ```
    
8. 启动并加入开机启动
    ```shell
    $ systemctl start docker       (重启命令  $  systemctl restart docker ) 
    $ systemctl enable docker   开机启动
    $ docker version  查看docker版本号
    ```

9. 验证是否安装成功
    ```shell
    $ docker run hello-world
    ```
## Docker 基本命令

- 查看所有运行或者不运行容器
- 列出所有容器ID
- 停止所有的container（容器），这样才能够删除其中的images：
- 如果想要删除所有container（容器）的话再加一个指令：
- 查看当前有些什么images
- 删除images（镜像），通过image的id来指定删除谁

    ```shell
    docker ps
    docker ps -a
    docker ps -aq
    docker images
    docker exec -it [name / id] /bin/bash
    exit()
    ```

## Docker 开机配置

- docker 中启动所有的容器命令
    ```shell
        docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)
    ```

- docker 中关闭所有的容器命令
    ```shell
        docker stop $(docker ps -a | awk '{ print $1}' | tail -n +2)
    ```

- docker 中删除所有的容器命令
    ```shell
        docker rm $(docker ps -a | awk '{ print $1}' | tail -n +2)
    ```

- docker 中删除所有的镜像
    ```shell
        docker rmi $(docker images | awk '{print $3}' |tail -n +2)
    ```
