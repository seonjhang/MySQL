# 🔍 MySQL `IF()` Function

The `IF()` function in MySQL evaluates a condition and returns one value if the condition is true, and another if it is false.

---

## 📌 Syntax

```sql
IF(condition, value_if_true, value_if_false)
```

---

## 🧪 Example

```sql
SELECT name,
       salary,
       IF(salary > 5000, 'High', 'Low') AS salary_level
FROM Employees;
```

📘 This will label each employee's salary as `'High'` or `'Low'` based on the threshold of 5000.

---

## ✅ Use Case

Use `IF()` when you need to evaluate **a single true/false condition** and return two possible outcomes. It is a simple and concise way to handle binary logic.

---

## ⚠️ Notes

- Only available in MySQL and some other dialects — not part of the SQL standard.
- For more than two conditions, use the `CASE` expression.
