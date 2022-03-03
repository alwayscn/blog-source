---
title: github + hexo 搭建个人博客
comments: true
tags:
  - github
  - hexo
  - github 博客
categories:
  - - 博客搭建
abbrlink: 1613536721
date: 2022-01-28 00:00:00
---

## 安装 Node.js

首先下载稳定版

[下载 Node.js](https://nodejs.org/dist/v9.11.1/node-v9.11.1-x64.msi)

我这里给的是64位的。

安装选项全部默认，一路点击`Next`。

最后安装好之后，按`Win+R`打开命令提示符，输入`node -v`和`npm -v`，如果出现版本号，那么就安装成功了。

## 添加国内镜像源

如果没有梯子的话，可以使用阿里的国内镜像进行加速。

```bash
npm config set registry https://registry.npm.taobao.org
```

## 安装 Git

为了把本地的网页文件上传到 github 上面去，我们需要用到分布式版本控制工具————Git

[下载 Git](https://git-scm.com/download/win)

安装选项还是全部默认，只不过最后一步添加路径时选择`Use Git from the Windows Command Prompt`，这样我们就可以直接在命令提示符里打开git了。

安装完成后在命令提示符中输入`git --version`验证是否安装成功。

## 注册 Github 账号

接下来就去注册一个 github 账号，用来存放我们的网站。大多数小伙伴应该都有了吧，作为一个合格的程序猿（媛）还是要有一个的。

打开 [ github ]([GitHub](https://github.com/)), 新建一个项目，输入自己的项目名字，README 初始化也要勾上。

然后项目就建成了，点击`Settings`，向下拉到最后有个`GitHub Pages`，点击`Choose a theme`选择一个主题。然后等一会儿，再回到`GitHub Pages`，

点击那个链接，就会出现自己的网页啦



## 安装 Hexo



在合适的地方新建一个文件夹，用来存放自己的博客文件，比如我的博客文件都存放在`D:\study\program\blog`目录下。

在该目录下右键点击`Git Bash Here`，打开 git 的控制台窗口，以后我们所有的操作都在 git 控制台进行，就不要用 Windows 自带的控制台了。

定位到该目录下，输入`npm i hexo-cli -g` 安装 Hexo。会有几个报错，无视它就行。

安装完后输入`hexo -v`验证是否安装成功。

然后就要初始化我们的网站，输入`hexo init`初始化文件夹，接着输入`npm install`安装必备的组件。

这样本地的网站配置也弄好啦，输入`hexo g`生成静态网页，然后输入`hexo s`打开本地服务器，然后浏览器打开 [http://localhost:4000/](https://link.zhihu.com/?target=http%3A//localhost%3A4000/)，就可以看到我们的博客啦

按`ctrl+c`关闭本地服务器。

官网： https://hexo.io/zh-cn/docs/

## 连接 Github 与本地

首先右键打开 git bash，然后输入下面命令：

```bash
git config --global user.name "alwayscn"
git config --global user.email "123@yeah.net"

```

用户名和邮箱根据你注册 github 的信息自行修改。

然后生成密钥 SSH key：

```bash
ssh-keygen -t rsa -C "123@yeah.net"

```

打开 [github](https://github.com)，在头像下面点击`settings`，再点击`SSH and GPG keys`，新建一个SSH，名字随便。

git bash 中输入

```bash
cat ~/.ssh/id_rsa.pub
```

将输出的内容复制到框中，点击确定保存。

输入`ssh -T git@github.com`，如果如下图所示，出现你的用户名，那就成功了。

打开博客根目录下的`_config.yml`文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。

修改配置：

```bash
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://alwayscn.github.io/alwaysblog/
root: /


deploy: 
  type: git 
  repository: git@github.com:alwayscn/alwaysblog.git
  branch: main
```

repository 修改为你自己的 github 项目地址。

## 写文章、发布文章

首先在博客根目录下右键打开 git bash，安装一个扩展`npm i hexo-deployer-git`。

然后输入`hexo new post "article title"`，新建一篇文章。

然后打开`D:\study\program\blog\source\_posts`的目录，可以发现下面多了一个文件夹和一个`.md`文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦。

编写完 markdown 文件后，根目录下输入`hexo g`生成静态网页，然后输入`hexo s`可以本地预览效果，最后输入`hexo d`上传到 github 上。这时打开你的主页就能看到发布的文章啦。



## 备份博客源文件

有时候我们想换一台电脑继续写博客，这时候就可以将博客目录下的所有源文件都上传到 github 上面。

首先在 github 博客仓库下新建一个分支`hexo`，然后`git clone`到本地，把`.git`文件夹拿出来，放在博客根目录下。

然后`git branch -b hexo`切换到`hexo`分支，然后`git add .`，然后`git commit -m "xxx"`，最后`git push origin hexo`提交就行了。
