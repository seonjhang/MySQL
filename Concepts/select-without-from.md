# SELECT Without FROM Clause in SQL

## 🧠 Question

```sql
SELECT 
    IFNULL(
        (SELECT DISTINCT Salary
         FROM Employee
         ORDER BY Salary DESC
         LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary;
```

**Q.** This query uses a subquery, but why does the outer SELECT statement not require a `FROM` clause?

---

## ✅ Summary Answer

- The outer `SELECT` simply returns a **scalar value** (a single value) from the subquery.
- In SQL, if you are **not querying a table or a set of rows**, a `FROM` clause is not needed.

---

## 📌 Examples

```sql
-- SELECT without FROM (valid)
SELECT 1 + 2;

-- SELECT with a scalar subquery (valid)
SELECT (SELECT COUNT(*) FROM Employee);
```

---

## 🔍 Related Concepts

- **Subquery**: A query nested inside another query.
- **Scalar Value**: A single value, not a table or row set.
- **IFNULL()**: Returns the first argument if it is not NULL, otherwise returns the second.

---

## 💡 Conclusion

> When a `SELECT` statement is only used to return a **scalar value**, it does not need a `FROM` clause. This is perfectly valid SQL syntax.
