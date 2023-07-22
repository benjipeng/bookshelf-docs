---
bookCollapseSection: true
weight: 20
---

# Structured Query Language (SQL)

{{< hint warning >}}
**Structured Query Language (SQL)** is a programming language designed for managing data in *relational databases*. It enables users to `create`, `read`, `update`, and `delete` data, as well as define the structure and constraints of database tables. SQL is essential for ***data analysis***, ***reporting***, and ***manipulation***, making it a critical skill for database administrators, data analysts, and software developers.
{{< /hint >}}

The basic SQL syntax includes clauses such as `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `ORDER BY`, and `JOIN`.

## 1. `JOIN`

> `Syntax`: `SELECT` column1, column2, ... `FROM` table1 `[INNER|LEFT|RIGHT|FULL OUTER]` `JOIN` table2 `ON` table1.column = table2.column;
>
`JOIN` is used to combine data from two or more tables based on a *related* column. There are several types of joins, including `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`. We'll discuss each type and provide examples with detailed explanations.
{{< hint info >}}
Consider two tables, `employees` and `departments`:
{{< /hint >}}

***employees***
| id | first_name | last_name | department_id |
| :---: | :---: | :---: | :---: |
| 1 | John | Doe | 1 |
| 2 | Jane | Smith | 2 |
| 3 | Alice | Johnson | 2 |

***departments***

| id | name |
| :---: | :---: |
| 1 | HR |
| 2 | IT |
| 3 | Finance |

### 1.1 `INNER JOIN`

```sql
SELECT e.first_name, e. last_name, d.name
FROM employees e
INNER JOIN department d ON e.department_id = d.id;
```

In this query, we first specify the columns we want to retrieve: `e.first_name`, `e.last_name`, and `d.name`. We then specify the tables we're joining, using aliases `e` for employees and `d` for departments. Finally, we provide the `JOIN` condition: `e.department_id = d.id`.

Result:

|first_name |last_name |name|
| :---: | :---: | :---: |
|John |Doe| HR|
|Jane |Smith| IT|
|Alice |Johnson| IT|

### 1.2 `LEFT JOIN`

A `LEFT JOIN` returns ***all*** rows from the `left` table (`employees` in our example) and the *matched rows* from the `right` table (`departments`). If no match is found, `NULL` values will be returned for *right* table columns.

```sql
SELECT e.first_name, e. last_name, d.name
FROM employees e
LEFT JOIN department d ON e.department_id = d.id;
```

Result is the same as the `INNER JOIN`.

### 1.3 `RIGHT JOIN`

A `RIGHT JOIN` returns ***all*** rows from the `right` table (`departments`) and the *matched rows* from the left table (`employees`). If no match is found, `NULL` values will be returned for *left* table columns.
