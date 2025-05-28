# 📊 SQL Logical Query Processing Order

Understanding **when** each clause in a SQL query is executed is critical to mastering concepts like **window functions**, **aggregations**, and **filters**.

---

## 🔁 Logical Query Processing Order

| Step | Clause      | Description                              |
|------|-------------|------------------------------------------|
| 1    | `FROM`      | Load tables and apply joins              |
| 2    | `WHERE`     | Filter rows (before grouping or calculations) |
| 3    | `GROUP BY`  | Group rows for aggregation               |
| 4    | `HAVING`    | Filter groups after aggregation          |
| 5    | `SELECT`    | Calculate final column values            |
| 6    | `WINDOW`    | 👉 Window functions are evaluated here    |
| 7    | `ORDER BY`  | Sort the final results                   |
| 8    | `LIMIT`     | Limit number of rows in the result set   |

---

## 💡 Why Does This Matter?

- You **cannot** use window functions in `WHERE` or `JOIN ON` clauses, because they haven’t been computed yet.
- Use a **subquery or CTE** if you need to filter based on a window function.
- `HAVING`, `SELECT`, and `ORDER BY` are the **safest places** to use window functions.

---
