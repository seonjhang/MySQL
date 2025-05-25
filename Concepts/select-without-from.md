# SELECT 문에서 FROM 절이 없는 경우

## 🧠 질문

```sql
SELECT 
    IFNULL(
        (SELECT DISTINCT Salary
         FROM Employee
         ORDER BY Salary DESC
         LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary;
```

**Q.** 이 구문에서 서브쿼리를 사용하는데, 왜 가장 바깥 SELECT에는 `FROM` 절이 없어도 되는 걸까?

---

## ✅ 답변 요약

- 바깥 SELECT는 **단일 값(스칼라 값)** 을 반환하는 **서브쿼리**를 호출하고 있을 뿐입니다.
- SQL에서는 **테이블이나 행 집합을 조회하지 않는 경우**, `FROM` 없이 `SELECT`문을 작성할 수 있습니다.

---

## 📌 예시

```sql
-- FROM 절 없는 SELECT (정상 작동)
SELECT 1 + 2;

-- FROM 절 없이 서브쿼리 값만 출력 (정상 작동)
SELECT (SELECT COUNT(*) FROM Employee);
```

---

## 🔍 관련 개념

- **서브쿼리 (Subquery)**: 다른 쿼리 안에 포함된 쿼리.
- **스칼라 값 (Scalar Value)**: 단일 값. 테이블이 아닌 하나의 결과값.
- **IFNULL()**: NULL일 경우 대체값을 반환.

---

## 💡 정리
> 바깥 SELECT문은 단순히 하나의 **스칼라 값**을 출력하려는 목적이기 때문에, `FROM` 절이 없어도 **문법적으로 유효**합니다.
