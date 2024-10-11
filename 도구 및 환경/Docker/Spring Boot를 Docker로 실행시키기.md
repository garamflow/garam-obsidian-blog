# Spring Boot를 Docker로 실행시키기
1. 스프링 부트 프로젝트를 생성해주고 코드를 작성한다.
2. Dockerfile을 프로젝트 최상단에 생성해준다.
```docker
FROM openjdk:17-jdk

COPY build/libs/*SNAPSHOT.jar app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]
```
3. Spring Boot 프로젝트 빌드하기
```bash
$ ./gradlew clean build
```
4. Dockerfile을 바탕으로 이미지 빌드하기
```bash
$ docker build -t hello-server .
```
5. 이미지가 잘 생성됐는 지 확인하기
```bash
$ docker image ls
```
6. 생성한 이미지를 컨테이너로 실행시켜보기
```bash
$ docker run -d -p 8080:8080 hello-server
```
7. 컨테이너 잘 실행되고 있는 지 확인하기
```bash
$ docker ps
```
8. localhost:8080 으로 들어가보기

9. 실행시킨 컨테이너 중지 / 삭제하기, 이미지 삭제하기
```bash
$ docker stop {컨테이너 ID}
$ docker rm {컨테이너 ID}
$ docker image rm {이미지 ID}
```