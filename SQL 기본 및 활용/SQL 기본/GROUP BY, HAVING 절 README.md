### GROUP BY, HAVING 절

- HAVING절은 GROUP BY에서의 WHERE절로 그룹화한 데이터들 중에서 조건이 필요한 경우에 사용됨 


- `집계함수`는 `HAVING절`, `ORDER BY절`에만 `올 수 있음` (SELECT절, FROM절, WHERE절 등에는 올 수 없음)


- `그룹화된 쿼리에서 ORDER BY절`에는 `GROUP BY에 명시`되었거나 `집계함수`만 올 수 있음
  ~~~
  EX)
  SELECT
      MEMBER_ID
      , SUM(PRICE) AS AMOUNT
  FROM
      ORDERS
  GROUP BY
      MEMBER_ID
  ORDER BY
      MEMBER_ID DESC -- GROUP BY절에 명시
      , SUM(PRICE) DESC -- 집계함수(SELECT절에 있는 값은 순서상 못가져옴)
  ~~~