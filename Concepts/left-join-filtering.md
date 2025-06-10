# 🔀 LEFT JOIN Filtering: `ON` vs `WHERE` in MySQL

In SQL, when using a `LEFT JOIN`, the placement of your filtering condition—whether in the `ON` clause or the `WHERE` clause—**matters a lot**.

---

## ❌ Filtering in the `WHERE` clause (Incorrect for LEFT JOIN)

```sql
SELECT product_id, 
       IFNULL(ROUND(SUM(price * units) / SUM(units), 2), 0) AS average_price
FROM Prices
LEFT JOIN UnitsSold USING (product_id)
WHERE purchase_date BETWEEN start_date AND end_date
GROUP BY product_id;
```

### 🔍 What’s wrong?
- Although we used `LEFT JOIN`, the `WHERE` clause filters out any rows where `UnitsSold.purchase_date` is `NULL`.
- As a result, **rows with no matching record in `UnitsSold` are dropped**.
- This behaves like an **INNER JOIN**, not a true `LEFT JOIN`.

---

## ✅ Filtering in the `ON` clause (Correct)

```sql
SELECT p.product_id,
       IFNULL(ROUND(SUM(p.price * u.units) / SUM(u.units), 2), 0) AS average_price
FROM Prices AS p
LEFT JOIN UnitsSold AS u
  ON p.product_id = u.product_id
  AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```

### ✅ Why it works
- The condition `purchase_date BETWEEN start_date AND end_date` is evaluated **during the join**.
- If there's no match, `NULL` values remain for the `UnitsSold` fields.
- This ensures the **LEFT JOIN includes all products**, even if no units were sold in the given period.

---

## 🧠 Summary

| Clause    | Keeps unmatched left rows? | Acts like INNER JOIN if failed match? | Best for LEFT JOIN? |
|-----------|-----------------------------|----------------------------------------|----------------------|
| `WHERE`   | ❌ No                        | ✅ Yes                                 | ❌ No                |
| `ON`      | ✅ Yes                       | ❌ No                                  | ✅ Yes               |

> 🔑 Use `ON` for filtering in `LEFT JOIN` to preserve unmatched rows from the left table.

