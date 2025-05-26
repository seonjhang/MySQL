# 🔗 SQL JOIN Types

SQL JOINs are used to combine rows from two or more tables based on a related column between them.

---

## 🧱 Types of JOINs

### 1. INNER JOIN
Returns only the rows with matching values in both tables.

```sql
SELECT *
FROM A
INNER JOIN B ON A.id = B.id;
```

✅ Use when you only want data where there is a match in both tables.

---

### 2. LEFT JOIN (LEFT OUTER JOIN)
Returns all rows from the left table, and the matched rows from the right table. If there’s no match, the result is NULL on the right side.

```sql
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id;
```

✅ Use when you want all data from the left table, regardless of match.

---

### 3. RIGHT JOIN (RIGHT OUTER JOIN)
Returns all rows from the right table, and the matched rows from the left table. If there’s no match, the result is NULL on the left side.

```sql
SELECT *
FROM A
RIGHT JOIN B ON A.id = B.id;
```

✅ Less common. Use when you want to keep all rows from the right table.

---

### 4. FULL JOIN (FULL OUTER JOIN)
Returns all rows when there is a match in one of the tables. Non-matching rows will contain NULL for the missing side.

```sql
-- Not supported in MySQL directly, simulate with UNION
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id
UNION
SELECT *
FROM A
RIGHT JOIN B ON A.id = B.id;
```

✅ Use when you want all data, matched or not.

---

### 5. CROSS JOIN
Returns the Cartesian product of the two tables. Every row from the first table is paired with every row from the second.

```sql
SELECT *
FROM A
CROSS JOIN B;
```

✅ Use with caution; result set size is (rows in A) × (rows in B).

---

### 6. CARTESIAN JOIN via Comma Syntax
Another way to produce a **Cartesian Join** is by using **comma-separated tables** in the `FROM` clause **without a `WHERE` condition**:

```sql
SELECT *
FROM A, B;
```

This is equivalent to `CROSS JOIN` and will return **all combinations of rows** from A and B.

📌 Example:

If A has 2 rows and B has 3 rows → result has **2 × 3 = 6 rows**

---

## 💡 Tips

- Use `INNER JOIN` when match is required.
- Use `LEFT JOIN` to preserve rows from the first table.
- Use `CROSS JOIN` or comma syntax only when you intentionally want full combinations.
- MySQL does not support `FULL OUTER JOIN` natively—use `UNION` as shown above.
- Always specify the `ON` condition to avoid accidental Cartesian products.

---

## 🧠 Summary Table

| JOIN Type     | Description                              | Nulls for Unmatched | MySQL Support |
|---------------|------------------------------------------|---------------------|----------------|
| INNER JOIN    | Only matching rows from both tables      | No                  | ✅              |
| LEFT JOIN     | All left rows + matched right rows       | Right side          | ✅              |
| RIGHT JOIN    | All right rows + matched left rows       | Left side           | ✅              |
| FULL JOIN     | All rows from both sides                 | Both sides          | 🚫 (simulate)  |
| CROSS JOIN    | Cartesian product                        | N/A                 | ✅              |
| A, B (comma)  | Cartesian product (implicit CROSS JOIN)  | N/A                 | ✅              |

---

## 🔍 JOIN Syntax Comparison: `JOIN ... ON` vs Comma Join

There are two main ways to write joins in SQL, but they are **not equal in clarity or safety**.

### ✅ Preferred: Explicit JOIN

```sql
SELECT w2.id
FROM Weather w1
JOIN Weather w2
  ON DATEDIFF(w2.recordDate, w1.recordDate) = 1
WHERE w2.temperature > w1.temperature;
```

- Defines relationships clearly
- Follows ANSI SQL standards
- Easier to read and maintain

---

### ❌ Discouraged: Comma-Separated Join

```sql
SELECT w2.id
FROM Weather w1, Weather w2
WHERE DATEDIFF(w2.recordDate, w1.recordDate) = 1
  AND w2.temperature > w1.temperature;
```

- Implicitly performs a **CROSS JOIN** (Cartesian product)
- Risk of massive result set if `WHERE` clause is forgotten
- Considered outdated and error-prone

---

### 🧠 Syntax Style Summary

| Feature                  | `JOIN ... ON`         | `A, B (comma join)`   |
|--------------------------|-----------------------|------------------------|
| Readability              | ✅ Clear               | ❌ Poor                |
| Risk of cross join       | ❌ Low                 | ⚠️ High if WHERE missed |
| SQL standard             | ✅ ANSI-compliant      | ❌ Legacy style         |
| Maintenance              | ✅ Easier              | ❌ Harder               |
| Recommendation           | ✅ Use this!           | ❌ Avoid if possible    |

> 💡 Always prefer `JOIN ... ON` for modern, maintainable, and safe SQL queries.
