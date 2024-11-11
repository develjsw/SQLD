### DCL ( Data Control Language )

- 데이터 제어 언어로 데이터 베이스 사용자와 그들의 권한을 관리하기 위해 사용
- 보안과 접근권한을 제어하는 데 필수
- 주요 명령어
  - GRANT : 데이터베이스 접근권한 부여
  - REVOKE : 데이터베이스 접근권한 철회
      ~~~
      $ GRANT SELECT,INSERT ON [ 테이블명 ] TO [ 유저명 ]; // 테이블에 대한 조회/생성 권한을 특정유저에게만 허용
      $ GRANT SELECT,INSERT ON [ 테이블명 ] TO [ 유저명 ] WITH GRANT OPTION; // 테이블에 대한 조회/생성 권한을 특정유저 뿐만 아니라 다른사용자에게도 허용
    
      $ REVOKE SELECT, INSERT ON [ 테이블명 ] FROM [ 유저명 ];
      ~~~
** 참고 사항 **
  - 아래 예시에서 A가 B의 권한을 회수한 경우 - C,D의 권한도 모두 회수됨
  - B가 C에게 권한을 부여할 수 있었던 건 A가 'WITH GRANT OPTION'를 통해서 부여했기 때문이므로 B,C는 모두 'WITH GRANT OPTION'로 권한 부여한 것으로 간주
    - A → B 권한부여
    - B → C 권한부여
    - C → D 권한부여