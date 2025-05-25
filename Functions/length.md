# 📏 MySQL LENGTH() Function

The `LENGTH()` function in MySQL returns the **length of a string in bytes**. This is especially useful when working with binary data or multi-byte character sets such as UTF-8.

---

## 🧠 Usage

```sql
SELECT LENGTH('Hello'); -- Returns 5
SELECT LENGTH('안녕');   -- Returns 6 in UTF-8 (each Korean character is 3 bytes)
```

- To get character count (not byte count), use `CHAR_LENGTH()` or `CHARACTER_LENGTH()` instead.

---

## 📌 Use Case: LeetCode Problem 1683 - Invalid Tweets

### 🔗 Problem Summary
Filter out tweets that exceed 15 characters in length.

---

## ✅ SQL Code

```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

---

## 🧪 Test Cases

| tweet_id | content                        |
|----------|--------------------------------|
| 1        | "Vote for Biden"               |
| 2        | "Let us go to the market."     |
| 3        | "Covid19 is not a joke."       |
| 4        | "Stay safe!"                   |

---

## 🧾 Test Result

| tweet_id |
|----------|
| 2        |
| 3        |

---

## 💡 Notes

- The key idea is to compare the **byte length** of the `content` column.
- In this case, `LENGTH()` works well because all characters are ASCII (1 byte each).
