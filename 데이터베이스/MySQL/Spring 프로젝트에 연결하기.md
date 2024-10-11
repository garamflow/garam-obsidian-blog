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

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb?useSSL=false&serverTimezone=Asia/Seoul
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA 관련 설정
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```



application.properties 혹은 application.yml 에 