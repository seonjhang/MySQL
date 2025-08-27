
# 🔀 UNION vs UNION ALL in SQL

In SQL, `UNION` and `UNION ALL` are **set operations** used to combine the result sets of two or more `SELECT` statements. Although they seem similar, they behave differently in how they handle duplicate rows.

---

## ✅ Syntax

```sql
SELECT column1, column2 FROM tableA
UNION / UNION ALL
SELECT column1, column2 FROM tableB;
```

---

## 🆚 Key Differences

| Feature              | `UNION`                                  | `UNION ALL`                              |
|----------------------|-------------------------------------------|-------------------------------------------|
| Duplicate Handling   | Removes **duplicate rows** automatically | Keeps **all rows**, including duplicates  |
| Performance          | Slower (due to sorting and deduplication)| Faster (no extra computation)             |
| Use Case             | When you need unique results             | When duplicates are meaningful or needed  |

---

## 💡 Example

### Tables

**Table: songs_weekly**

| user_id | song_id | listen_time         |
|---------|---------|---------------------|
| 1       | 100     | 2022-08-01 12:00:00 |
| 1       | 100     | 2022-08-03 13:00:00 |

**Table: songs_history**

| user_id | song_id | song_plays |
|---------|---------|------------|
| 1       | 100     | 2          |

---

### Query using `UNION`

```sql
WITH t1 AS (
  SELECT user_id, song_id, COUNT(song_id) AS song_plays
  FROM songs_weekly
  WHERE listen_time <= '2022-08-04 23:59:59'
  GROUP BY user_id, song_id
  UNION
  SELECT user_id, song_id, song_plays
  FROM songs_history
)
SELECT user_id, song_id, SUM(song_plays) AS total_plays
FROM t1
GROUP BY user_id, song_id
ORDER BY total_plays DESC;
```

> ✅ In this case, `UNION` ensures that no duplicate rows exist across the two datasets.

---

### Query using `UNION ALL`

```sql
WITH t1 AS (
  SELECT user_id, song_id, COUNT(song_id) AS song_plays
  FROM songs_weekly
  WHERE listen_time <= '2022-08-04 23:59:59'
  GROUP BY user_id, song_id
  UNION ALL
  SELECT user_id, song_id, song_plays
  FROM songs_history
)
SELECT user_id, song_id, SUM(song_plays) AS total_plays
FROM t1
GROUP BY user_id, song_id
ORDER BY total_plays DESC;
```

> ⚠️ `UNION ALL` may include duplicates, resulting in inflated totals unless handled properly.

---

## ⚠️ When to Use What?

- Use `UNION` if:
  - You want distinct rows.
  - You don’t mind slower performance.

- Use `UNION ALL` if:
  - You want **all records** including duplicates.
  - You're optimizing for **performance** and can handle duplicates in logic.

---

## 🔍 Summary

- `UNION` = `UNION DISTINCT` (deduplicated set)
- `UNION ALL` = faster, but may cause duplicates

```sql
-- Performance-sensitive use case:
SELECT col FROM A
UNION ALL
SELECT col FROM B;

-- Deduplicated result:
SELECT col FROM A
UNION
SELECT col FROM B;
```

---

📁 **Recommended folder**: `concepts/set-operations/union-vs-unionall.md`
