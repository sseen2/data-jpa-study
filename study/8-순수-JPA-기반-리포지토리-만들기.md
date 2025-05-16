# 8강

### JPQL
- 테이블이 아닌 객체를 대상으로 하는 쿼리
  - SQL과 비슷하지만 약간 차이가 있음

### update 코드가 없는 이유
- JPA는 기본적으로 Entity를 변경할 때 변경 감지(Dirty Checking) 기능으로 데이터를 바꾸게 됨
  - EntityManager를 통해 조회 -> Entity 직접 수정 -> 트랜잭션 커밋 -> 자동으로 변경된 부분을 업데이트
  - 자바 컬렉션과 동일한 방식으로 변경 가능

    > setUsername()을 하게 되면 Member를 update 하지 않아도 값이 변경됨  