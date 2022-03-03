---
title: shell 编程
tags:
  - shell
categories:
  - - 后端领域
    - 编程语言
    - shell
comments: true
abbrlink: 4046588353
date: 2021-11-02 00:00:00
---


## shell 实例


- echo 用于向窗口输出文本
```shell
#!/bin/bash

echo "时光静好，岁月安然！"
```

- 脚本运行
```shell
$ ./test.sh

$  sh test.sh
```


## 变量

[ **变量名的命名规则** ]

1. 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头
1. 中间不能有空格，可以使用下划线（_）
1. 不能使用标点符号
1. 不能使用bash里的关键字（可用help命令查看保留关键字）



- **变量赋值**
```shell
#!/bin/bash

string="从前冬天冷呀 夏天雨呀水呀 秋天远处传来你声音暖呀暖呀"

# 使用变量
echo ${string}

# 语句给变量赋值 (将 /etc 下目录的文件名循环出来。将文件名 赋值给 file)
for file in `ls /etc` 或 for file in $(ls /etc)
	do 
	echo "文件： ${file}"
	done
```

- **只读变量( readonly  )**
```shell
#!/bin/bash

# 只读变量( readonly  )
base_url="www.baidu.com"
readonly base_url
base_url="www.google.com"

# 运行脚本，结果如下：
	/bin/bash: NAME: This variable is read only.
```

- **删除变量（unset ）**
```shell
#!/bin/bash

variable_name="System"
unset variable_name

echo ${variable_name}  # 没有任何输出
```

- **变量类型**
```shell
1) 局部变量: 局部变量在脚本或命令中定义，仅在当前 shell 实例中有效，其他 shell 启动的程序不能访问局部变量。

2) 环境变量: 所有的程序，包括 shell 启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候 shell 脚本也可以定义环境变量。

3) shell 变量: shell 变量是由 shell 程序设置的特殊变量。shell 变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了 shell 的正常运行
```


## 字符串


- 字符串可以用单引号，也可以用双引号，也可以不用引号
```shell
#!/bin/bash

# 单引号
str='this is a string'
单引号字符串的限制：
	单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
	单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。
	
# 双引号
_name='system'
str="Hello, I know you are \"${_name}\"! \n"
echo -e ${str}

# 输出结果为：
	Hello, I know you are "runoob"! 

双引号的优点：
	双引号里可以有变量
	双引号里可以出现转义字符
```

- **字符串拼接**
```shell
#!/bin/bash

_name="system"
# 使用双引号拼接
greeting="hello, "$_name" !"  	# 双引号拼接
greeting_1="hello, ${_name} !"	# 双引号存在变量
echo $greeting  $greeting_1

# 使用单引号拼接
greeting_2='hello, '$_name' !'  # 单引号拼接
greeting_3='hello, ${_name} !'  # 单引号字符串中存在变量
echo $greeting_2  $greeting_3

# 输出结果
hello, system ! hello, system !
hello, system ! hello, ${_name} !   # 单引号字符串中存在变量，原样输出
```

- **获取字符串长度**
```shell
#!/bin/sh
string="abcd"
echo ${#string} #输出 4
```


- **提取字符串**
```shell
#!/bin/sh
string="从前冬天冷呀 夏天雨呀水呀 秋天远处传来你声音暖呀暖呀"

echo ${string:0:6}  # 输出 从前冬天冷呀(包含 0, 但不包含 6)  第一个字符的索引值为 0

注意： 
  1. 不支持负数切片
  2. 如果后一个数小于开始的数字，则该值表示向后延伸长度（如：${string:7:3} >> 夏天雨）
  3. 如果后一个数大于开始的数字，则该值表示向后延伸位置（如：${string:3:7} >> 天冷呀 夏天雨）
```

- **查找字符串**
```shell
#!/bin/sh
string="从前冬天冷呀 夏天雨呀水呀 秋天远处传来你声音暖呀暖呀"

# 查找字符 i 或 o 的位置(哪个字母先出现就计算哪个)：

echo `expr index "$string" 呀秋` # 输出 6（从 1 开始 ）
```


## shell 数组


- **定义数组**

    在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为
```shell
# 数组名=(值1 值2 ... 值n)

array=(0 1 2 3 n)

# 可以单独定义数组的各个分量：
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen  # 可以不使用连续的下标，而且下标的范围没有限制
```

