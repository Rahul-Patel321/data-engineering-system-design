# SQL Interview Guide

A collection of SQL interview questions with production-oriented answers for Data Engineer interviews.

---

# 1. What is the difference between WHERE and HAVING?

## Expected Answer

WHERE filters rows before aggregation.

HAVING filters records after aggregation.

Example

```sql
SELECT department,
       COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 5;
```

---

## Why Interviewer Asks

To verify your understanding of SQL execution order.

---

## Common Mistake

Using HAVING without GROUP BY when WHERE is sufficient.

---

## Production Perspective

Use WHERE whenever possible because it reduces the number of rows processed before aggregation.

---

# 2. Explain SQL Order of Execution.

## Expected Answer

```
FROM

↓

JOIN

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

DISTINCT

↓

ORDER BY

↓

LIMIT
```

---

## Why Interviewer Asks

Many SQL mistakes happen because developers confuse the logical order of execution.

---

# 3. Difference between ROW_NUMBER(), RANK() and DENSE_RANK()

## ROW_NUMBER()

Always assigns unique numbers.

```
1
2
3
4
```

---

## RANK()

Duplicate values receive the same rank.

```
1
2
2
4
```

---

## DENSE_RANK()

Duplicate values receive the same rank without gaps.

```
1
2
2
3
```

---

## Production Perspective

ROW_NUMBER() is commonly used for removing duplicates.

---

# 4. What are Window Functions?

Window functions perform calculations across a set of rows without collapsing them into a single row.

Common Functions

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LAG()
- LEAD()
- NTILE()
- SUM()
- AVG()

---

# 5. Explain CTE.

## Expected Answer

A Common Table Expression improves readability and allows complex queries to be broken into smaller logical steps.

Example

```sql
WITH sales AS
(
SELECT customer_id,
       SUM(amount) total_sales
FROM orders
GROUP BY customer_id
)

SELECT *
FROM sales
WHERE total_sales > 10000;
```

---

# 6. Difference between DELETE, TRUNCATE and DROP

| DELETE | TRUNCATE | DROP |
|----------|-----------|------|
| Removes rows | Removes all rows | Removes table |
| WHERE supported | No | No |
| Can Rollback* | Depends on DB | Depends on DB | Removes structure |

---

# 7. What are Indexes?

Indexes improve query performance by reducing full table scans.

Use indexes on:

- Primary Keys
- Foreign Keys
- Frequently filtered columns

Avoid indexing every column because indexes increase storage and slow INSERT/UPDATE operations.

---

# 8. Explain Joins

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN
- CROSS JOIN
- LEFT SEMI JOIN (Spark)
- LEFT ANTI JOIN (Spark)

Know when to use each one.

---

# 9. What is Normalization?

Normalization reduces redundancy.

Normal Forms

- 1NF
- 2NF
- 3NF
- BCNF

---

# 10. What is Denormalization?

Denormalization improves query performance by reducing joins.

Common in Data Warehouses.

---

# 11. What are Primary Keys?

Primary Key

- Unique
- Not Null

Foreign Key

- References another table

---

# 12. Explain Star Schema.

Fact Table

↓

Dimension Tables

Advantages

- Faster BI queries
- Easy reporting
- Simpler joins

---

# 13. Explain Snowflake Schema.

Dimensions are normalized.

Advantages

- Less redundancy

Disadvantages

- More joins

---

# 14. How do you remove duplicates?

Example

```sql
WITH cte AS
(
SELECT *,
ROW_NUMBER() OVER
(
PARTITION BY customer_id
ORDER BY updated_at DESC
) rn
FROM customers
)

SELECT *
FROM cte
WHERE rn = 1;
```

---

# 15. Difference between UNION and UNION ALL

UNION

- Removes duplicates
- Slower

UNION ALL

- Keeps duplicates
- Faster

Production systems generally prefer UNION ALL unless duplicate removal is required.

---

# 16. SQL Performance Optimization

Best Practices

- Avoid SELECT *
- Use WHERE
- Use indexes
- Avoid unnecessary DISTINCT
- Partition large tables
- Use proper JOIN conditions
- Filter early
- Analyze execution plans

---

# 17. Common SQL Questions

- Second highest salary
- Nth highest salary
- Duplicate records
- Running totals
- Consecutive records
- Gaps and islands
- Top N per group
- Latest record per customer
- Rolling averages

Practice solving these without memorizing solutions.

---

# 18. Production Tips

Good SQL Developers think about

- Readability
- Performance
- Scalability
- Maintainability

Not just correctness.

---

# Final Interview Advice

When answering SQL questions:

✅ Explain the logic.

✅ Mention performance considerations.

✅ Discuss trade-offs.

✅ Consider edge cases such as NULL values, duplicate rows, and large datasets.

Interviewers value structured reasoning as much as the final query.
