# 📆 MySQL Date & Time Functions

This file summarizes commonly used MySQL functions for manipulating and calculating date and time values.

---

## 🧱 1. `DATE_ADD(date, INTERVAL expr unit)`

**Adds** a time interval to a date.

```sql
SELECT DATE_ADD('2024-01-01', INTERVAL 7 DAY);  -- '2024-01-08'
```

- Add days, months, years, hours, etc.
- Use case: due dates, expiration, schedule generation

---

## 🔁 2. `DATE_SUB(date, INTERVAL expr unit)`

**Subtracts** a time interval from a date.

```sql
SELECT DATE_SUB('2024-01-10', INTERVAL 5 DAY);  -- '2024-01-05'
```

---

## 📅 3. `DATEDIFF(date1, date2)`

Returns the **number of days** between two dates.

```sql
SELECT DATEDIFF('2024-01-10', '2024-01-05');  -- 5
```

- Result is `date1 - date2`
- Only supports day-level difference

---

## 🕐 4. `TIMESTAMPDIFF(unit, datetime1, datetime2)`

Returns the difference between two timestamps in the specified unit.

```sql
SELECT TIMESTAMPDIFF(DAY, '2024-01-01', '2024-01-10');  -- 9
SELECT TIMESTAMPDIFF(HOUR, '2024-01-01 00:00:00', '2024-01-01 03:00:00');  -- 3
```

- Units: `SECOND`, `MINUTE`, `HOUR`, `DAY`, `MONTH`, `YEAR`, etc.

---

## 🧪 5. `NOW()` / `CURRENT_DATE()` / `CURDATE()`

Get current date and/or time.

```sql
SELECT NOW();            -- '2024-05-25 15:30:00'
SELECT CURRENT_DATE();   -- '2024-05-25'
SELECT CURDATE();        -- '2024-05-25'
```

- `NOW()` returns full datetime
- `CURDATE()` or `CURRENT_DATE()` returns only the date

---

## 🔁 6. `DATE_FORMAT(date, format)`

Format a date/time value as a string.

```sql
SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i');  -- '2024-05-25 15:45'
```

- Format codes:
  - `%Y`: year
  - `%m`: month
  - `%d`: day
  - `%H`: hour
  - `%i`: minutes

---

## 🧮 7. EXTRACT(YEAR_MONTH FROM date)
Extracts parts of a date such as year, month, day, etc.

```sql
SELECT EXTRACT(YEAR_MONTH FROM '2024-06-09');  -- 202406
SELECT EXTRACT(YEAR FROM '2024-06-09');        -- 2024
SELECT EXTRACT(MONTH FROM '2024-06-09');       -- 6
```

Use case: Grouping or filtering by year, month, etc.
---

## 🧱 8. LPAD(str, length, pad_str)
Pads the left side of a string with another string until a certain length is reached.

```sql
SELECT LPAD('6', 2, '0');  -- '06'
SELECT LPAD(MONTH(NOW()), 2, '0');  -- Pads month numbers to always have two digits
```

Use case: Formatting months or days as `01`, `02`, etc., for consistent date strings.


✅ Example Use: Formatting Date as `YYYY-MM`

```sql
SELECT CONCAT(YEAR(trans_date), '-', LPAD(MONTH(trans_date), 2, '0')) AS month
FROM Transactions;
```

Alternative with `DATE_FORMAT`:

```sql
SELECT DATE_FORMAT(trans_date, '%Y-%m') AS month
FROM Transactions;
```

---

## 📆 9. YEAR(date) / MONTH(date)
Extracts the year or month from a given date.

```sql
SELECT YEAR('2024-06-09');   -- 2024
SELECT MONTH('2024-06-09');  -- 6
```

✅ Use Cases:
- Used in reporting or grouping queries (e.g., by year/month)
- Often combined with `GROUP BY`, `ORDER BY`, or string formatting

---

## 💡 Summary Table

| Function          | Purpose                      | Notes                             |
|-------------------|------------------------------|-----------------------------------|
| `DATE_ADD()`       | Add interval to a date       | `INTERVAL 7 DAY`, `1 MONTH`, etc. |
| `DATE_SUB()`       | Subtract interval from date  | Same as above                     |
| `DATEDIFF()`       | Days between two dates       | Only supports day unit            |
| `TIMESTAMPDIFF()`  | Difference in any time unit  | More flexible than `DATEDIFF`     |
| `NOW()` / `CURDATE()` | Current date/time         | Use `NOW()` for full datetime     |
| `DATE_FORMAT()`    | Custom date formatting       | Useful for display purposes       |
