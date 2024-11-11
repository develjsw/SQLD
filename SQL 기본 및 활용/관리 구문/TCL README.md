### `TCL ( Transaction Control Language )`

- 트랜잭션 제어 언어로, 데이터베이스에서 트랜잭션 작업을 제어함
- 데이터의 일관성을 유지하지 위해 사용
- 주요 명령어
  - `COMMIT` : 현재까지의 트랜잭션을 영구적으로 저장
  - `ROLLBACK` : 트랜잭션 중 발생한 변경사항을 원래 상태로 되돌림
  - `SAVEPOINT` : 트랜잭션 내 특정 지점을 저장, ROLLBACK 시 이 지점으로 되돌릴 수 있음
  - `SET TRANSACTION` : 트랜잭션 설정
      ~~~
      EX)
      // Oracle은 트랜잭션을 명시적으로 시작하는 명령어가 존재하지 X
    
      // 데이터 삽입
      INSERT INTO CUSTOMER (id, name, tel) VALUES (1, 'John', 010-1111-1111);
      INSERT INTO CUSTOMER (id, name, tel) VALUES (2, 'Mike', 010-2222-2222);
    
      // 특정 시점 저장
      SAVEPOINT savepoint1;
    
      // 데이터 수정
      UPDATE CUSTOMER SET name = 'sangwoo' WHERE id = 2;
    
      // savepoint1 시점으로 되돌리기
      ROLLBACK TO savepoint1;
      
      // 영구 저장
      COMMIT;
    
      // 결과 : CUSTOMER 테이블에는 John과 Mike 2개의 데이터만 저장되어 있음
      ~~~