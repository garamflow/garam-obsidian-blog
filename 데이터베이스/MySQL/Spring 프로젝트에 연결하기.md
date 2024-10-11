# Spring (feat. JPA) 프로젝트에 연결하기
## 1. 의존성 추가하기
MySQL과 연결하려면 MySQL JDBC 드라이버가 필요합니다.
프로젝트의 `build.gradle` 혹은 `pom.xml`에 의존성을 추가해줍니다.
```groovy
runtimeOnly 'com.mysql:mysql-connector-j'
```

```xml
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    ...
</dependencies>
```

## 2. 애플리케이션 설정 추가
Spring 프로젝트가 MySQL 데이터베이스와 통신하려면 데이터베이스 URL, 사용자 이름, 비밀번호 등을 설정해야 합니다.
`application.properties` 혹은 `application.yml`에 작성하면 됩니다.

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb?createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false&serverTimezone=Asia/Seoul&characterEncoding=utf8
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA 관련 설정
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

```yml
spring:
  datasource:
	# url: jdbc:mysql://데이터베이스주소:포트번호/데이터베이스이름?options
    url: jdbc:mysql://localhost:3306/mydb?createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false&serverTimezone=Asia/Seoul&characterEncoding=utf8
    username: root
    password: your_password
    driver-class-name: com.mysql.cj.jdbc.Driver

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
```
- **`url: jdbc:mysql://localhost:3306/mydb`**
	- JDBC를 사용하여 `localhost`에 있는 MySQL 서버의 `mydb`라는 데이터베이스에 연결하는 URL이라는 의미
- **`driver-class-name: com.mysql.cj.jdbc.Driver`**
	- MySQL 데이터베이스 연결에 사용할 JDBC 드라이버의 클래스 이름입니다.
	- MySQL Connector/J의 최신 버전인 `com.mysql.cj.jdbc.Driver`를 사용합니다.
- **`hibernate.ddl-auto: update`**
	- Hibernate의 자동 DDL(Data Definition Language) 동작을 설정합니다.
	- 이 옵션은 애플리케이션 실행 시 엔티티 클래스의 스키마를 데이터베이스에 자동으로 반영하는 방법을 지정합니다.
	- **`update`**: 애플리케이션 실행 시 데이터베이스 스키마를 업데이트합니다. 기존 데이터는 그대로 유지하고 스키마만 변경됩니다. (주의: 운영 환경에서 위험할 수 있습니다.)
- **`show-sql: true`**: JPA가 실행되는 동안 **SQL 쿼리**를 콘솔에 출력할지 여부를 설정합니다. `true`로 설정하면 실행되는 SQL이 콘솔에 출력됩니다.
- **`properties.hibernate.format_sql: true`**: SQL 쿼리의 출력 형식을 보기 좋게 **포맷**합니다. 이를 통해 SQL 쿼리를 읽기 쉽게 만듭니다.

