---
layout: post
title: LeetCode - Department Highest Salary
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.
```
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
```
The Department table holds all departments of the company.
```
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```
Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, Max has the highest salary in the IT department and Henry has the highest salary in the Sales department.
```
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+
```
<!--more-->
### Sql Solution
```mysql
select d.Name as Department, e.Name as Employee, e.Salary from Employee as e, Department as d, (select DepartmentId, Max(Salary) as Salary from Employee group by DepartmentId) as s where s.Salary = e.Salary and s.DepartmentId = e.DepartmentId and e.DepartmentId = d.Id
```