- **读取数组**
```shell
#!/bin/bash
array=(0 1 2 3 "时光" "静好" (value0 value1 value2 value3) )

echo ${array[0]}

# 使用 @ 或 * 符号可以获取数组中的所有元素
echo ${array[@]} # 输出： 0 1 2 3 时光 静好
```

- **获取数组的长度**
```shell
#!/bin/bash
array=(0 1 2 3 "时光" "静好" )

# 取得数组元素的个数 
length=${#array[@]}
# 或者
length=${#array[*]}
echo ${length} # 6

# 取得数组单个元素的长度
lengthn=${#array_name[n]}

lengthn=${#array_name[4]}
echo ${lengthn} # 2
```


## shell 注释


- 以 **#** 开头的行就是注释，会被解释器忽略
```shell
#!/bin/bash

#--------------------------------------------
# 这是一个注释
# author：
# site：
# slogan：
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
# 
#
##### 用户配置区 结束  #####
```

- **多行注释**
```shell
#!/bin/bash

:<<EOF
注释内容...
注释内容...
注释内容... 
EOF

# EOF 也可以使用其他符号:

:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```

## shell 传递参数


> 在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n**。**n** 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……



- 实例
```shell
#!/bin/bash
# file_name = test.sh
# 以下实例我们向脚本传递三个参数，并分别输出，其中 $0 为执行的文件名（包含文件路径）

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";

# 执行脚本
sh test.sh 1 2 3
    Shell 传递参数实例！
    执行的文件名：test.sh
    第一个参数为：1
    第二个参数为：2
    第三个参数为：3
    
./test.sh 3 2 1
    Shell 传递参数实例！
    执行的文件名：./test.sh
    第一个参数为：3
    第二个参数为：2
    第三个参数为：1
```
| 参数处理 | 说明 |
| :--- | :--- |
| $# | 传递到脚本的参数个数 |
| $* | 以一个单字符串显示所有向脚本传递的参数。 如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 |
| $$ | 脚本运行的当前进程 ID 号 |
| $! | 后台运行的最后一个进程的 ID号 |
| $@ | 与 $$* 相同，但是使用时加引号，并在引号中返回每个参数。 如"$$@"用「"」括起来的情况、以"$1" "$$2" … "$$n" 的形式输出所有参数。 |
| $- | 显示Shell使用的当前选项，与 [set命令](https://www.runoob.com/linux/linux-comm-set.html) 功能相同。 |
| $? | 显示最后命令的退出状态。0 表示没有错误，其他任何值表明有错误。 |

- **$_ 与 $@ 区别_
```tex
相同点：都是引用所有参数。
不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。
```

## shell 运算符


> shell 运算符包括 算术运算符、关系运算符、布尔运算符、字符串运算符、文件测试运算符
> 原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。
> expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

- 实例
```shell
#!/bin/bash

val=`expr 5 + 5`

# 等价于  
val=$[a+b]

echo ${val} # 10
```

   - 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
   - 完整的表达式要被 ”``“ 包含
- **算术运算符**
```shell
#!/bin/bash
#  + 、- 、* 、 / 、= 、% 、 == 、 ！=      
# 注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。

a=50
b=27

result=`expr $a + $b`
echo "a + b : ${result}"

result=`expr ${a} - ${b}`
echo "a - b : ${result}"

# 乘号(*)前边必须加反斜杠(\)才能实现乘法运算
# 在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 "*" 不需要转义符号 "\" 
result=`expr $a \* $b`
echo "a * b : ${result}"

result=`expr $a / $b`
echo "a / b : ${result}"

result=`expr $a % $b`
echo "a % b : ${result}"

# 注意空格 [ $a == $b ] 
if [ $a == $b ] 
then 
  echo " a 等于 b"
fi

if [ $a != $b ] 
then
  echo "a 不等于 b"
fi

```

- **关系运算符**
> 关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

| 运算符 | 说明（假定变量 a 为 10，变量 b 为 20） | 举例 |
| :--- | :--- | :--- |
| -eq | 检测两个数是否相等，相等返回 true。 | [ $a -eq $b ] 返回 false。 |
| -ne | 检测两个数是否不相等，不相等返回 true。 | [ $a -ne $b ] 返回 true。 |
| -gt | 检测左边的数是否大于右边的，如果是，则返回 true。 | [ $a -gt $b ] 返回 false。 |
| -lt | 检测左边的数是否小于右边的，如果是，则返回 true。 | [ $a -lt $b ] 返回 true。 |
| -ge | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | [ $a -ge $b ] 返回 false。 |
| -le | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | [ $a -le $b ] 返回 true。 |

```shell
#!/bin/bash

a=50
b=20

# -eq
if [ $a -eq $b ]
then 
  echo "-eq : a 等于 b"
else 
  echo "-eq : a 不等于 b"
fi
```

- **布尔运算符**
| 运算符 | 说明（假定变量 a 为 10，变量 b 为 20） | 举例 |
| :--- | :--- | :--- |
| ! | 非运算，表达式为 true 则返回 false，否则返回 true。 | [ ! false ] 返回 true。 |
| -o | 或运算，有一个表达式为 true 则返回 true。 | [ $a -lt 20 -o $b -gt 100 ] 返回 true。 |
| -a | 与运算，两个表达式都为 true 才返回 true。 | [ $a -lt 20 -a $b -gt 100 ] 返回 false。 |

```shell
#!/bin/bash

a=50
b=20

if [ $a != $b ]
then 
  echo "a 不等于 b， 返回 true"
else 
  echo " a 等于 b"
fi

if [ $a -gt 100 -o $b -lt 50 ]
then
  echo "a 大于 100或 b小于50 满足一个条件成立 "
fi

if [ $a -gt 100 -a $b -lt 50 ]
then
  echo "a 大于 100 与 b小于50 返回 false "
else 
  echo "条件不成立， 必须同时满足， a 大于 100， b 小于 50"
```

- **逻辑运算符**
| 运算符 | 说明（假定变量 a 为 10，变量 b 为 20） | 举例 |
| :--- | :--- | :--- |
| && | 逻辑的 AND | [[ $a -lt 100 && $b -gt 100 ]] 返回 false |
| &#124;&#124; | 逻辑的 OR | [[ $a -lt 100 &#124;&#124; $b -gt 100 ]] 返回 true |

```shell
#!/bin/bash

a=10
b=20

if [[ $a -gt 100 || $b -lt 50 ]]
then
  echo "a 大于 100 或 b 小于 50 条件成立 返回 true"
else 
  echo "a 大于 100 或 b 小于 50 条件不成立 返回 false"
fi

if [[ $a -gt 100 && $b -lt 50 ]]
then
  echo "a 大于 100 与 b小于50 返回 true "
else 
  echo "条件不成立, false， 必须同时满足， a 大于 100， b 小于 50"
fi
```

- **字符串运算符**
| 运算符 | 说明（假定变量 a 为 "abc"，变量 b 为 "efg"） | 举例 |
| :--- | :--- | :--- |
| = | 检测两个字符串是否相等，相等返回 true。 | [ $a = $b ] 返回 false。 |
| != | 检测两个字符串是否相等，不相等返回 true。 | [ $a != $b ] 返回 true。 |
| -z | 检测字符串长度是否为0，为0返回 true。 | [ -z $a ] 返回 false。 |
| -n | 检测字符串长度是否不为 0，不为 0 返回 true。 | [ -n "$a" ] 返回 true。 |
| $ | 检测字符串是否为空，不为空返回 true。 | [ $a ] 返回 true。 |

- **文件测试运算符**
> 文件测试运算符用于检测 Unix 文件的各种属性。

| 操作符 | 说明 | 举例 |
| :--- | :--- | :--- |
| -b file | 检测文件是否是块设备文件，如果是，则返回 true。 | [ -b $file ] 返回 false。 |
| -c file | 检测文件是否是字符设备文件，如果是，则返回 true。 | [ -c $file ] 返回 false。 |
| -d file | 检测文件是否是目录，如果是，则返回 true。 | [ -d $file ] 返回 false。 |
| -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | [ -f $file ] 返回 true。 |
| -g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。 | [ -g $file ] 返回 false。 |
| -k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。 | [ -k $file ] 返回 false。 |
| -p file | 检测文件是否是有名管道，如果是，则返回 true。 | [ -p $file ] 返回 false。 |
| -u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。 | [ -u $file ] 返回 false。 |
| -r file | 检测文件是否可读，如果是，则返回 true。 | [ -r $file ] 返回 true。 |
| -w file | 检测文件是否可写，如果是，则返回 true。 | [ -w $file ] 返回 true。 |
| -x file | 检测文件是否可执行，如果是，则返回 true。 | [ -x $file ] 返回 true。 |
| -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。 | [ -s $file ] 返回 true。 |
| -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。 | [ -e $file ] 返回 true。 |

- 其他检查符：
   - **-S**: 判断某文件是否 socket。
   - **-L**: 检测文件是否存在并且是一个符号链接。
```shell
#!/bin/bash

file="/tmp/exlog/test.sh"

if [ -d $file ]
then
   echo "文件是个目录"
else
   echo "文件不是个目录"
fi
if [ -r $file ]
then
   echo "文件可读"
else
   echo "文件不可读"
fi
if [ -w $file ]
then
   echo "文件可写"
else
   echo "文件不可写"
fi
if [ -x $file ]
then
   echo "文件可执行"
else
   echo "文件不可执行"
fi
```



## shell 输出


#### echo命令


```shell
#!/bin/bash

echo "It is a test" / echo It is a test

### 显示转义字符
echo "\"It is a test\""

### 显示变量

# read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量
printf "请输入变量： "
read name 
echo "$name It is a test"

# 保存为 main.sh 文件 执行
[root@localhost exlog]# sh main.sh 
请输入变量：qwe
qwe It is a test 

### 显示换行
echo -e "OK! \n" # -e 开启转义
echo "It is a test"
# 输出结果：
OK!

It is a test

### 显示不换行
echo -e "OK! \c" # -e 开启转义 \c 不换行
echo "It is a test"
# 输出结果：
OK! It is a test

### 显示结果定向至文件
printf "请输入变量： "
read name 
echo "$name It is a test" > test.sh

# 保存为 main.sh 文件 执行, cat test.sh

### 原样输出字符串，不进行转义或取变量(用单引号)

echo '$name\"'  

# 输入结果  $name\"

### 显示命令执行结果 注意： 这里使用的是反引号 `, 而不是单引号 '
echo `date`

# Thu Jul 24 10:08:46 CST 2014
```


#### printf 命令


> printf 使用引用文本或空格分隔的参数，外面可以在 printf 中使用格式化字符串，还可以制定字符串的宽度、左右对齐方式等。
> 默认 printf 不会像 echo 自动添加换行符，我们可以手动添加 \n



```shell
#!/bin/bash
echo "Hello, Shell"
printf "Hello, Shell\n"

printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876

# 输出结果
    姓名     性别   体重kg
    郭靖     男      66.12
    杨过     男      48.65
    郭芙     女      47.99
```

**%s %c %d %f** 都是格式替代符，**％s** 输出一个字符串，**％d** 整型输出，**％c** 输出一个字符，**％f** 输出实数，以小数形式输出。
**%-10s** 指一个宽度为 10 个字符（**-** 表示左对齐，没有则表示右对齐），任何字符都会被显示在 10字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
**%-4.2f** 指格式化为小数，其中 **.2** 指保留2位小数。

## Shell 输入/输出重定向
| 命令 | 说明 |
| :--- | :--- |
| command > file | 将输出重定向到 file。 |
| command < file | 将输入重定向到 file。 |
| command >> file | 将输出以追加的方式重定向到 file。 |
| n > file | 将文件描述符为 n 的文件重定向到 file。 |
| n >> file | 将文件描述符为 n 的文件以追加的方式重定向到 file。 |
| n >& m | 将输出文件 m 和 n 合并。 |
| n <& m | 将输入文件 m 和 n 合并。 |
| << tag | 将开始标记 tag 和结束标记 tag 之间的内容作为输入。 |



> _需要注意的是文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。_



## shell 流程控制


### if 控制语句


```shell
#!/bin/bash

a=10
b=20
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi
```


### for 循环


```shell
#!/bin/bash

for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done

# 序输出字符串中的字符
for str in This is a string
do
    echo $str
done
# 输出结果
    This
    is
    a
    string

# 通常情况下 shell 变量调用需要加 $,但是 for 的 (()) 中不需要
for((i=1;i<=5;i++));do
    echo "这是第 $i 次调用";
done;
```


### while 语句


```shell
#!/bin/bash
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```


> 以上实例使用了 Bash let 命令，它用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量



### 无限循环


```shell
#!/bin/bash
while true
do
  printf "请输入内容："
  read content
  echo "您输入额内容是 ${content}"
done

# 或者

while ：
do
  printf "请输入内容："
  read content
  echo "您输入额内容是 ${content}"
done

#或者

for (( ; ; ))
do
  printf "请输入内容："
  read content
  echo "您输入额内容是 ${content}"
done
```


### until 循环


> until 循环执行一系列命令直至条件为 true 时停止。
> until 循环与 while 循环在处理方式上刚好相反。
> 一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。



```shell
#!/bin/bash

a=0

until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```


### case ... esac


> **case ... esac** 为多选择语句,是一种多分枝选择结构，每个 case 分支用右圆括号开始，用两个分号 **;;** 表示 break，即执行结束，跳出整个 case ... esac 语句，esac（就是 case 反过来）作为结束标记。
> 可以用 case 语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。



```shell

echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```


### 跳出循环


- **break**
> break 命令允许跳出所有循环（终止执行后面的所有循环）

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

- **continue**
> continue 命令与 break 命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done
```


## Shell 函数


```shell
#!/bin/bash

# shell 函数定义

[ function ] funname [()]

{

    action;

    [return int;]

}
```


> - 1、可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
> - 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)



