# 🔁 LAG() and LEAD() in MySQL

`LAG()` and `LEAD()` are **window functions** that allow access to other rows in a result set **without using JOINs or subqueries**. They are commonly used to compare a row with its previous or next row.

---

## 📌 General Concept

### 🔁 `LAG(expression [, offset, default])`

- Returns a value from a **previous row** in the window frame.
- Optional parameters:
  - `offset`: how many rows back to look (default = 1)
  - `default`: value to return if there’s no row

```sql
LAG(temperature, 1, NULL) OVER (ORDER BY recordDate)
```

---

### ⏩ `LEAD(expression [, offset, default])`

- Returns a value from a **next row**.
- Same optional parameters as `LAG()`.

```sql
LEAD(temperature, 1, NULL) OVER (ORDER BY recordDate)
```

---

### 🧠 Use Cases

| Scenario                              | Use Function |
|---------------------------------------|--------------|
| Compare with previous day's value     | `LAG()`      |
| Detect upward/downward trends         | `LAG()` or `LEAD()` |
| Compare with next week's data         | `LEAD()` with offset = 7 |
| Avoid complex `JOIN` or `SELF-JOIN`   | Both         |

---

### ⚠️ Notes

- Requires **MySQL 8.0 or higher**.
- Part of the **ANSI SQL:2003** standard.
- Cannot be used directly in `WHERE` clause—use in `SELECT`, subquery, or `HAVING`.

---

Window functions `LAG()` and `LEAD()` are used to access data from a previous or next row **without using self joins**.

---

## 🔁 LAG()

- Retrieves the value from a previous row.
- Commonly used to compare a current value with the one before it.

```sql
SELECT id, temperature,
       LAG(temperature) OVER (ORDER BY recordDate) AS prev_temp
FROM Weather;
```

---

## ⏩ LEAD()

- Retrieves the value from the next row.
- Useful for comparing current value with the next value.

```sql
SELECT id, temperature,
       LEAD(temperature) OVER (ORDER BY recordDate) AS next_temp
FROM Weather;
```

---

## 🧠 Use Case: Compare temperatures

```sql
SELECT id
FROM (
    SELECT id, temperature, recordDate,
           LAG(temperature) OVER (ORDER BY recordDate) AS prev_temp
    FROM Weather
) AS temp
WHERE temperature > prev_temp;
```

---

## ⚠️ Notes

- Available in MySQL 8.0 and above.
- Cannot be used in earlier versions—use JOINs as an alternative.
