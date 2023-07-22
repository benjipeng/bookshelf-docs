# SQL Order of Operation

{{< hint info >}}
Understanding the order of operations and the logical processing order in SQL is crucial when constructing complex queries. It helps you predict how the query will be executed, avoid mistakes, and optimize performance.
{{< /hint >}}

## Order of Operations (Logical Processing Order)

The ***logical*** processing order follows:

1. *FROM* and *JOIN* clauses
2. *WHERE* clause
3. *GROUP BY* clause
4. *Aggregates* and window functions
5. *HAVING* clause
6. *SELECT* clause
7. *DISTINCT* keyword
8. *ORDER BY* clause
9. *LIMIT* and *OFFSET* clauses
10. `TOP`

| ***Lexical*** | ***Logical*** |
| :---: | :---: |
| *SELECT* | **FROM** |
| *DISTINCT* | **JOIN** |
| *TOP* | **WHERE** |
| [AGGREGATION] | **GROUP BY** |
| **FROM** | [AGGREGATION] |
| **JOIN** | HAVING |
| **WHERE** | *SELECT* |
| **GROUP BY** | *DISTINCT* |
| HAVING | ORDER BY |
| ORDER BY | *TOP / LIMIT* |

### Example 1

{{< columns >}}
```sql
SELECT City,
  Profit
FROM dbo.Orders
ORDER BY Profit DESC;
```
<--->
| **Lexical** | **Logical** |
| :---: | :---: |
| SELECT | FROM |
| FROM | SELECT |
| ORDER BY | ORDER BY |

{{< /columns >}}

### Example 2

{{< columns >}}
```sql
SELECT o.City,
  AVG(o.Profit) AS Average_Profit
FROM Orders AS o
JOIN(
  SELECT TOP(3) City,
    SUM(Profit) AS Total_Profit
  FROM dbo.Orders
  GROUP BY City
  ORDER BY Total_Profit DESC
  ) AS sub
  ON o.City = sub.City
GROUP BY o.City
ORDER BY o.City,
  Average_Profit;
```

<--->

| **Lexical** | **Logical** |
| :---:        | :---:       |
| SELECT | FROM |
| FROM | JOIN -> INNER |
| JOIN | GROUP BY |
| GROUP BY | [Aggregate] |
| ORDER BY | SELECT |
|         | ORDER BY |

{{< /columns >}}