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

### 2. LEFT JOIN (or LEFT OUTER JOIN)
Returns all rows from the left table, and the matched rows from the right table. If there’s no match, the result is NULL on the right side.

```sql
SELECT *
FROM A
LEFT JOIN B ON A.id = B.id;
```

✅ Use when you want all data from the left table, regardless of match.

---

### 3. RIGHT JOIN (or RIGHT OUTER JOIN)
Returns all rows from the right table, and the matched rows from the left table. If there’s no match, the result is NULL on the left side.

```sql
SELECT *
FROM A
RIGHT JOIN B ON A.id = B.id;
```

✅ Less common. Use when you want to keep all rows from the right table.

---

### 4. FULL JOIN (or FULL OUTER JOIN)
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

## 💡 Tips

- Use `INNER JOIN` when match is required.
- Use `LEFT JOIN` to preserve rows from the first table.
- MySQL does not support `FULL OUTER JOIN` natively—use `UNION` as shown above.
- Always specify the `ON` condition to avoid unexpected Cartesian products.

---

## 🧠 Summary Table

| JOIN Type     | Description                              | Nulls for Unmatched | MySQL Support |
|---------------|------------------------------------------|---------------------|----------------|
| INNER JOIN    | Only matching rows from both tables      | No                  | ✅              |
| LEFT JOIN     | All left rows + matched right rows       | Right side          | ✅              |
| RIGHT JOIN    | All right rows + matched left rows       | Left side           | ✅              |
| FULL JOIN     | All rows from both sides                 | Both sides          | 🚫 (simulate)  |
| CROSS JOIN    | Cartesian product                        | N/A                 | ✅              |
