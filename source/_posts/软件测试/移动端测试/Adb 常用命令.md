---
title: adb 常用命令
date: 2020-7-13
comments: true
tags:
  - 软件测试
  - 移动端测试
  - adb
categories:
  - - 软件测试
    - 移动端测试
abbrlink: 2030954057
---
- 列出所有的连接设备

```
adb devices
```

- 拷⻉⽂件/⽬录到设备

```
 adb push E:/images/test.jpg /sdcard/
```

- 从设备拷⻉⽂件/⽬录

```
 adb pull /sdcard/images/test.jpg E:\tmp
```

- 浏览设备⽇志

```
 adb logcat
```

- 列出所有包名

```
 adb shell pm list packages
```

- 安装 apk ⽂件

```
 adb install [apk路径]

 覆盖安装： adb install -r [apk路径]

```

- 卸载 app

```
 adb uninstall com.xx.xx

 保留app数据：  adb uninstall -k com.xx.xx

```

- 查看 package name，启动应⽤后输⼊命令

```
 windows环境下: adb shell dumpsys activity | findstr "mFocusedActivity"

 Linux、Mac环境下： adb shell dumpsys activity | grep "mFocusedActivity"
```

- 截图

```
 adb shell screencap /sdcard/screen.png
```

- app 启动时间测试

```
 1. logcat⽅法，命令：

  adb shell logcat -v time |findstr ActivityManager
  取第⼀个activity的启动时间点，最后⼀个activity的展示完成的时间点，相减得到启动时间。（系统⻆度）

 2. 录屏⽅式

 ⼿⼯点击app到客户端启动，多次取平均值（⽤户⻆度）
```

**adb shell**

- adb shell 进⼊ Android 设备环境
- 设备基本信息：

```
 命令：cat /system/build.prop | grep "product"
```

```
1 ro.product.model          ⼿机代号也就是⼿机名
2 ro.product.brand          ⼿机品牌
3 ro.product.name           ⼿机正式名称
4 ro.product.device         ⼿机采⽤的设备
5 ro.product.board          ⼿机采⽤的处理器
6 ro.product.cpu.abi        cpu的版本
7 ro.product.cpu.abi2       cpu的品牌
8 ro.product.manufacturer   ⼿机制造商
9 o.product.locale.language ⼿机默认语⾔
10 ro.product.locale.region 地区语⾔
11 ro.build.product         建⽴产品
```

- 获取 cpu 信息

```
命令：cat /proc/cpuinfo
```

```
1 processor：     系统中逻辑处理核的编号。对于单核处理器，则课认为是其CPU编号，对于多核处理器则可以是物理核、或者使⽤超线程技术虚拟的逻辑核
2 vendor_id：     CPU制造商
3 cpu family：    CPU产品系列代号
4 model：         CPU属于其系列中的哪⼀代的代号
5 model name：    CPU属于的名字及其编号、标称主频
6 stepping ：     CPU属于制作更新版本
7 cpu MHz ：      CPU的实际使⽤主频
8 cache size ：   CPU⼆级缓存⼤⼩
9 physical id ：  单个CPU的标号
10 siblings ：    单个CPU逻辑物理核数
11 core id ：     当前物理核在其所处CPU中的编号，这个编号不⼀定连续
12 cpu cores ：   该逻辑核所处CPU的物理核数
13 apicid ：      ⽤来区分不同逻辑核的编号，系统中每个逻辑核的此编号必然不同，此编号不⼀定连续
14 fpu ：         是否具有浮点运算单元（Floating Point Unit）
15 fpu_exception ：是否⽀持浮点计算异常
16 cpuid level ：  执⾏cpuid指令前，eax寄存器中的值，根据不同的值cpuid指令会返回不同的内容
17 wp ：           表明当前CPU是否在内核态⽀持对⽤户空间的写保护（Write Protection）
18 flags ：        当前CPU⽀持的功能
19 bogomips ：     在系统内核启动时粗略测算的CPU速度（Million Instructions Per Second）
20 clflush size ： 每次刷新缓存的⼤⼩单位
21 cache_alignment：缓存地址对⻬单位
22 address sizes ： 可访问地址空间位数
```

- 获取设备内存

```
命令：cat /proc/meminfo
```

```
1 MemTotal:     所有可⽤RAM⼤⼩（即物理内存减去⼀些预留位和内核的⼆进制代码⼤⼩）
2 MemFree:      LowFree与HighFree的总和，被系统留着未使⽤的内存
3 Buffers:      ⽤来给⽂件做缓冲⼤⼩
4 Cached:       被⾼速缓冲存储器（cache memory）⽤的内存的⼤⼩（等于 diskcache minus SwapCache ）
5 SwapCached:   被⾼速缓冲存储器（cache memory）⽤的交换空间的⼤⼩，已经被交换出来的内存，但仍然被存放在swapfile中。⽤来在需要的时候很快的被替换⽽不需要再次打开
6 Active:       在活跃使⽤中的缓冲或⾼速缓冲存储器⻚⾯⽂件的⼤⼩，除⾮⾮常必要否则不会被移作他⽤
7 Inactive:     在不经常使⽤中的缓冲或⾼速缓冲存储器⻚⾯⽂件的⼤⼩，可能被⽤于其他途径.
8 HighTotal:
9 HighFree:     该区域不是直接映射到内核空间。内核必须使⽤不同的⼿法使⽤该段内存。
10 LowTotal:
11 LowFree:     低位可以达到⾼位内存⼀样的作⽤，⽽且它还能够被内核⽤来记录⼀些⾃⼰的数据结构。Among many
12 other things, it is where everything from the Slab is allocated
13 SwapTotal:   交换空间的总⼤⼩
14 SwapFree:    未被使⽤交换空间的⼤⼩
15 Dirty:       等待被写回到磁盘的内存⼤⼩。
16 Writeback:   正在被写回到磁盘的内存⼤⼩。
17 AnonPages：  未映射⻚的内存⼤⼩
18 Mapped:      设备和⽂件等映射的⼤⼩。
19 Slab:        内核数据结构缓存的⼤⼩，可以减少申请和释放内存带来的消耗。
20 SReclaimable:可收回Slab的⼤⼩
21 SUnreclaim： 不可收回Slab的⼤⼩（SUnreclaim+SReclaimable＝Slab）
22 PageTables： 管理内存分⻚⻚⾯的索引表的⼤⼩。
23 NFS_Unstable:不稳定⻚表的⼤⼩
24 VmallocTotal:可以vmalloc虚拟内存⼤⼩
25 VmallocUsed: 已经被使⽤的虚拟内存⼤⼩。
26 VmallocChunk: largest contigious block of vmalloc area which is free
```
