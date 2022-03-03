---
title: python 基础
tags:
  - python
categories:
  - - 后端领域
    - 编程语言
    - python
comments: true
abbrlink: 2562162005
date: 2021-10-02 00:00:00
---

## Python 环境搭建

- 下载安装

```shell
$ 下载页面：https://www.python.org/downloads/windows/
	2.7：https://www.python.org/downloads/release/python-2718/（选择：Windows x86-64 MSI installer）
	3.8：https://www.python.org/downloads/release/python-385/（选择：Windows x86-64 executable installer）

	2.7 版本直连：https://www.python.org/ftp/python/2.7.18/python-2.7.18.amd64.msi
	3.7 版本直连：https://www.python.org/ftp/python/3.7.9/python-3.7.9-amd64.exe
```


- pip 升级



```shell
$ python2 -m pip install --upgrade pip --force-reinstall
$ python3 -m pip install --upgrade pip --force-reinstall
```


- 虚拟环境



```shell
在 python3 的环境下创建

$ 安装虚拟环境软件包：pip3 install virtualenv
$ 创建虚拟环境： virtualenv Venv
$ 虚拟环境管理器安装： pip3 install virtualenvwrapper-win
$ 添加全局变量配置虚拟环境路径： WORKON_HOME  / C:\Python\Virtualenv    => 虚拟环境都创建在此目录下
    创建虚拟环境： mkvirtualenv Venv(虚拟环境名称)
    激活虚拟环境： workon Venv(虚拟环境名称)
    退出虚拟环境： deactivate
    删除虚拟环境： rmvirtualenv Venv(虚拟环境名称)
    列出虚拟环境： workon / lsvirtualenv

	创建虚拟环境指定 Python 版本： mkvirtualenv --python==C:\Python\Python37\python.exe 虚拟环境名称
```


- 第三方包本地安装



```shell
$  **.whl : 
$		pip install  **.whl
$  **.egg : 
$		1. 先下载ez_setup.py,运行python ez_setup 进行easy_install工具的安装
$		2. easy_install **.egg
$  **.zip / tar.gz
		python setup.py install
```
## Python 数据类型


**不可变数据类型：** Number（数字）、String（字符串）、Tuple（元组）


**可变数据类型：**   List（列表）、Dictionary（字典）、Set（集合）


**序列容器：** String（字符串）、List（列表）Tuple（元组）


**非序列容器**：Dictionary（字典）、Set（集合）


### 数据类型之间的运算规则


- 算术运算符



```
常见运算符：+ 、 - 、 * 、/ （/ 在 python2 和 python3 中的作用不同）

** : 幂运算 2 ** 3 <==> 2 的三次方
// : 取整运算
%  ：取余运算

/ 在python 2.X 当除数与被除数都是整数时，取整数，当其中一个为浮点数时，结果为浮点数，在 3.x 则直接为浮点数
```


- 赋值运算符



```
常见运算符：= 、+= 、-= 、*=、/= (A += B 相当于 A = A + B)

//=	: A //= B <==> A = A // B
%=	: A %= B <==> A = A % B
**= : A **= B <==> A = A ** B
```


- 比较运算符



```
常见运算符：>, < , >=, <=, ==, != 

Python 中 没有 全等于 ===
```


- 逻辑运算符



```python
# 逻辑运算符:逻辑与 and， 逻辑或 or， 逻辑非not (and，全真则真； or，全假为假)
# and(且)  ==> 非 0 为真， 0 为假
ret = 0 and 2 # ==> 第一个条件为假，没有必要检查第二个条件 故 输出第一个条件 0
ret = 1 and 0 # ==> 第一个条件为真，第二个条件必须执行   输出第二个条件 0
ret = 1 and 2 # ==> 第一个条件为真，第二个条件必须执行   输出第二个条件 2

# or(或)   ==> 一个为真则为真
ret = 1 or 2  # 检查第一个条件，为真， 输出第一个条件 0
ret = 0 or 1  # 第一个条件为假，第二个条件必须执行   输出第二个条件 1
ret = 0 or 0  # 第一个条件为假，第二个条件必须执行   输出第二个条件 0
```