- **实例**
```shell
#!/bin/bash

function demo (){
  echo "这是一个 shell 函数！"
}

echo "----- 函数开始执行 -----"

demo()

echo "----- 函数执行完毕 -----"

# 函数 return 

function demo_return(){
  a=10
  b=20
  return $((a + b))
  # return $(($a + $b))
  # return $[a + b]
}

demo_return
echo "和：$?"
```
> 函数返回值在调用该函数后通过 $? 来获得。
> 注意：所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可

- **函数参数**
> 在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数...
> 注意，$$10 不能获取第十个参数，获取第十个参数需要$${10}。当n>=10时，需要使用${n}来获取参数。

| 参数处理 | 说明 |
| :--- | :--- |
| $# | 传递到脚本或函数的参数个数 |
| $* | 以一个单字符串显示所有向脚本传递的参数 |
| $$ | 脚本运行的当前进程ID号 |
| $! | 后台运行的最后一个进程的ID号 |
| $@ | 与$*相同，但是使用时加引号，并在引号中返回每个参数。 |
| $- | 显示Shell使用的当前选项，与set命令功能相同。 |
| $? | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

```shell
#!/bin/bash

funWithParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
    echo "脚本运行的当前进程ID号: $$"
    echo "后台运行的最后一个进程的ID号:$!"
    echo "$-"
    echo "$?"
    
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73
```

