# 6강

### `@GeneratedValud`
- pk 값을 JPA가 알아서 순차적인 값으로 넣어줌

### `@PersistenContext` 사용
- 스프링 컨테이너가 JPA에 있는 EntityManager를 가져옴
  ```java
  @PersistenceContext
  private EntityManager em;
  ``` 

- em 에다가 entity를 넣으면 (`Member.class`) JPA가 알아서 Entity에 맞는 쿼리를 가져옴
   ```java
   em.find(Member.class, id);
   ```
  
### Entity
- 기본 생성자가 존재해야 함 (protected 까지 가능)
  - 프록시 기술을 쓸 때 JPA 구현체들이 기본 생성자에 접근하기 때문에 private 로 생성자를 막는다면 오류가 발생

### Test
- `@Transactional` 어노테이션
  - 테스트가 끝나는 시점에 롤백
  - DB에서 직접 확인하고 싶다면 `@Rollback(false)` 어노테이션을 사용할 것