- **数据类型之间运算规则**



```
总结：
  1. 数字和数字之间可以进行所有的运算
  2. 字符串和字符串之间只能进行加法运算
  3. 数字和字符串之间只能进行乘法运算
```


### 数据类型转换


**前提：可以转换为目标类型**


- 转换为 Number 类型



```python
value = '666'
int(value) # ==> 666
```


- 转换为 String 类型



```python
value = 666
str(value)  ==> '666'
```


- 转换为 float 类型



```python
value = 666 # ‘666’呢？
float(value)  ==> 666.00
```


### 数字（Number）


- 整数（integer）
- 小数 / 浮点数（float）



**[ 常用的数字函数 ]**


```python
abs(x)          #返回数字的绝对值，如abs(-10) 返回 10
math.fabs(x)    #返回数字的绝对值，如math.fabs(-10) 返回10.0
exp(x)          #返回e的x次幂(e^x),如math.exp(1) 返回2.718281828459045
math.log(x)     #返回x的对数如math.log(math.e)返回1.0,math.log(100,10)返回2.0
math.log10(x)   #返回以10为基数的x的对数，如math.log10(100)返回 2.0
math.modf(x)    #返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示
pow(x)          #返回x**y 运算后的值
math.sqrt(x)    #返回数字x的平方根
round(x,[n])    #返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数
math.sin(x)     #返回的x弧度的正弦值
```


### 字符串（String）


