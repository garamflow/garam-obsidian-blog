# JPA 소개
## (1) ORM
- Object-relational mapping (객체 관계 매핑)
- 객체는 객체대로 설계하고 관계형 데이터베이스는 관계형 데이터베이스대로 설계하고, ORM 프레임워크가 중간에서 매핑해준다.
- 대중적인 언어에는 대부분 ORM 기술이 존재한다.

## (2) JPA
- JAVA 애플리케이션과 JDBC API 사이에서 동작한다.
- SQL 중심 개발에서 객체 중심으로 개발할 수 있다.
- 생산성, 유지보수, 패러다임 불일치를 해결할 수 있다.

### (1) 생산성
- 저장 : `jap.persist(member)`
- 조회 : `Member member = jpa.find(memberId)`
- 수정 : `member.serName("변경 이름")`
- 삭제 : `jpa.remove(member)`

### (2) 유지보수
- SQL은 JPA가 해결해주므로 필드만 추가해주면 된다.
```
public class Member {
	private String memberId;
	private String name;
	private String tel;
}
```

### (3) 패러다임의 불일치 해결
- 상속
- 연관관계
- 객체 그래프 탐색
- 비교하기

### (4) 성능 최적화 기능
- 1차 캐시와 동일성 보장
- 트랜잭션을 지원하는 쓰기 지연
- 지연 로딩