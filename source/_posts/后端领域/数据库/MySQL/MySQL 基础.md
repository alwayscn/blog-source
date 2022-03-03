---
title: MySQL 基础
comments: true
tags:
  - mysql
categories:
  - - 后端领域
    - 数据库
    - MySQL
abbrlink: 1206568676
date: 2020-08-02 00:00:00
---


## 数据库基本操作

> 关系型数据库： 以二维表存储数据

### 数据表操作

- 数据表的创建

```sql
-- unsigned: 无符号
-- primary key： 主键
-- auto_increment： 自动递增

create table demo (
    id int unsigned primary key auto_increment,
    name varchar(10),
    age int unsigned
)

```

- 数据表的删除

```sql

-- 删除掉 demo 表
drop table demo;

-- 如果数据库中存在demo表，就把它从数据库中drop掉。
drop table if exists demo;

-- 使用场景
drop table if exists demo;
create table demo (
    id int unsigned primary key auto_increment,
    name varchar(10),
    age int unsigned
)
```
### 数据操作

- 增
```sql
-- 单条添加
insert into demo values(null, "鲁班", 20);

-- 多条添加
insert into demo(name, age) values("鲁班大师", 50),("凯", 32),("安琪拉", 20), ... ...

```
- 删
```sql
-- 删除表中所有数据
delete from demo;

-- 按条件删除数据
delete from demo where name ="鲁班大师";  ==> 删除 name 是 鲁班大师的整条数据

```
- 改
```sql
update demo set name = "小乔", age = 20 where id = 10;

```
- 查
```sql

select * from demo;
select name, age from demo;

-- 条件查询
select name from demo where id = 1;

-- where 支持多种运算符
   - 比较运算符： =, >, <, >=, <=, !=
   - 逻辑运算符： and(且), or(或), not(非)
   - 模糊查询： like ==> %, _ 
     + where name like '孙%'
     + where name like '孙_'
     + where name like '%孙%'
     + where name like '_ _'
   - 范围查询 in('男', 女), between 18 and 20
   - 空判断： null , isnull


-- 设置别名
select name as 姓名, age as 年龄 from demo;

-- 数据表设置别名
select D.name, D.age from demo as D;

```
- 去掉字段中重复的数据
```sql
select distinct sex from student;

-- 去掉多个字段中重复的数据
select distinct sex, class from student;

```
- 排序
```sql
select * from student order by age;
-- 升序： order by age asc (默认)
-- 降序： order by age desc

-- 多次排序
select * from student order by age,id desc 先年龄正序，id降序

-- 中文排序
select * from student order by convert(name using gbk)
```

### 聚合函数

- count 统计
```sql
select count(*) from student;  ==> 只要有值就统计
       count(name)
```
- max 最大值
```sql
select max(age) from student;  
```
- min 最小值
```sql
select min(age) from student;  
```
- sum 求和
```sql
select sum(age) from student;  
```
- avg 平均值
```sql
select avg(age) from student;  
```
### 分组

- group by 根据某一字段排序，可以去重
```sql
-- 每个班级的平均，最大年龄
select class, avg(age), max(age) from student group by class;
```
### 连接查询

- 等值查询
```sql
select * from student as stu, score as sc where stu.sid = sc.sid;
```
- 内查询
```sql
select * from student as stu
inner join score as sc on stu.sid = sc.sid;
```
- 多表连接(两两之间产生条件)
```sql
select * from student as stu
inner join score as sc on stu.sid = sc.sid
inner join course as co on sc.cid = co.cid;
```
- 自关联（同一个表查询多次，自己产生关联，表必须起别名）
```sql
select * from areas as sheng
inner join areas as shi on sheng.pid = shi.pid
```
- 左连接（jion 前边的表）
```sql
select * from student as stu
left join score as sc on stu.sid = sc.sid;
```
- 右连接
```sql
select * from student as stu
right join score as sc on stu.sid = sc.sid;
```
- 子查询
```sql
-- 查询大于平均年龄的学生
select * from student whrer age > (select avg(age) from student);
```
- 数据分表
```sql
create table newStudent (
    id int unsigned primary key auto_increment,
    name varchar(10),
    age int unsigned
)
-- 查询的数据插入到另一个表中（查询出来的列必须对应表中的字段名，否则会新建）
insert into newStudent(id, name, age )  select id,name,age from student;

-- 创建并直接插入（查询出来的列必须对应表中的字段名，否则会新建）
create table newStudent (
    id int unsigned primary key auto_increment,
    Sname varchar(10)
) select name as Sname  from student;
```
### 索引（作用于某个字段）

**加索引后会使写入、修改、删除变慢，每一次增加数据平衡树都会重新排列，也会增加表的体积，占用磁盘存储空间。**
- 查看索引
```sql
    show index from 表名;
```
- 创建索引（创建索引后，表在磁盘上的存储结构就由整齐排列的结构转变成了树状结构，也就是「平衡树」结构）
```sql
-- 建表时创建索引 key (age)、primary key、unique
create table newStudent (
    id int unsigned primary key auto_increment,
    name varchar(10) unique
    age int unsigned,
    key (age)
)

-- 已经存在的表创建索引
create index 索引名称 on 表名(字段名(长度))
create index i_index on newStudent(name(10))

```