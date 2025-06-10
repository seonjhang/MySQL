# 🔍 MySQL `REGEXP` and `RLIKE` Operator

MySQL provides the `REGEXP` (or `RLIKE`) operator to perform advanced pattern matching using **regular expressions**.

---

## 📌 Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name REGEXP pattern;
```

📝 `RLIKE` is a synonym for `REGEXP`.

---

## 🧪 Basic Examples

### 1. Names that contain 'a', 'b', or 'c'

```sql
SELECT *
FROM Users
WHERE name REGEXP '[abc]';
```

✅ Matches any name with at least one of the letters `a`, `b`, or `c`.

---

### 2. Names starting with 'J'

```sql
SELECT *
FROM Users
WHERE name REGEXP '^J';
```

✅ `^` anchors the pattern to the **start** of the string.

---

### 3. Names ending with 'n'

```sql
SELECT *
FROM Users
WHERE name REGEXP 'n$';
```

✅ `$` anchors the pattern to the **end** of the string.

---

### 4. Names with exactly 3 lowercase letters

```sql
SELECT *
FROM Users
WHERE name REGEXP '^[a-z]{3}$';
```

✅ Matches names like `tom`, `jim`.

---

### 5. Match digit patterns

```sql
SELECT *
FROM Logs
WHERE message REGEXP '[0-9]{4}';
```

✅ Matches any 4-digit number in the message.

---

## 🧠 REGEXP vs LIKE

| Feature                  | `LIKE`          | `REGEXP` / `RLIKE`      |
|--------------------------|------------------|--------------------------|
| Wildcard support         | `%`, `_` only    | Full regex patterns      |
| Anchors (^, $)           | ❌ Not supported | ✅ Supported              |
| Bracket expressions      | ❌ No            | ✅ Yes (`[abc]`)          |
| Quantifiers `{n}`        | ❌ No            | ✅ Yes                    |
| Complexity               | Simple patterns  | Advanced search patterns |
| Index usage              | ✅ Yes           | ⚠️ Often not used         |

---

## ⚠️ Notes

- MySQL's regular expression engine is **not Perl-compatible** and does **not support lookaheads or backreferences**.
- As of MySQL 8.0, regex support is enhanced with `REGEXP_LIKE()` as part of the standard SQL function set.

---

## ✅ Use Case Tips

- Use `LIKE` for simple patterns (`starts with`, `ends with`, `contains`)
- Use `REGEXP` for complex pattern matching (e.g., `[A-Za-z]+[0-9]$`)
