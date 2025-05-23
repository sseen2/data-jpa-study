## 13장

## 쿼리 메소드
### 2. @NamedQuery
- 쿼리에 이름을 부여하고 호출하는 기능
- 쿼리문을 xml 파일로 빼서 사용할 수도 있음

[NamedQuery 코드](https://github.com/sseen2/data-jpa-study/blob/5c1a4c2f4295bf9c5a375f2e830e784cef35eb74/src/main/java/study/data_jpa/entity/Member.java#L21-L24)
```java
@NamedQuery(
        name = "Member.findByUsername",
        query="select m from Member m where m.username = :username"
)
public class Member {
    private String username;
}
```
[NamedQuery 사용](https://github.com/sseen2/data-jpa-study/blob/5c1a4c2f4295bf9c5a375f2e830e784cef35eb74/src/main/java/study/data_jpa/repository/MemberRepository.java#L14-L15)
```java
public interface MemberRepository extends JpaRepository<Member, Long> {
    @Query(name = "Member.findByUsername")
    List<Member> findbyUsername(@Param("username") String username);
}
```
- `@Query()`를 주석처리해도 정상적으로 실행
  1. JpaRepository<타입, PK 타입>에서 타입 값과 메서드 이름으로 namedQuery를 먼저 찾음
     - 지금 상황에서는 Member.findByUsername을 찾음
  2. NamedQuery가 있다면 실행
  3. 없다면 메소드 이름으로 쿼리 생성
  - 우선순위를 바꿀 수도 있음

- 장점
  - 오타가 발생한다면 애플리케이션 로딩 시점에서 한 번 파싱하기 때문에 바로 예외 발생
    > 기본적으로 정적 쿼리기 때문에 애플리케이션 로딩 시점에 쿼리를 파싱
    > -> JPQL을 SQL로 미리 만들어 놓는 과정에서 오타가 있다면 예외가 발생하게 됨

- 실무에서 잘 사용하지 않는 이유
    - Entity에 정의하는 게 별로임
    - 메서드에 바로 쿼리를 지정할 수 있는 기능이 있기 때문에 굳이 NamedQuery를 사용하지 않아도 됨
