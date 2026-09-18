# SQL: IN/NOT IN, EXISTS, WHERE와 HAVING

**날짜:** 2026-09-18 (금)

---

## 1. IN과 NOT IN

- **IN**: 내가 지정한 목록 안에 해당하는 값을 조회한다.
- **NOT IN**: 지정한 목록에 해당되지 않는 값을 조회한다.

```sql
SELECT * FROM students WHERE grade IN ('A', 'B');
SELECT * FROM students WHERE grade NOT IN ('A', 'B');
```

## 2. EXISTS (존재 여부 확인)

**EXISTS**는 조건을 만족하는 행이 존재하는지를 조회한다.

- 조건을 만족하는 행이 1개라도 있음 → `TRUE` → 조회됨
- 조건을 만족하는 행이 하나도 없음 → `FALSE` → 조회되지 않음

```sql
SELECT * FROM customers c
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.customer_id = c.customer_id
);
```

## 3. WHERE와 HAVING

- **WHERE**: `GROUP BY`하기 전에 개별 행을 필터링할 때 사용한다.
- **GROUP BY**: 같은 값을 가진 행들을 그룹으로 묶는 것.
- **HAVING**: `GROUP BY`로 묶인 그룹 결과(집계함수 값)를 기준으로 필터링할 때 사용한다.

```sql
SELECT category, SUM(line_total) AS total
FROM order_items
GROUP BY category
HAVING SUM(line_total) > 100000;
```
