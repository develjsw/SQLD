### NULL 속성의 이해

1. `NULL을 포함`한 `산술연산(사칙연산)` 결과는 항상 `NULL`이다
   ~~~
   EX) NULL + 300 = NULL
   EX) 300 / NULL = NULL
   ~~~

2. `집계함수`는 `NULL을 무시`한다
   ~~~
   EX) SUM(100, 200, NULL) = 300
   EX) AVG(400, 200, NULL) = 300 (400 + 200 / 2)
   ~~~

3. NULL 비교
   - `NULL에 대한` 모든 `비교연산결과`는 `False`이다 `(IS NULL 제외)`
   - `INNER JOIN`시 조인 컬럼에 `NULL을 포함한 행`은 `생략`된다
   - NATURAL JOIN시 조인 컬럼에 NULL을 포함한 행은 생략된다


4. NULL 집합
   - `NULL 집합`에 대한 `COUNT 결과는 0`이다
     ~~~
     EX) SELECT COUNT(MOD_DATE) AS CNT FROM ORDERS // 0
     EX) (참고) SELECT COUNT(ORDER_ID) AS CNT FROM ORDERS // 8
     EX) (참고) SELECT COUNT(*) AS CNT FROM ORDERS // 8
     ~~~
   - `NULL 집합`에 대한 `COUNT를 제외한 집계함수` 결과는 `NULL`이다
     ~~~
     EX) SELECT SUM(DISCOUNT_RATE) AS SUM FROM INVENTORY // NULL
     EX) SELECT AVG(DISCOUNT_RATE) AS AVG FROM INVENTORY // NULL
     EX) SELECT MAX(DISCOUNT_RATE) AS AVG FROM INVENTORY // NULL
     ~~~
   - 공집합(WHERE절 조건에 만족하는 행이 없는 경우)의 집계함수 결과도 위와 동일하다
     ~~~
     EX) SELECT COUNT(MOD_DATE) AS CNT FROM ORDERS WHERE MOD_DATE > TO_DATE('2024-11-11 00:00:00', 'YYYY-MM-DD HH24:MI:SS') // 0
     EX) SELECT AVG(DISCOUNT_RATE) AS AVG FROM INVENTORY WHERE DISCOUNT_RATE > 10 // NULL
     ~~~

5. NULL과 GROUP BY
   - NULL 그룹도 GROUP BY 결과로 출력된다
     ~~~
     EX) SELECT DISCOUNT_RATE, COUNT(DISCOUNT_RATE) AS CNT FROM INVENTORY GROUP BY DISCOUNT_RATE // NULL, 0
     ~~~
   - HAVING 결과에 만족하는 그룹이 없는 경우 공집합이 리턴된다
     ~~~
     EX) SELECT DISCOUNT_RATE, COUNT(DISCOUNT_RATE) AS CNT FROM INVENTORY GROUP BY DISCOUNT_RATE HAVING DISCOUNT_RATE > 0 // 공집합, 공집합
     ~~~

6. NULL 치환 함수
   - NVL, NVL2, COALESCE / IS NULL은 NULL 값을 특정값으로 치환하는 함수이다
     - `NVL(타겟, NULL인 경우 보여줄 값)`
     - `NVL2(타겟, NULL 아닌경우 보여줄 값, NULL인 경우 보여줄 값)`
     - `COALESCE(타겟1, 타켓2, 타겟3 ...) // 타겟1부터 NULL값이 아닌 값이 나올때까지 다음 인수의 값으로 평가 진행, 모두 NULL값이라면 NULL값 반환`
        ~~~
        EX) SELECT COALESCE('출력1', '출력2', NULL) FROM DUAL // 출력1
        EX) SELECT COALESCE(NULL, '출력2', NULL) FROM DUAL // 출력2
        EX) SELECT COALESCE(NULL, NULL, '출력3') FROM DUAL // 출력3
        ~~~
   - DECODE, CASE문으로도 NULL 치환이 가능하다
     - `DECODE(표현식, 검색값1, 반환값1, 검색값2, 반환값2, ..., 기본값) // 표현식과 일치하는 검색값이 있는 경우 해당 반환값을 반환, 일치하는 값이 없는 경우 기본값 반환(기본값 생략한 경우 NULL 반환)`
        ~~~
        EX) SELECT DECODE('test', 'test', 'test출력') FROM DUAL // test출력
        EX) SELECT DECODE('test', 'test1', 'test1출력', 'test', 'test2출력', 'default') FROM DUAL // test2출력
        EX) SELECT DECODE('test', 'test1', 'test1출력', 'test2', 'test2출력', 'default') FROM DUAL // default
        EX) SELECT DECODE('test', 'test1', 'test1출력', 'test2', 'test2출력') FROM DUAL // NULL
        ~~~
   - SQL-SERVER의 NULLIF는 특정값과 같은 값을 NULL로 치환해주는 함수이다

