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
혹스 jar 파일 빌드 시 아래와 같이 빌드하면 테스트 태스크를 제외하고 빌드한다.
```bash
./gradlew build -x test
```

4. Dockerfile 작성하기
```docker
FROM openjdk:17-jdk

COPY build/libs/*SNAPSHOT.jar /app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]
ENTRYPOINT ["/bin/bash", "-c", "sleep 500"] # 500초 동안 시스템을 일시정지 시키는 명령어
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

6. Spring Boot 프로젝트 빌드하기
```bash
./gradlew clean build

or
# 테스트 태스크 없이 빌드
./gradlew build -x test
```

7. compose 파일 실행시키기
```bash
docker compose up -d --build
```

8. compose 실행 현황 보기
```bash
$ docker compose ps
$ docker ps
$ docker logs [Container ID]
```

## 컨테이너로 실행시킨 Spring Boot가 MySQL에 연결이 안 되는 이유
![springboot_mysql_not_connect](/media/도구%20및%20환경/Docker/springboot_mysql_not_connect.webp)

각각의 컨테이너는 **자신만의 네트워크망과 IP 주소**를 가지고 있다. 호스트 컴퓨터 입장에서 localhost는 호스트 컴퓨터를 가리키지만, Spring Boot 컨테이너 입장에서 localhost는 Spring Boot 컨테이너를 가리킨다.

그런데 Spring Boot의 코드를 작성할 때 DB 정보를 아래와 같이 입력했었다. Spring Boot가 실행되는 환경인 컨테이너 입장에서 [localhost:3306](http://localhost:3306)라는 주소는, Spring Boot 컨테이너 내부에 있는 3306번 포트와 연결을 시도하게 된다. 하지만 Spirng Boot가 실행되는 컨테이너 내부의 3306번 포트에는 아무것도 실행되고 있지 않다. 이러한 구조상의 문제 때문에 Spring Boot가 MySQL에 연결이 안 되고 있었던 것이다.
```yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: pwd1234
    driver-class-name: com.mysql.cj.jdbc.Driver
```

### 해결법
그럼 어떻게 Spring Boot의 컨테이너에서 다른 컨테이너에 존재하는 MySQL에 연결을 할 수 있을까?
compose.yml에서 정의한 Service 이름으로 서로 통신할 수 있다.

```yml
# applicaion.yml

spring:
  datasource:
    url: jdbc:mysql://my-db:3306/mydb
    username: root
    password: pwd1234
    driver-class-name: com.mysql.cj.jdbc.Driver
```
위 코드에서 my-db는 도대체 어디서 나온 값일까?

```yml
# compose.yml

services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd1234
      MYSQL_DATABASE: mydb
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping" ]
      interval: 5s
      retries: 10
```
이 service 이름이 컨테이너의 주소를 뜻한다. 해당 컨테이너의 IP 주소와 같은 역할을 한다.
위와 같이 코드를 수정한 뒤에 다시 한 번 컨테이너를 실행시켜보자.
```bash
$ ./gradlew clean build
$ docker compose down
$ docker compose up --build -d

$ docker ps # 정상적으로 Spring Boot, MySQL이 실행된 걸 확인할 수 있다. 
```