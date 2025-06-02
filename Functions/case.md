# 🔍 MySQL `CASE` Expression

The `CASE` expression provides conditional logic in SQL with multiple possible outcomes. It is part of the SQL standard and more flexible than `IF()`.

---

## 📌 Syntax

### ✅ Searched CASE
```sql
CASE 
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE default_result
END
```

### ✅ Simple CASE
```sql
CASE column
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ...
    ELSE default_result
END
```

---

## 🧪 Example (Searched CASE)

```sql
SELECT name,
       salary,
       CASE 
           WHEN salary >= 8000 THEN 'High'
           WHEN salary >= 5000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_band
FROM Employees;
```

---

## ✅ Use Case

Use `CASE` when you need to check **multiple conditions** and return different values depending on the match. It is more readable for complex logic.

---

## ⚖️ Comparison vs `IF()`

- `CASE` is **standard SQL** and portable.
- Better for **more than two** outcomes.
- Readable when using **multiple branches**.
