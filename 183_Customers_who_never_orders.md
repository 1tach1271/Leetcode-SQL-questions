# 183. Customers Who Never Order
## Contents
- [Schema](#sql-schema)
- [Problem Statement](#problem-statement)
- [Code](#code-)

### Question Link:
https://leetcode.com/problems/customers-who-never-order/?envType=problem-list-v2&envId=m8baczxh


## SQL Schema

### Table: Customers

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

- `id` is the primary key (column with unique values) for this table.
- Each row of this table indicates the ID and name of a customer.
 

### Table: Orders


| Column Name | Type |
|-------------|------|
| id          | int  |
| customerId  | int  |

- `id` is the primary key (column with unique values) for this table.
- `customerId` is a foreign key (reference columns) of the ID from the Customers table.
- Each row of this table indicates the ID of an order and the ID of the customer who ordered it.
 
## Problem Statement
- Write a solution to find all customers who never order anything.

- Return the result table in any order.

- The result format is in the following example.

 

## Example 1:

### Input: 
**Customers table:** 

| id | name  |
|----|-------|
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |

**Orders table:**

| id | customerId |
|----|------------|
| 1  | 3          |
| 2  | 1          |

**Output:** 

| Customers |
|-----------|
| Henry     |
| Max       |

## Code-
```sql
select a.name as Customers
from Customers a
left join Orders b
on a.id = b.customerId
where b.customerId is NULL;
```
