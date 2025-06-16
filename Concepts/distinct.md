# ❌ Incorrect Use of DISTINCT in SELECT Clause

In MySQL, the `DISTINCT` keyword is used to return only **unique rows**, but it must be placed **before all selected columns**, not in front of just one column.

---

## ❗ Invalid Syntax

```sql
SELECT teacher_id, DISTINCT subject_id
FROM Teacher;
```

🔴 **Why this is wrong:**
MySQL does not allow `DISTINCT` to be used on a single column like this within the `SELECT` clause.

---

## ✅ Correct Usage

### 1. Apply `DISTINCT` to the entire row
Returns only unique combinations of `teacher_id` and `subject_id`.

```sql
SELECT DISTINCT teacher_id, subject_id
FROM Teacher;
```

### 2. Get unique values of just one column
Returns all unique `subject_id` values from the `Teacher` table.

```sql
SELECT DISTINCT subject_id
FROM Teacher;
```

---

## 🧠 Summary

| Syntax                      | Valid | Purpose                                      |
|----------------------------|-------|----------------------------------------------|
| `SELECT DISTINCT col1, col2` | ✅    | Unique pairs of col1 and col2                |
| `SELECT col1, DISTINCT col2` | ❌    | ❌ Invalid SQL syntax                         |
| `SELECT DISTINCT col`        | ✅    | Unique values of one column                  |

> Always place `DISTINCT` at the start of the `SELECT` clause when used.

