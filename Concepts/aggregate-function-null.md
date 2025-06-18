# 🧠 Understanding Aggregate Functions on Empty Sets in MySQL

In MySQL, aggregate functions like `MAX()`, `SUM()`, `AVG()`, etc., behave differently from regular `SELECT` queries when no rows are returned by a subquery or filter.

---

## ✅ Key Concept

**Aggregate functions always return one row**, even if the input dataset is empty.  
In contrast, a regular `SELECT` will return **zero rows** if no match is found.

---

## 🔍 Example

Given the table:

```sql
MyNumbers
---------
| num |
|-----|
| 8   |
| 8   |
| 7   |
| 7   |
| 3   |
| 3   |
| 3   |
```

Suppose we want to find the maximum number that occurs **exactly once**.

---

### ❌ Query 1: Using `IFNULL(...)` on direct `GROUP BY`

```sql
SELECT IFNULL(num, NULL) AS num
FROM MyNumbers
GROUP BY num
HAVING COUNT(num) = 1
ORDER BY num DESC
LIMIT 1;
```

- This query returns **0 rows** because there is no number that appears exactly once.

---

### ✅ Query 2: Using `MAX(...)` over a subquery

```sql
SELECT MAX(num) AS num
FROM (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(num) = 1
) AS t;
```

- This query returns **1 row** with a `NULL` value.
- Why? Because `MAX()` is an aggregate function, and when applied over an **empty input set**, it still returns **one row** with a **NULL value**.

---

## 📌 Summary Table

| Query Type     | No Matching Rows | Result       |
|----------------|------------------|--------------|
| Regular SELECT | ❌ No row         | 0 rows       |
| Aggregate (`MAX`, `SUM`) | ✅ Returns row | 1 row with NULL |

---

## 🧠 Tip

If you're checking for the presence of values using aggregation, always remember:
- **Aggregate functions will return one row**, so check for `IS NULL` if needed.
- If you want zero output when there's no match, use a **non-aggregate subquery**.

```sql
-- Check if any result exists
SELECT MAX(num) FROM ...;
-- Check if any unique number exists
-- → Compare to NULL explicitly
```

---

## 🧪 Practical Implication

This distinction is crucial when writing queries that need to:
- Return "no result" vs. "result is unknown or empty"
- Be used in reporting dashboards where the **presence of a row matters**
