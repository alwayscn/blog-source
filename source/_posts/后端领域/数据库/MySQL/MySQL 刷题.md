---
title: MySQL 刷题记录
comments: true
tags:
  - mysql
  - leetcode
  - 牛客
categories:
  - - 后端领域
    - 数据库
    - MySQL
abbrlink: 2689587330
date: 2020-10-13 00:00:00
---


## [组合两个表](https://leetcode-cn.com/problems/combine-two-tables/)

表1: Person

```
+-------------+---------+
| 列名         | 类型     |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId 是上表主键
```

表2: Address

```
+-------------+---------+
| 列名         | 类型    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId 是上表主键
```


编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：

```
FirstName, LastName, City, State
```

**[ 解题 ]**

```mysql
select FirstName, LastName, City, State from Person
left join Address on Address.PersonId = Person.PersonId;

-- left join Address using(PersonId)
```

## [ 第二高的薪水](https://leetcode-cn.com/problems/second-highest-salary/)

编写一个 SQL 查询，获取 Employee 表中第二高的薪水（Salary） 。

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

例如上述 Employee 表，SQL查询应该返回 200 作为第二高的薪水。如果不存在第二高的薪水，那么查询应返回 null。

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

**[ 解题 ]**

```mysql
# Write your MySQL query statement below

# 方法一
select MAX(Salary) as SecondHighestSalary from Employee WHERE Salary < (select max(Salary) from Employee)；

# 方法二

-- SELECT
--     IFNULL(
--       (SELECT DISTINCT Salary
--        FROM Employee
--        ORDER BY Salary DESC
--         LIMIT 1 OFFSET 1),
--     NULL) AS SecondHighestSalary；
```

## [超过经理收入的员工](https://leetcode-cn.com/problems/employees-earning-more-than-their-managers/)

Employee 表包含所有员工，他们的经理也属于员工。每个员工都有一个 Id，此外还有一列对应员工的经理的 Id。

```
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
```

给定 Employee 表，编写一个 SQL 查询，该查询可以获取收入超过他们经理的员工的姓名。在上面的表格中，Joe 是唯一一个收入超过他的经理的员工。

```
+----------+
| Employee |
+----------+
| Joe      |
+----------+
```

**[ 解题 ]**

```mysql
# Write your MySQL query statement below

select A.Name as Employee  from Employee AS A,Employee AS B 
WHERE A.ManagerId = B.Id And A.Salary > B.Salary;
```

## [查找重复的电子邮箱](https://leetcode-cn.com/problems/duplicate-emails/)

编写一个 SQL 查询，查找 Person 表中所有重复的电子邮箱。

```
示例：

+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

根据以上输入，你的查询应返回以下结果：

```

+---------+
| Email   |
+---------+
| a@b.com |
+---------+
说明：所有电子邮箱都是小写字母。
```

**[ 解题 ]**

```mysql
# Write your MySQL query statement below

-- select Email, count(*) as Num  from Person group by Email;

-- select Email from t where Num >1

select Email from (select Email, count(*) as Num  from Person group by Email) t where t.Num > 1;
```

## [从不订购的客户](https://leetcode-cn.com/problems/customers-who-never-order/)

某网站包含两个表，Customers 表和 Orders 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户。

Customers 表：

```
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
```

Orders 表：

```
+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```

例如给定上述表格，你的查询应返回：

```
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```

**[ 解题 ]**

```mysql
# Write your MySQL query statement below

-- select Name as Customers from Customers Where Id not in (select Orders.CustomerId from Orders );

select c.Name as Customers from Customers c

left join Orders o on c.Id = O.CustomerId
Where o.CustomerId is null;

```












## 模板

表1: Person

```

```

表2: Address

```

```

编写一个 SQL 查询

```
FirstName, LastName, City, State
```

**[ 解题 ]**

```mysql

```



## 模板

表1: Person

```

```

表2: Address

```

```

编写一个 SQL 查询

```
FirstName, LastName, City, State
```

**[ 解题 ]**

```mysql

```





## 模板

表1: Person

```

```

表2: Address

```

```

编写一个 SQL 查询

```
FirstName, LastName, City, State
```

**[ 解题 ]**

```mysql

```





