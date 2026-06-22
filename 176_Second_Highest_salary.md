# 176. Second Highest Salary
## Content
- [SQL Schema](#sql-schema)
- [Problem Statement](#problem-statement)
- [Code](#code-)

### Question Link:
https://leetcode.com/problems/second-highest-salary/?envType=problem-list-v2&envId=m8baczxh

## SQL Schema
### Table: Employee

| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

- `id` is the primary key (column with unique values) for this table.
- Each row of this table contains information about the salary of an employee.
 
## Problem Statement

Write a solution to find the **second highest distinct salary** from the `Employee` table. If there is no second highest salary, return null (return None in Pandas).

The result format is in the following example.

---

## Example 1:

### Input: 
**Employee table:**
| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |


Output: 
| SecondHighestSalary |
|---------------------|
| 200                 |
## Example 2:

### Input: 

**Employee table:**

| id | salary |
|----|--------|
| 1  | 100    |

### Output: 

| SecondHighestSalary |
|---------------------|
| null                |

# Code:-
```SQL
SELECT max(salary) as SecondHighestSalary
FROM Employee 
where salary<(select max(salary) from  Employee);
```
