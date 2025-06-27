# 🔀 Non-Equi Join in SQL

In SQL, a **non-equi join** is a type of join where the condition uses comparison operators other than the equals sign (`=`), such as `>`, `<`, `>=`, or `<=`.

---

## 🧠 What is a Non-Equi Join?

Instead of joining two tables where column values are equal, a non-equi join compares values using a range.

### 🔍 Example

```sql
SELECT *
FROM Queue q1
JOIN Queue q2 ON q1.turn >= q2.turn
GROUP BY q1.turn;
```

### 🧾 What happens here?

This join matches each row in `q1` with **all rows in `q2` where `q2.turn` is less than or equal to `q1.turn`**.

If `Queue` contains:

| turn |
|------|
| 1    |
| 2    |
| 3    |

Then the join produces:

| q1.turn | q2.turn |
|---------|---------|
| 1       | 1       |
| 2       | 1       |
| 2       | 2       |
| 3       | 1       |
| 3       | 2       |
| 3       | 3       |

This effectively creates a **cumulative or rolling relationship**, where higher `q1.turn` values include more prior rows.

---

## ✅ Use Cases

- Cumulative counts or sums
- Ranking rows without using window functions
- Implementing logic based on previous or lower values

---

## ⚠️ Caution

- Non-equi joins can produce large result sets (like a CROSS JOIN).
- Be mindful of performance: add indexes or filtering as needed.
- Not all SQL optimizers handle them efficiently.

---

## 🧠 Summary

| Feature             | Description                         |
|---------------------|-------------------------------------|
| Operator            | Uses `>`, `<`, `>=`, `<=`           |
| Result              | Often larger than equi-joins        |
| Purpose             | Cumulative or range-based matching  |
| Performance         | May be slow without indexing        |
