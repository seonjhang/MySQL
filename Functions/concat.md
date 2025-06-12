# 🔗 CONCAT() Function in MySQL

The `CONCAT()` function joins two or more strings into one.

## 🔍 Syntax
```sql
CONCAT(str1, str2, ..., strN)
```

- Accepts any number of string arguments.
- If **any argument is NULL**, the result is NULL.

## ✅ Examples
```sql
SELECT CONCAT('Hello', ' ', 'World');  -- 'Hello World'
SELECT CONCAT('2024', '-', '06', '-', '09');  -- '2024-06-09'
```

## ⚠️ Tip
- To safely handle NULLs, use `CONCAT_WS()` (with separator), which ignores NULLs:
```sql
SELECT CONCAT_WS('-', '2024', NULL, '09');  -- '2024-09'
```

## 🧠 Use Cases
- Building date strings like `'YYYY-MM'`
- Merging columns into a formatted string
- Creating unique IDs or labels from multiple values