- **注意点**



```shell
#!/bin/bash
function demoFun1(){
    echo "这是我的第一个 shell 函数!"
    return `expr 1 + 1`
}

demoFun1
echo $?

function demoFun2(){
 echo "这是我的第二个 shell 函数!"
 expr 1 + 1
}

demoFun2
echo $?
demoFun1
echo 在这里插入命令！
echo $?  # 显示 上一条 echo 在这里插入命令！ 的结果，0表示没有错误，其他任何值表明有错误。

# 输出结果

这是我的第一个 shell 函数!
2
这是我的第二个 shell 函数!
2
0
这是我的第一个 shell 函数!
在这里插入命令！
0
```


> 调用 demoFun2 后，函数最后一条命令 expr 1 + 1 得到的返回值（$?值）为 0，意思是这个命令没有出错。所有的命令的返回值仅表示其是否出错，而不会有其他有含义的结果。
> 第二次调用 demoFun1 后，没有立即查看 $? 的值，而是先插入了一条别的 echo 命令，最后再查看 $? 的值得到的是 0，也就是上一条 echo 命令的结果，而 demoFun1 的返回值被覆盖了。
> 下面这个测试，连续使用两次 **echo $?**，得到的结果不同，更为直观：



```shell
#!/bin/bash

function demoFun1(){
    echo "这是我的第一个 shell 函数!"
    return `expr 1 + 1`
}

demoFun1
echo $?
echo $?   # 显示 上一条 echo $? 的结果，0表示没有错误，其他任何值表明有错误。

# 输出结果

这是我的第一个 shell 函数!
2
0
```
