# @Modifying
## 1) `@Modifying` 란?
- Spring Data JPA에서 사용하는 어노테이션이다.
- 주로 `@Query` 어노테이션과 함께 사용된다.
- 조회 (Query)가 아닌 데이터를 변경하는 작업 (INSERT, UPDATE, DELETE 등)을 수행하는 JPQL이나 SQL 쿼리를 정의할 때 필요하다.

## 2) 사용 방법
- `@Modifying` 어노테이션은 데이터 변경 작업 수행 쿼리 메소드에 추가된다.
- 대부분 `@Transactional` 어노테이션도 함께 사용해야 한다.
	- 데이터 변경 작업이 트랜잭션 내에서 실행되어야 하기 때문이다.
- `@Query` 어노테이션과 함께 사용하여 JPQL 또는 SQL 쿼리를 직접 정의할 수 있다.

## 3) 사용 예시
```java
public interface UserRepository extends JpaRepository<User, Long> {
	@Modifying
	@Transactional
	@Query("update User u set u.name = ?1 where u.id = ?2")
	int updateUserNameById(String name, Long id);
}
```
- `updateUserNameById` 메소드는 사용자의 이름을 업데이트하는 JPQL 쿼리를 정의한다.
- `@Modifying` 어노테이션은 메소드가 데이터베이스의 데이터를 변경하는 작업임을 명시하며, `@Transactional`은 이 작업이 트랜잭션의 일부로 실행됨을 보장한다.

## 4) 사용 시 주의사항
- `@Modifying` 어노테이션을 사용할 때 메소드의 실행 결과로 영향 받은 엔티티의 수가 반환된다.
	- 따라서 반환 타입을 `void` 대신 `int` 또는 `void`로 지정해야 할 수 있다.
- `@Modifying` 어노테이션을 사용하는 메소드를 호출하기 전후에 영속성 컨텍스트를 명시적으로 플러시하거나 클리어하는 것이 좋을 수 있다.
	- `clearAutomatically`와 `flushAutomatically` 속성을 통해 설정할 수 있다.
- 데이터 변경 작업 후에는 영속성 컨텍스트의 상태와 데이터베이스의 상태가 동기화되지 않을 수 있다.