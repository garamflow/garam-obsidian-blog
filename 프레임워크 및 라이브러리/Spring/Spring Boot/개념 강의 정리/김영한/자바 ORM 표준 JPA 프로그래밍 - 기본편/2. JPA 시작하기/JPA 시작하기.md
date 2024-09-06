# JPA 시작하기
## (1) H2 Database 설치하기
- https://www.h2database.com
- h2 데이터베이스는 2.2.222 버전을 다운로드 받아서 설치한다. 다음 링크를 선택하면 2.2.222 버전을 다운로드 받아서 설치할 수 있다. 압축을 풀면 바로 실행할 수 있다.
	- https://github.com/h2database/h2database/releases/download/version-2.2.222/h2-2023-08-22.zip
- 맥, 리눅스 사용자 설치
	- 디렉토리 이동 : `cd bin`
	- 권한 주기: `chmod 755 h2.sh`
	- 실행: `./h2.sh`
- H2 데이터베이스를 실행하면 웹 브라우저가 열리면서 화면이 오픈된다.
	- 주의! 특히 뒤에 jsessionid 부분이 변경되면 안된다.
- 사용자명은 `sa` 입력 JDBC URL에 다음 입력한다.
	- `jdbc:h2:~/test` (최초 한번)
		- 이 경우 `연결 시험` 을 호출하면 오류가 발생한다. `연결` 을 직접 눌러주어야 한다.
	- 본인 홈 폴더로 이동한 다음 `~/test.mv.db` 파일 생성 확인(숨김 파일)
- 이후부터는 `jdbc:h2:tcp://localhost/~/test` 이렇게 접속하면 된다.

## (2)JPA 구동 방식
### Maven
![JPA 구동 방식](/media/Spring%20Boot/개념%20강의%20정리/김영한/자바%20ORM%20표준%20JPA%20프로그래밍%20-%20기본편/2.%20JPA%20시작하기/JPA%20구동%20방식.svg)

### 객체와 테이블 생성하고 매핑해보기
```java
import jakarta.persistence.*;

@Entity
@Table(name = "USER")
public class Member {
	@Id
	private Long id;
	@Column(name = "username")
	private String name;

	// Getter, Setter
}
```
- `@Entity` : JPA가 관리할 객체
- `@Table(name = "USER")` : 테이블에서 USER라는 이름의 테이블과 매핑한다.
- `@Id` : 데이터베이스 PK와 매핑
- `@Column(name = "username")` : 해당 이름을 가진 컬럼과 매핑한다.

### 주의점
- 엔티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에서 공유해서 사용한다.
- 엔티티 매니저는 쓰레드간에 공유하지 않는다. 
	- 사용 후 버려야한다.
- **JPA의 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.**

## (3) JPQL
- JPA를 사용하면 엔티티 객체를 중심으로 개발하게 된다.
- 그래서 쿼리를 짤 때도 **엔티티 객체를 대상**으로 짜야된다.
- 그것을 SQL을 추상화한 JPQL이라고 한다.
	- 객체 지향 쿼리 언어
- SQL과 문법이 유사하다.
	- JPQL은 엔티티 객체를 대상으로 쿼리
	- SQL은 데이터베이스 테이블을 대상으로 쿼리