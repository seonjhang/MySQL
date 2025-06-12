# 🧱 LPAD() Function in MySQL

The `LPAD()` function pads the **left side** of a string with another string until it reaches a specified length.

## 🔍 Syntax
```sql
LPAD(str, length, pad_str)
```

- `str`: the original string to pad
- `length`: the total length of the returned string
- `pad_str`: the string to pad with

## ✅ Examples
```sql
SELECT LPAD('7', 2, '0');        -- '07'
SELECT LPAD('abc', 5, '*');     -- '**abc'
SELECT LPAD('abc', 2, '*');     -- 'ab' (original string is truncated)
```

## 🧠 Use Cases
- Formatting months as `01`, `02`, etc.
- Generating padded IDs (e.g., `00001`)
- Ensuring consistent string lengths for sorting or display
