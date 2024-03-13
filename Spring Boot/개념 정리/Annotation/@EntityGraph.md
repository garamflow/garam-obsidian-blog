# @EntityGraph
## 1) `@EntityGraph`란?
- JPA에서 엔티티의 로딩 전략을 구성할 때 사용한다.
- 특정 엔티티를 조회할 때 연관된 엔티티나 컬렉션을 어떻게 로딩할 지 세밀하게 제어할 수 있다.
- JPA는 지연 로딩과 즉시 로딩 방식을 제공하는데, `@EntityGraph`를 사용하면 이런 로딩 전략을 쿼리 메소드 수준에서 동적으로 변경 가능하다.

## 2) 사용 방법
- 레포지토리 인터페이스의 메소드 위에서 선언해서 사용한다.
- 해당 어노테이션을 사용할 때는 `attributePaths` 속성을 통해 로딩하고 싶은 연관 엔티티의 경로를 지정한다.
- `type` 속성을 사용해 로딩 전략을 지정할 수 있다.
	- `LOAD` , `FETCH`

## 3) 사용 예시
```java
@Entity
public class Book {
	@Id
	private Long id;
	private String title;

	@ManyToOne(fetch = FetchType.LAZY)
	private Author author;
}

public interface BookRepository extends JpaRepository<Book, Long> {
	@EntityGraph(attrivutePaths = {"author"}, type = EntityGraph.EntityGraphType.FETCH)
	Optional<Book> findById(Long id);
}
```
- `Book` 엔티티는 `Author` 엔티티와 연관되어 있다.
- 기본적으로 `Author` 는 지연 로딩으로 설정되어 있지만 `findById` 메소드에 `@EntityGraph`를 사용해서 `author`를 즉시 로딩하게 지정되어 있다.
- 해당 메소드를 통해 `Book` 엔티티를 조회할 때 `Author` 엔티티도 함께 로딩된다.

## 4) 사용 시 장점
### (1) 성능 최적화
- 필요한 엔티티만 선택적으로 즉시 로딩해서 N+1 문제 해결로 성능을 최적화할 수 있다.

### (2) 유연성
- 리본 로딩 전략을 변경하지 않아도, 필요에 따라 특정 쿼리에서만 로딩 전략을 조정할 수 있다.