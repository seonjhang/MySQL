# 🪟 Window Functions in MySQL

Window functions allow you to perform calculations **across a set of rows that are related to the current row**, while still preserving individual rows in the result.

---

## 📘 What Is a Window Function?

Unlike aggregate functions (`SUM()`, `AVG()`, etc.) that collapse multiple rows into one, **window functions return a value for each row**.

**Syntax:**
```sql
<function>() OVER (
    PARTITION BY column
    ORDER BY column
    [ROWS BETWEEN ...]
)
```

---

## 🔑 Key Clauses

- `PARTITION BY`: Divides result set into partitions (like groups)
- `ORDER BY`: Orders rows within each partition
- `ROWS BETWEEN`: Defines the window frame (optional)

---

## 🧱 Common Window Functions in MySQL

| Category       | Function          | Description                                      |
|----------------|-------------------|--------------------------------------------------|
| Ranking        | `ROW_NUMBER()`     | Assigns unique row numbers                       |
|                | `RANK()`           | Rank with gaps                                   |
|                | `DENSE_RANK()`     | Rank without gaps                                |
| Aggregates     | `SUM()`, `AVG()`   | Running totals, moving averages                  |
| Value Access   | `LAG()`            | Previous row's value                             |
|                | `LEAD()`           | Next row's value                                 |
|                | `FIRST_VALUE()`    | First value in partition                         |
|                | `LAST_VALUE()`     | Last value in partition                          |
| Distribution   | `NTILE(n)`         | Distributes rows into n buckets                  |
|                | `PERCENT_RANK()`   | Percent rank (0 to 1 scale)                      |
|                | `CUME_DIST()`      | Cumulative distribution                          |

---

## 🧪 Example: `ROW_NUMBER()`

```sql
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM Employees;
```

- Ranks employees by salary **within each department**
- `PARTITION BY` resets the ranking for each department

---

## 💡 Notes

- **MySQL 8.0+ only**
- Cannot be used in `WHERE` clause directly — use subqueries or `CTE`
- Combine with `JOIN`, `CASE`, and other SQL logic for advanced analytics

---

## 🧠 Summary

> Window functions are essential for advanced analytics in SQL. They allow row-by-row operations while maintaining access to the full context of data.

Great for:
- Rankings
- Comparisons
- Running totals
- Trend analysis

---

## 🧭 Where Can You Use a Window Function?

| SQL Clause      | Usage     | Notes |
|------------------|-----------|-------|
| `SELECT`         | ✅ Yes    | Most common usage — shows results in columns |
| `ORDER BY`       | ✅ Yes    | Can sort results using window function |
| `HAVING`         | ✅ Yes    | Can filter based on windowed results |
| `WHERE`          | ❌ No     | Cannot use — runs before window functions are computed |
| `GROUP BY`       | ❌ No     | Window functions are applied after grouping |
| `JOIN ON`        | ❌ No     | Join conditions must not use window functions |

---

### ❌ Why Not in `WHERE`?

```sql
-- Invalid
SELECT *
FROM Employees
WHERE RANK() OVER (ORDER BY salary DESC) <= 3;
```

Window functions cannot be used in `WHERE` because they are evaluated **after** rows are filtered.  
To use a window function in filtering, wrap it in a subquery:

```sql
SELECT *
FROM (
  SELECT *, RANK() OVER (ORDER BY salary DESC) AS rank
  FROM Employees
) AS ranked
WHERE rank <= 3;
```

> 💡 Tip: Use subqueries or CTEs to filter rows using window function results.
