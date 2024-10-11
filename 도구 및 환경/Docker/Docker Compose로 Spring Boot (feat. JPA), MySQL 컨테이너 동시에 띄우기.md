# Docker Compose로 Spring Boot (feat. JPA), MySQL 컨테이너 동시에 띄우기
Spring Boot + JPA + MySQL 프로젝트를 컨테이너 띄워본다.

## 1. Spring Boot 설치 및 코드 작성하기
- 스프링부트를 설치해준다.
- 간단하게 코드를 작성해준다.
- 만약 지금 프로젝트를 실행하면 데이터베이스가 연결이 안되어 있어서 에러가 뜬다.

### 1.1 application.properties (or .yml) 작성하기
```yml
spring:
	datasource:
		url: jdbc:mysql://localhost:3306/mydb
		username: root
		password: password
		driver-class-name: com.mysql.cj.jdbc.Driver
		
```
- 