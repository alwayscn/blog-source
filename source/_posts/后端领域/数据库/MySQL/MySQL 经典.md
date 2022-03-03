---
title: MySQL 经典面试题
comments: true
tags:
  - mysql
categories:
  - - 后端领域
    - 数据库
    - MySQL
abbrlink: 4225305543
date: 2020-09-01 00:00:00
---

### 取得每个部门最高薪水的人员名称

```sql
-- 分析
-- 第一步： 求出每个部门最高的薪水
SELECT 
	e.deptno,MAX(e.sal) as maxsal
FROM emp e
GROUP BY 
	e.deptno;
-- 将以上查询结果当成一个临时表 t(deptno,maxsal)

-- 最高薪水的人员名称（两张表的连接）
SELECT 
	e.deptno,e.ename,t.maxsal,e.sal
FROM 
	(SELECT e.deptno,MAX(e.sal) AS maxsal 
     FROM emp e 
     GROUP BY e.deptno;) t
JOIN emp e ON t.deptno = e.deptno
WHERE t.maxsal = e.sal 
ORDER BY e.deptno;

```

### 那些人的薪水在部门的平均薪水之上

```sql
-- 分析 
-- 第一步，求出部门的平均薪水
SELECT 
	e.deptno, AVG(e.sal) AS avgsal
FROM 
	emp e
GROUP BY e.deptno; 
-- 将以上查询结果当成一个临时表 t(deptno,avgsal)

-- 薪水在部门的平均薪水之上的人员（两张表的连接）
SELECT e.deptno,e.ename,e.sal,t.avgsal 
FROM 
	(SELECT e.deptno, AVG(e.sal) AS avgsal 
	 FROM emp e 
     GROUP BY e.deptno;) t
JOIN emp e ON t.deptno = e.deptno
WHERE e.sal > t.avgsal
ORDER BY e.deptno;

```