- 字符串是 Python 中最常用的数据类型。我们可以使用引号( ’ 或 " )来创建字符串
- 字符串切片索引



```python
str = 'Runoob'

print (str)          # 输出字符串
print (str[0:-1])    # 输出第一个到倒数第二个的所有字符
print (str[0])       # 输出字符串第一个字符
print (str[2:5])     # 输出从第三个开始到第五个的字符
print (str[2:])      # 输出从第三个开始的后的所有字符
print (str * 2)      # 输出字符串两次
print (str + "TEST") # 连接字符串

# 输出

Runoob
Runoo
R
noo
noob
RunoobRunoob
RunoobTEST
```


**[ python三引号 ]**


python 三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符


```python
para_str = """这是一个多行字符串的实例
    多行字符串可以使用制表符
    TAB ( \t )。
    也可以使用换行符 [ \n ]。
    """
print (para_str)
# 输出

这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (    )。
也可以使用换行符 [ 
]。
```


### 列表（List）


- 列表是最常用的 Python 数据类型，它可以作为一个方括号内的逗号分隔值出现，列表的数据项不需要具有相同的类型
- 创建一个列表，只要把逗号分隔的不同的数据项使用方括号括起来即可
- 列表切片索引



**[ 常用的列表函数 ]**


```python
list.append(obj)          #在列表末尾添加新的对象
list.count(obj)           #统计某个元素在列表中出现的次数
list.extend(seq)          #在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
list.index(obj)           #从列表中找出某个值第一个匹配项的索引位置
list.pop([index=-1])      #移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
list.remove(obj)          #移除列表中某个值的第一个匹配项
list.reverse()            #反向列表中元素
list.sort( key=None, reverse=False)    #对原列表进行排序,True 降序,False 升序（默认）
list.clear()              #清空列表
list.copy()               #复制列表
```


### 元组（Tuple）


- 元组与列表类似，不同之处在于元组的元素不能修改



### 字典（Dictionary）


- 字典是另一种可变容器模型，且可存储任意类型对象
- **dict = {key1 : value1, key2 : value2 }：**每个键值(key=>value)对用冒号(:)分割，每个对之间用逗号(,)分割，整个字典包括在花括号({})中
- **注意：**键必须是唯一的，但值则不必；值可以取任何数据类型（如字符串，数字或元组），但键必须是不可变的。



**[ 访问字典的值 ]**


```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
'''
    del dict['Name']     # 删除键 'Name'
    dict.clear()         # 清空字典
    del dict             # 删除字典

    '''
print ("dict['Name']: ", dict['Name'])
print ("dict['Age']: ", dict['Age'])
# 输出
dict['Name']:  Runoob
    dict['Age']:  7
```


**[ 字典键的特性 ]**


- 不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住



```python
dict = {'Name': 'Runoob', 'Age': 7, 'Name': '小菜鸟'}

print ("dict['Name']: ", dict['Name'])
123
#输出
dict['Name']:  小菜鸟
    12
```


- 键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行



```python
dict = {['Name']: 'Runoob', 'Age': 7}

print ("dict['Name']: ", dict['Name'])
123
#输出
Traceback (most recent call last):
    File "test.py", line 3, in <module>
    dict = {['Name']: 'Runoob', 'Age': 7}
    TypeError: unhashable type: 'list'
```


**[ 字典函数 ]**


```python
radiansdict.clear()          #删除字典内所有元素
pop(key[,default])           #删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值
```


### 集合（Set）


- 集合是一个无序的不重复元素序列，可以使用大括号 { } 或者 set() 函数创建集合
- **注意：**创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典



```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)                      # 去重功能
#输出
{'orange', 'banana', 'pear', 'apple'}

'orange' in basket                 # 快速判断元素是否在集合内
#输出
True

'crabgrass' in basket
#输出
False

# 下面展示两个集合间的运算
a = set('abracadabra')
b = set('alacazam')
print(a)
#输出                                  
{'a', 'r', 'b', 'c', 'd'}

print(a - b)                              # 集合a中包含而集合b中不包含的元素
#输出
{'d', 'b', 'r'}

print(a | b)                              # 集合a或b中包含的所有元素
#输出
{'c', 'b', 'r', 'z', 'l', 'm', 'a', 'd'}

print(a & b)                              # 集合a和b中都包含了的元素
#输出
{'a', 'c'}

print(a ^ b)                              # 不同时包含于a和b的元素
#输出
{'l', 'b', 'z', 'r', 'm', 'd'}
```


**[ 添加元素 ]**


- **s.add( x )** 将元素 x 添加到集合 s 中，如果元素已存在，则不进行任何操作



```python
thisset = set(("Google", "Runoob", "Taobao"))
thisset.add("Facebook")
print(thisset)
#输出
{'Taobao', 'Facebook', 'Google', 'Runoob'}
```


- **s.update( x )** 参数可以是列表，元组，字典等



```python
thisset = set(("Google", "Runoob", "Taobao"))
thisset.update({1,3})
print(thisset)
#输出
{1, 3, 'Google', 'Taobao', 'Runoob'}

thisset.update([1,4],[5,6])  
print(thisset)
#输出
{1, 3, 4, 5, 6, 'Google', 'Taobao', 'Runoob'}
```


**[ 移除元素 ]**


```python
s.remove( x )		# 将元素 x 从集合 s 中移除，如果元素不存在，则会发生错误

s.discard( x )		# 移除集合中的元素，如果元素不存在，不会发生错误

s.pop()				# 随机删除集合中的一个元素，在交互模式，pop 是删除集合的第一个元素（排序后的集合的第一个元素）
```


**[ 集合函数 ]**


```python
add()	        #为集合添加元素
clear()	        #移除集合中的所有元素
copy()	        #拷贝一个集合
union()	        #返回两个集合的并集
update()	    #给集合添加元素
```


## Python 输入输出


### 标准输入输出函数


- **print()** 标准输出函数



```python
#  换行符  \n,  end='\n'
print('aaa' end='') # 不换行
print('bbb' end='#') # bbb 和 ccc 之间用 # 连接
print('ccc')

# 格式化输出
name = '鲁班'
age = 20

> %s ==> string
> %d ==> digit(数字)
> %f ==> float
> %% ==> 输出 %

print('他的名字是' + name +',他的年龄是' + age + '。') # 输出格式
print('他的名字是%s,他的年龄是%d。' %(name, age))

print('胜率%d%%' % 87)  # %% 表示 %  ==> 87%
```


- **input()** 标准输入函数,输入的内容是字符串



```python
print('请输入你的姓名：')
input()
<==> input('请输入你的姓名：')

# 保存输入的数据

input_content = input('请输入你的姓名：')
print( input_content)
# 动态
print('欢迎您 %s !' % input_content)
```


## Python 分支语句


### if 分支语句


- 比较运算符



```
==  相等, !=  不相等, >   大于, <   小于, >=  大于等于, <=  小于等于
```


- if 语句



```python
if a > b  :
    ret = a -b
    else:
        ret = a + b
        print(ret)
```


- 多个条件之间的关系



```python
# and(且)  ==> 非 0 为真， 0 为假
ret = 0 and 2 # ==> 第一个条件为假，没有必要检查第二个条件 故 输出第一个条件 0
ret = 1 and 0 # ==> 第一个条件为真，第二个条件必须执行   输出第二个条件 0
ret = 1 and 2 # ==> 第一个条件为真，第二个条件必须执行   输出第二个条件 2

# or(或)   ==> 一个为真则为真
ret = 1 or 2  # 检查第一个条件，为真， 输出第一个条件 0
ret = 0 or 1  # 第一个条件为假，第二个条件必须执行   输出第二个条件 1
ret = 0 or 0  # 第一个条件为假，第二个条件必须执行   输出第二个条件 0

# 例  and 优先级 高于 or
a = 10
b = 20
ret = a > b and a or b
= false and a or b
= false or b
= b                 # ==> b 20
ret = a < b and a or b
= true and a or b
= a or b
= a                 # ==> a 10
# not(非)
```


### while 语句


```python
"""
    我不喜欢这个世界，我只喜欢你！
    """
# while 循环

# i = 1
# while i <= 100:
#     print(i)
#     i += 1
#
# print('END')

# 1-100 偶数

# i = 1
# while i <= 100:
#     # print(i)
#     # i += 2
#     if i % 2 == 0:
#         print(i)
#     i += 1

# 1-100 累加和

# start = 1
# end = 100
# total = 0
# while start <= end:
#     total = total + start
#     start += 1
# print(total)

# start = int(input('开始数：'))
# end = int(input('结束数：'))
# total = 0
# while start <= end:
#     total = total + start
#     start += 1
# print(total)

# 1-100 奇数和

# start = 1
# total = 0
# while start <= 100:
#     if start % 2 != 0:
#         total = total + start
#     start += 1
# print('奇数和：',total)

# 打印 *

# n = 1
# while n <= 5:
#     print('*' * n)
#     n += 1

# 1- 100 除 50 不累加

# index = 1
# total = 0
# while index <= 100:
#     if index != 50:
#         total = total + index
#     index += 1
# print(total)
# index = 1
# total = 0
# while index <= 100:
#     if index == 50:
#         index += 1
#         continue  # 跳过本次循环 不是退出循环
#     total = total + index
#     index += 1
# print(total)

# 大于 50 停止循环

# i = 1
# while i <= 100:
#     if i > 50:
#         break  # 后边的代码不执行，并且终止循环
#     i += 1
# print(i)

# 简易版员工管理系统
# 1 展示信息
# 2 新增信息
# 3 修改信息
# 4 删除信息
# 5 退出

while True:
    print('欢迎使用')
    print('*' * 10 + '操作菜单' + '*' * 10)

    print('1. 展示信息')
    print('2. 新增信息')
    print('3. 修改信息')
    print('4. 删除信息')
    print('5. 退出')
    # 保存用户操作
    user_operation = int(input('请输入您的操作：'))
    if user_operation == 1:
        print('姓名\t年龄\t')
        print('鲁班\t20\t')
        print('吕布\t30\t')
        print('小乔\t18\t')
        elif user_operation == 2:
            name = input('请输入姓名：')
            age = input('请输入年龄：')
            print('%s 添加成功'% name)
            elif user_operation == 3:
                name = input('请输入修改姓名')
                print('%s 修改成功'% name)


                elif user_operation == 4:
                    name = input('请输入修改姓名')
                    print('%s 删除成功'% name)
                    elif user_operation == 4:
                        print('退出成功')
                        break
                        else:
                            print('输入有误')

                            print('*' * 27)
```


## Python 函数操作


```python
# 定义函数：
def 函数名():
	一行或多行代码

# def sum(a, b):
#     ret = a + b
#     return ret
# result =  sum(10, 20)
# result = result + 100
# print(result)

# 两个数之间的所有数之和

start = int(input('输入开始数字：'))
end = int(input('输入结束数字：'))
def sum(start, end):
    """这是我的函数文档"""
    if not isinstance(start, int):
        print('请输入整数')
        return None
    if not isinstance(end, int):
        print('请输入整数')
        return None
    if start > end:
        print('start 必须小于 end')
        return None
    total = 0
    whi le start <= end:
        total = total + start
        start += 1
        print(total)

        sum(start, end)

        # 输入运算符进行计算

        while True:
            Operator = input('请输入运算符')

            def Operation(left, right, Oper):
                a = left
                b = right
                if Oper == '+':
                    result = a + b
                    elif Oper == '-':
                        result = a - b
                        elif Oper == '*':
                            result = a * b
                            elif Oper == '/':
                                result = a / b
                                else:
                                    print('输入有误')
                                    result = None
                                    return result

                                result = Operation(10, 20, Operator)
                                print(result)
```


## 数据类型基础操作


### 字符串（String）


> 维度：方法的作用，参数，返回值，原数据是否改变



##### 符串的遍历


```python
istr = 'hello'
# 方法一
i = 0
while i < 5:
    print(istr[i])
    i += 1
    # 方法二
    for v in istr:
        print(v, end=' ')
```


##### 字符串的替换


- **replace()** [ str.replace('old', 'new', 替换次数) ]



```python
strEmail = 'zxymaibox@yeah.net'

newstr = strEmail.replace('y','#') # 将所有的 y 替换成 ‘#’
newstr = strEmail.replace('y','#', 1) # 只替换第一次出现的 y
```


##### 字符串查找


- **find()**
- 返回第一次出现的位置，如果没有则返回 -1



```python
strEmail = 'zxymaibox@yeah.net'

# 找到 @ 的位置

strEmail.find('@')
```


##### 字符串的切片


```python
# 以 @ 获取前后内容

strEmail = 'zxymaibox@yeah.net'
possion = strEmail.find('@')  # 10

# *****************

strEmail[起始 : 结束 : 步长]

# 起始值不写表示从 0 开始
print(strEmail[: 9])

# 结束值不写表示到最后
print(strEmail[10:])

# 步长(第三个值表示步长)
print(strEmail[0: 9: 1])  <==> print(strEmail[0 : 9]) # zxymaibox
print(strEmail[0: 9: 2])  # zyabx
print(strEmail[0: 9: 3])  # zmb

# 起始 : 结束 : 步长 可以是负值
print(strEmail[9: 1: -1]  # xobiamyxz

      # 字符串的逆序
      print(strEmail[:: -1])

      # *****************

      # 切片语法左闭右开

      方法一：

      username => print(strEmail[0: 9])
      # 获取字符串长度
      length = len(strEmail)

      houzhui => print(strEmail[10: length])

      方法二：

      username = strEmail[:possion]
      houzhui = strEmail[possion + 1:]
      print(username, houzhui)
```


##### 字符串拆分成列表


- **split()**
- 返回拆分后的列表



```python
# 以 @ 获取前后内容
strEmail = 'zxymaibox@yeah.net'

# 查询某一字符出现的次数
strCount = strEmail.count('@')

if strCount == 1:
    result = strEmail.split('@')

    print(result)  # => ['zxymaibox', 'yeah.net']

    username = result[0]
    houzhui = result[1]
```


##### 查询某一字符出现的次数


- **count()**



```python
strEmail = 'zxymaibox@yeah.net'

print(strEmail.count('@')) # => 1
print(strEmail.count('y')) # => 2
```


##### 判断字符串是否全为字母


- **isalpha()** [str.isalpha()]
- 返回布尔值



##### 字符串去除两侧空格


- **strip()**
- 返回新的字符串



### 列表（List）


```python
list = [10, 20, 30, 40]
# 列表支持切片语法,可以切成小列表
list[:: -1]
```


##### 列表的遍历


```python
list = [10, 20, 30, 40]
# 方法一
index = 0
length = len(list)
while index < length:
    print(list[index])
    index += 1
    # 方法二
    for val in list:
        print(val)
```


##### 列表元素插入


```python
list = [10, 20, 30, 40]
# 尾部插入
list.append(30)
# 指定位置插入
list.insert(0, 200)
```


##### 列表元素删除


- **pop()** 位置删除，[ 无参数的时候，默认删除最后一个位置的元素 ]
- **remove()** 值删除， [ 默认删除第一次出现的值 ]
- **clear() **清空列表，



```python
list = [10, 20, 30, 40, 20]
# 位置删除 pop
list.pop()
list.pop(2)
#  值删除
list.remove(20)
# 列表清空
list.clear()
```


##### 列表元素查找和修改


- **index(oldValue)** [ 如果值存在返回位置，不存在会报错 ]
- **count(oldValue)** [ 查找出现的次数，如果不为 0 ，再使用 index 方法 ]



```python
list = [10, 20, 30, 40]
# if list.count(20) != 0:
#     indexC = list.index(20)
#     # 修改值
#     list[indexC] = 20

或
#  in 和 not in 判断值是否存在

if 20 in list:
    indexC = list.index(20)
    # 修改值
    list[indexC] = 20
```


##### 列表元素排序


- **sort()** [默认从小到大, reverse= false ]
- 参数： reverse=True 实现降序排列；
- 逆序： reverse() [ 实现列表的逆序 ]



```python
# 创建一个包含 10 个随机数的列表
import random
list = []
i = 0
while i < 10:
    randomNum =  random.randint(1, 100) # 1-100 的随机数
    list.append(randomNum)
    i += 1
    print(list)
    list.sort()
```


##### 两个列表元素追加


- **extend()**



```python
list1 = [1,2,3,4]
list2 = [10,20,30,40]

list1.extend(list2)
print(list1)  # [1,2,3,4,10,20,30,40]
```


### 元祖（Tuple）


**可以理解为列表，但是他的元素不可修改**


- 元组一旦创建不可修改
- 元组只有一个元素时，需要在尾部添加一个逗号
- 元组比列表更节省空间
- 元组是序列式容器支持索引、切片操作



```python
# 定义元组
tuple = (10,20,30,40)

# 只支持不能修改元素的方法
# 查询元素
- index
- count
# 遍历操作
- while
- for
```


### 字典（Dictionary）


```python
# 字典的定义，键是唯一的，值可以重复，不支持索引和切片
dict = {
    'name': 'serendipity',
    'gender': '女'
    'age' : '20',
}
```


##### 字典元素访问


```python
dict = {
    'name': 'serendipity',
    'gender': '女'
    'age' : '20',
}

## 获取值
1. print(dict['age'])   # 20 , 不存在会报错
2. 使用 get 方法
print(dict.get('age', '我是默认返回值'))  # 20 , 不存在返回 None , 可以指定默认返回值

## 添加和修改元素（如果 key 存在就是修改元素，不存在则添加元素）
dict['score'] = 99       # 添加元素
dict['name'] = '时光静好' # 修改元素
```


##### 字典元素删除


```python
person = {
    'name': 'serendipity',
    'gender': '女'
    'age' : '20',
}

## 删除元素(也适用于列表)
del  person['age']

## 清空字典
person.clear()

## 删除整个字典
del person
```


##### 字典的遍历


```python
person = {
    'name': 'serendipity',
    'gender': '女'
    'age' : '20',
}

for val in person:
    print(val)   # name,gender,age 默认只能遍历键

    # ***********************

    # 遍历字典的键
    personKeyList = person.keys()
    print(personKeyList)  # dict_keys 类型： dict_keys(['name', 'gender', 'age'])

    # 把 dict_keys 类型 转换 成列表类型
    print(list(personKeyList))  # ['name', 'gender', 'age']


    # 遍历字典的值
    personValList = person.values()
    print(personValList)  # dict_values 类型： dict_values(['serendipity', '女', '20'])

    # 把 dict_values 类型 转换 成列表类型
    print(list(personValList))  # ['serendipity', '女', '20']


    # 键值对遍历
    personKeyValList = person.items()
    print(personKeyValList)  # dict_items 类型： dict_items([('name': 'serendipity'),('gender': '女'), ('age' : '20')])

    # 把 dict_items 类型 转换 成列表类型
    print(list(personKeyValList))  # [('name': 'serendipity'),('gender': '女'), ('age' : '20')]


    keyValList = list(person.items())

    for value in keyValList:
        print(value)
        print('key:', value[0],'value:', value[1])


        i = 0
        while i < len(keyValList):
            print('key:', keyValList[i][0], 'value:', keyValList[i][1] )
            i += 1
```


### 集合（Set）


## Python 文件操作


### 文件的打开和关闭


- **open(文件名, 访问模式)** 打开文件 [ 参数： 文件名 ， 访问模式]
   - 访问模式： r 以只读方式打开文件（默认）
   - 访问模式： w 打开文件只用于写入
   - 访问模式： a 打开文件用于追加，文件存在，新的内容写入已有内容之后，文件不存在，创建新文件进行写入
   - 访问模式： rb 以二进制格式打开文件用于只读，文件指针放在开头
   - 访问模式： wb 以二进制格式打开文件用于写入，文件存在，将其覆盖，文件不存在，创建新文件进行写入
   - 访问模式： wb 以二进制格式打开文件用于追加，文件存在，新的内容写入已有内容之后，文件不存在，创建新文件进行写入
- **close()** 关闭文件



** pyCharm 文件编码: file encodings: GBK **


```python
#  写入文件
fileA= open('test.md', 'w') # 参数 文件名， 访问模式

content= "1. 时光静好，岁月安然 \n 一人之间，山水江湖"
fileA.write(content)

# 关闭文件
fileA.close()

# 读取文件
fileB= open('test.md', 'r')

content = fileB.read()
print(content)

fileB.close()
```


### 文件读写


- **write()**         一次只可以写一行
- **writelines()**  一次写入多行，以列表形式
- **read()**         没有参数读取文件所有数据，指定参数（1,2,3... ...）读取指定个数的数据
- **readline()**    一次读取一行
- **readlines()**   一次读取多行



```python
#  写入文件
fileA= open('test.md', 'w') # 参数 文件名， 访问模式

content= "1. 时光静好，岁月安然 \n 一人之间，山水江湖!"
fileA.write(content)

lines = ['时光静好，岁月安然.\n', '一人之间，山水江湖!\n']
fileA.writelines(lines)

# 关闭文件
fileA.close()

## 读取文件

fileB= open('test.md', 'r')

"""文件内容:

    时光静好，岁月安然.
    一人之间，山水江湖!
    """

content = fileB.read()
content1 = fileB.readline()
content2 = fileB.readline()

content4 = fileB.readlines()

print(content)  # 读取所有内容
print(content1) # 时光静好，岁月安然.
print(content2) # 一人之间，山水江湖!(因为第一行content1 已经读过，所以读取下一行内容)

print(content4) # ['时光静好，岁月安然.\n', '一人之间，山水江湖!\n']

# 按行读取
for line in content4:
    if line[-1] == '\n':
        print(line[:-1])
        else: 
            print(line)

            fileB.close()
```


### 文件拷贝


```python
# 获取要拷贝的文件名

old_fileName = input('请输入您要拷贝的文件名：')

# 读取拷贝文件内容

new_fileName = old_fileName + 'bk'

# 打开新的文件

file_old = open(old_fileName, 'rb')
file_new = open(new_fileName, 'wb') 

# 将老文件内容写入新文件

old_fileContent = file_old.read()
file_new.write(old_fileContent)

# 关闭文件

file_old.close()
file_new.close()
```


### 文件和目录操作


```python
import os

# 文件重命名
os.rename('test.md', 'hello.txt')

# 文件删除
os.remove('test.md') # 路径问题：写绝对路径

# 创建和删除目录
os.mkdir('abc')
os.rmdir('abc')

# 获取目录的文件列表
os.listdir('abc')

# 获取和设置工作目录
os.getCWD()  # CWD 默认当前文件路径
os.chdir('\Users\YII\Desktop\\') # 设置默认工作目录
```
