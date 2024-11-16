### `DML ( Data Manipulation Language )`

- 데이터 조작 언어로, 데이터베이스 내에서 데이터를 추가,수정,삭제하는 데 사용
- 주요 명령어
  - `INSERT` : 데이터 삽입 
  - `UPDATE` : 데이터 수정
  - `DELETE` : 데이터 삭제
  - `MERGE` : 데이터 병합
  - `SELECT` : 데이터 조회
      ~~~
      -- 데이터 삽입
      INSERT INTO [ 테이블명 ] ([ 컬럼명1 ], [ 컬럼명2 ], [ 컬럼명3 ]) VALUES ([ 컬럼값1 ], [ 컬럼값2 ], [ 컬럼값3 ]);
    
      -- 데이터 수정
      UPDATE [ 테이블명 ] SET [ 변경할 컬럼 ] = [ 변경할 컬럼값 ] WHERE [ 조건 ];
    
      -- 데이터 삭제
      DELETE FROM [ 테이블명 ] WHERE [ 조건 ];
    
      -- 데이터 조회
      SELECT [ 컬럼명 ] FROM [ 테이블명 ] WHERE [ 조건 ];
      ~~~
- INSERT에서 컬럼명 명시 하지 않으면 모든 컬럼값 적어줘야 함
  ~~~
  EX)
  INSERT INTO 테이블명 (컬럼1, 컬럼2, 컬럼3) VALUES (값1, 값2, 값3); // Success
  INSERT INTO 테이블명 VALUES (값1, 값2, 값3); // 여기에서 컬럼이 더 있는 경우 에러 발생
  ~~~