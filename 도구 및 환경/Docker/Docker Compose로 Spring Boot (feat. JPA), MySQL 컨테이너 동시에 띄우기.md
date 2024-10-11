# Docker Compose로 Spring Boot (feat. JPA), MySQL 컨테이너 동시에 띄우기
Spring Boot + JPA + MySQL 프로젝트를 컨테이너 띄워본다.

1. Spring Boot 설치 및 코드 작성하기
- 스프링부트를 설치해준다.
- 간단하게 코드를 작성해준다.
- 만약 지금 프로젝트를 실행하면 데이터베이스가 연결이 안되어 있어서 에러가 뜬다.

2. application.properties (or .yml) 작성하기
```yml
spring:
	datasource:
		url: jdbc:mysql://localhost:3306/mydb
		username: root
		password: password
		driver-class-name: com.mysql.cj.jdbc.Driver		
```

3. 테스트 코드 삭제
현재 돌아가지 않는 테스트코드때문에 에러가 나므로 해당 파일을 지금은 삭제해준다.

4. Dockerfile 작성하기
```docker
FROM openjdk:17-jdk

COPY build/libs/*SNAPSHOT.jar /app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

5. compose.yml 작성하기
```yml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
		# my-db의 컨테이너가 생성되고 healthy 하다고 판단 될 때, 해당 컨테이너를 생성한다. 
    depends_on:
      my-db:
        condition: service_healthy
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd1234
      MYSQL_DATABASE: mydb # MySQL 최초 실행 시 mydb라는 데이터베이스를 생성해준다.
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping" ] # MySQL이 healthy 한 지 판단할 수 있는 명령어
      interval: 5s # 5초 간격으로 체크
      retries: 10 # 10번까지 재시도
```





