# 🔎 SQL `LIKE` Operator

The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

---

## 📌 Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name LIKE pattern;
```

---

## 🧪 Examples

### 1. Starts with 'J'

```sql
SELECT * 
FROM Users
WHERE name LIKE 'J%';
```

✅ `%` matches zero or more characters.

---

### 2. Ends with 'n'

```sql
SELECT * 
FROM Users
WHERE name LIKE '%n';
```

---

### 3. Contains 'oh'

```sql
SELECT * 
FROM Users
WHERE name LIKE '%oh%';
```

---

### 4. One character between letters

```sql
SELECT * 
FROM Users
WHERE name LIKE '_an';
```

✅ `_` matches exactly one character.

---

## 🔤 Case Sensitivity

- `LIKE` is **case-insensitive** by default in MySQL with common collations (e.g., `utf8_general_ci`).
- Use `BINARY` keyword for case-sensitive matching:

```sql
SELECT *
FROM Users
WHERE BINARY name LIKE 'J%';
```

---

## 🧠 Best Practices

| Pattern     | Meaning                                  |
|-------------|------------------------------------------|
| `'a%'`      | Starts with `'a'`                        |
| `'%a'`      | Ends with `'a'`                          |
| `'%a%'`     | Contains `'a'`                           |
| `'a_c'`     | Starts with `'a'`, one letter, then `'c'`|

---

## 🚀 Performance Tip

Avoid leading `%` to maintain index usage:

```sql
-- Slower
WHERE name LIKE '%abc'

-- Faster
WHERE name LIKE 'abc%'
```
