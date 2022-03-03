---
title: Robot Framework
comments: true
tags:
  - 软件测试
  - 自动化测试，Robot Framework
categories:
  - - 软件测试
    - 自动化测试
abbrlink: 3888393026
date: 2021-05-11 00:00:00
---

**特点**
- 提供可视化界面 ride、 eclipse
- txt、html 等格式编写测试用例，而不是编程语言
- 支持**关键字驱动**（直接调用已有的关键字，组成自动化用例）
- 支持 web 、app、api 自动化测试
- 开源，基于 Python 编写

## Robot Framework 环境搭建


- **安装 wxPython**

```shell
$ 下载页面： http://wxpython.org/download.php#stable
	在选择版本下载的时候要注意选择与 Python 版本对应的版本，并且选择 unicode 版本。
	比如版本：wxPython2.8-win64-unicode-py27.exe，否则安装完成后不能支持中文。
	下载完成后，选择默认项进行安装即可。
```


- **安装 Robot Framwork**

```shell
$	pip install robotframwork
	图形化界面：RIDE
		pip install robotframework-ride
		pip install robotframework-ride==1.7.4.1（指定版本安装）
```


- **安装 selenium2library**

```shell
$	pip install robotframework-selenium2library
```


- **第三方包本地安装**

```shell
$  **.whl : 
$		pip install  **.whl
$  **.egg : 
$		1. 先下载ez_setup.py,运行python ez_setup 进行easy_install工具的安装
$		2. easy_install **.egg
$  **.zip / tar.gz
$		python setup.py install
```

- **启动 RIDE**
   - 通过文件启动（双击 [dirPath]\python\Lib\site-packages\robotide下的**init**.py文件）
   - 通过命令启动（运行 -> ride.py 回车 / 确认）
```shell
$	cd C:\Python27\Scripts\
# 运行
$ python ride.py
```

   - 将C:\Python27\Scripts\ride.py 创建快捷键，打开 ride.py 文件之后（以 python 方式打开），点击“运行（start）”按钮。
- **查看 pybot 版本**

```shell
$	cd C:\Python27\Scripts
# 运行
$ pybot --version
```

## Robot Framework + PyCharm


- **pyCharm 插件**

```shell
$	File >> Settings >> Plugins >> intelliBot 插件 install
```


- **RobotFramework 的文件类型识别配置**

```shell
$	File >> Settings >> Editor >> File Types
$		列表中 找到 Robot Feature 选中
$		File Name Patterns: 点击 +  >> 分别添加 *.txt 和 *.
```


- **Suite 和 Case 的执行配置**

```shell
$	在我们在执行脚本时，可以单独执行一个case，也可以执行case的集合：suite（测试套），所以我们这里要做两个配置。
$ 	File >> Settings >> Tools >> External Tools >> 点击 +
$ 		Name：Robot Run SingleTestCase
$		Program: C:\Python\Python27\Scripts\robot.exe
$       Arguments：-d results -t "$SelectedText$" ./
$       Working directory：$FileDir$
$	点击 + 
$       Name：Robot Run TestSuite
$		Program: C:\Python\Python27\Scripts\robot.exe
$       Arguments：-d results $FileName$
$       Working directory：$FileDir$
```


- **问题解决**

```shell
解决：‘chromedriver’ executable needs to be in PATH 问题 
（在使用 selenium 启动谷歌 Chrome 浏览器的时候，是需要用到 chromedirver 的）

    1.首先需要下载 Chromedriver，下载后得到的是一个 chromedriver.exe 文件。
        chromedriver下载地址:  http://npm.taobao.org/mirrors/chromedriver/
    2.将 chromedriver.exe 拷贝至谷歌浏览器目录（如 C:\Program Files\Google\Chrome\Application）以及 python 根目录（C:\Python27）。
    3.将谷歌浏览器环境变量添加到path（C:\Users\HD003\AppData\Local\Google\Chrome\Application）。
    至此，就可以解决 ‘chromedriver’ executable needs to be in PATH问题了。
```

## Robot Framework + Eclipse




## Robot Framework + RIDE


### RIDE 的使用


```shell
工程创建： 
	File => New Project
			=> Type: Directory(方便管理) 如果内容简单选择 file
			=> Format: 推荐 txt 
		 => New Suite(测试套件)
		 	=> Type: file
		 	=> Format: txt
		 => New Test Case
	注意： *测试套件，表示它有了新的修改，还没有保存
Project 工作区：
第一行的 Source 列出了这个 Project 的路径  

Settings:
	Documentation：文档，每一项都有。可以给当前的对象加入文档说明。
	Setup 和 TearDown 分别表示启动和停止，也就是你可以在对应的文本框设置一个关键字，那么指定的事件触发的时候就会执行这个关键字。
	Suite Stetup: 套件启动
	Suite Teardown: 套件停止
	Test Steup: 案例启动
	Test Teardown: 案例停止
	Force Tags: 强制 tag 标记，强制的给他的所有子元素加上这些tags。后面运行的时候我们可以选择指定tag的案例来运行。



资源添加：
	右键 工程名称 => New Resource
	或
	右键 External Resources => Add Resource
	
用户关键字：（Resource 用来保存用户关键字）
	右键新创建的资源 => New User Keyword 
User Keyword 工作区：
	Tags： 
    Documentation：文档，每一项都有。可以给当前的对象加入文档说明。
$$  Arguments: 设置传入参数
    Teardown: 设置完成时的动作，比如写上 Close All Browsers，表示在这个用户关键字执行完成之后会执行什么关键字。
    Timeout: 设置超时时间，如写上 1min，表示 1 分钟超时，如果这个关键字执行超过 1 分钟则认为失败。
$$  Return Value: 设置返回值
    
    User Keywords 其实就是一个函数,Bulletin 的 Keywords 和 TestLib 里的 Keywords 也都是一个个的函数，只是封装在不同层面。后 2 个是在代码级的封装，将 python 代码写成的函数封装成可以调用的关键字，而User Keywords 就是把这些可调用的关键字进一步的封装，可以理解为应用层面的封装，而且可以层层封装。到后面你会发现，大部分时间，你其实是和User Keywords在打交道，利用好User Keywords，会方便很多。
```
##### 测试套件（TestSuite）
```
测试套件工作区：
第一行的 Source 列出了这个 TestSuite 的路径

Settings:
	Documentation：
	Suite Stetup:
	Suite Teardown: 
	Test Steup: 
	Test Teardown:
	Test Template：测试模版，可以指定某个关键字为这个测试套件下所有 TestCase 的模版，这样所有的 TestCase 就只需要设置这个关键字的传入参数即可
	Test Timeout：
	Force Tags: 在文件型 Suite 这里还可以继续给子元素增加 Force Tags，但是他不能删除父元素设置的 tags
    Default Tags：默认标记，其实和 Force Tags 没啥区别的，效果都是一样的，只是颜色不同而已。
	
	
再往下大体分为三部分
（1）加载外部文件
    Add Library ：加载测试库，主要是[PYTHON目录]\Lib\site-packages里的测试库
    Add Resource：加载资源，主要是你工程相关的资源文件
    Add Variables：加载变量文件
（2）定义内部变量
    Add Scalar：定义变量
    Add List：定义列表型变量
    Add Dict：定义字典型变量
（3）元数据定义
	Add Metadata：定义元数据。作用是在 report 和 log 里显示定义好的内容，格式和 document 一样。
```


##### 测试用例（TestCase）
```shell
测试用例工作区：

Settings:
	Documentation：略
	Stetup: 略
	Teardown: 略
	Template：略
	Timeout：略
```

##### Run 页面

