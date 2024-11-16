### 조인 (JOIN)

- INNER JOIN
- LEFT OUTER JOIN (=LEFT JOIN)
- RIGHT OUTER JOIN (=RIGHT JOIN)
- FULL OUTER JOIN
  - 일치하는 행은 결합, 일치하지 않는 행도 포함 (NULL로 표시)
  ~~~
  -- 테이블 A
  SELECT * FROM employees;
  | employee_id | name   |
  |-------------|--------|
  | 1           | Alice  |
  | 2           | Bob    |
  | 3           | Charlie|
  
  
  -- 테이블 B
  SELECT * FROM departments;
  | department_id | manager_id |
  |---------------|------------|
  | 101           | 1          |
  | 102           | 4          |
  
  
  -- FULL OUTER JOIN 사용 결과
  SELECT
      e.employee_id,
      e.name,
      d.department_id,
      d.manager_id
  FROM 
      employees e
      FULL OUTER JOIN departments d
  ON e.employee_id = d.manager_id;
  
  | employee_id | name    | department_id | manager_id |
  |-------------|---------|---------------|------------|
  | 1           | Alice   | 101           | 1          |
  | 2           | Bob     | NULL          | NULL       |
  | 3           | Charlie | NULL          | NULL       |
  | NULL        | NULL    | 102           | 4          |
  ~~~

- CROSS JOIN
  - 모든 가능한 조합 생성 (카티션 곱)

  ~~~
  -- 테이블 A
  SELECT * FROM products;
  | product_id | product_name |
  |------------|--------------|
  | 1          | Laptop       |
  | 2          | Smartphone   |
  
  
  -- 테이블 B
  SELECT * FROM stores;
  | store_id | store_name  |
  |----------|-------------|
  | 101      | Store A     |
  | 102      | Store B     |
  
  
  -- CROSS JOIN 사용 결과
  SELECT
      p.product_id,
      p.product_name,
      s.store_id,
      s.store_name
  FROM 
      products p
      CROSS JOIN stores s;
  
  | product_id | product_name | store_id | store_name |
  |------------|--------------|----------|------------|
  | 1          | Laptop       | 101      | Store A    |
  | 1          | Laptop       | 102      | Store B    |
  | 2          | Smartphone   | 101      | Store A    |
  | 2          | Smartphone   | 102      | Store B    |
  ~~~ 