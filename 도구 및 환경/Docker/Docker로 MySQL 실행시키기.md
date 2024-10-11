# Docker로 MySQL 실행시키기
## 1. MySQL 이미지로 컨테이너 실행시키기
### 1.1 MySQL 컨테이너 설치 및 실행
```bash
docker run -e MYSQL_ROOT_PASSWORD=password123 -p 3306:3306 -d mysql
```
- **참고)** `docker pull` 과정은 생략해도 상관없다. 왜냐하면 `docker run mysql`로 실행시켰을 때, 로컬에 이미지가 없으면 Dockerhub으로부터 MySQL 이미지를 알아서 다운받아서 실행시키기 때문이다.
- `-e MYSQL_ROOT_PASSWORD=password123` : `-e` 옵션은 컨테이너의 환경 변수를 설정하는 옵션이다.
- [Dockerhub의 MySQL 공식 문서](https://hub.docker.com/_/mysql)를 보면 환경 변수로 `MYSQL_ROOT_PASSWORD`를 정해주어야만 정상적으로 컨테이너가 실행된다고 적혀져 있다.
- 아래의 명령어로 컨테이너로 들어가서 환경 변수를 직접 눈으로 확인해보자.
```bash
$ docker exec -it [MySQL 컨테이너 ID] bash

$ echo $MYSQL_ROOT_PASSWORD # MYSQL_ROOT_PASSWORD라는 환경변수 값 출력
$ export # 설정되어 있는 모든 환경변수 출력
```

### 1.2 컨테이너 실행시킬 때 에러 없이 잘 실행됐는 지 로그 체크
```bash
docker logs [컨테이너 ID 또는 컨테이너명]
```

### 1.3 DBeaver에도 연결시키기
![dbeaver_connect](/media/도구%20및%20환경/Docker/dbeaver_connect.png)

> [!Note] Public KEy Retrieval is not allowed 에러 발생 시
> 오류는 MySQL 서버에 DBeaver 또는 다른 MySQL 클라이언트를 통해 연결할 때 발생할 수 있는 오류입니다. 이 문제는 주로 MySQL의 최신 버전에서 새로운 **암호화 키 교환 메커니즘**으로 인해 발생합니다.
> 1. DBeaver에서 연결하려는 데이터베이스를 마우스 오른쪽 버튼으로 클릭하고 **"Edit Connection"** 을 선택합니다.
> 2. 왼쪽에서 **"Driver Properties"** 탭을 클릭합니다.
> 3. **"Add Property"** 버튼을 클릭합니다.
> 4. `allowPublicKeyRetrieval`이라는 속성을 추가하고, 값을 `true`로 설정합니다.

![mysql_container_connect](/media/도구%20및%20환경/Docker/mysql_container_connect.webp)

## 2. Volume 이용하기
### 2.1 Volume 이용해서 MySQL 컨테이너 띄우기
```bash
	cd /Users/jaeseong/Documents/Develop
mkdir docker-mysql # MySQL 데이터를 저장하고 싶은 폴더 만들기
pwd # 현재 위치 주소 알아보기

docker run -e MYSQL_ROOT_PASSWORD=password123 -p 3307:3306 -v {호스트의 절대경로}/mysql_data:/var/lib/mysql -d mysql
docker run -e MYSQL_ROOT_PASSWORD=password123 -p 3306:3306 -v /Users/jaeseong/Documents/Develop/docker-mysql/mysql_data:/var/lib/mysql -d mysql
```
- `pwd` 명령어로 볼륨으로 사용하고자 하는 경로를 확인한 뒤 입력해주자.
- **주의)** `mysql_data` 디렉토리를 미리 만들어 놓으면 안 된다. 그래야 처음 이미지를 실행시킬 때 mysql 내부에 있는 `/var/lib/mysql` 파일들을 호스트 컴퓨터로 공유받을 수 있다. `mysql_data` 디렉토리를 미리 만들어놓을 경우, 기존 컨테이너의 `/var/lib/mysql` 파일들을 전부 삭제한 뒤에 `mysql_data`로 덮어씌워 버린다.
- DB에 관련된 데이터가 저장되는 곳이 `/var/lib/mysql`인지는 Dockerhub MySQL의 공식 문서에 나와있다.
![mysql_volume](/media/도구%20및%20환경/Docker/mysql_volume.webp)

### 2.2 MySQL 컨테이너 삭제하고 다시 띄워보기
```bash
# 컨테이너 종료
$ docker stop [MySQL 컨테이너 ID]
$ docker rm [MySQL 컨테이너 ID]

# 비밀번호 바꿔서 컨테이너 생성
$ docker run -e MYSQL_ROOT_PASSWORD=**pwd1234** -p 3306:3306 -v /Users/jaeseong/Documents/Develop/docker-mysql/mysql_data:/var/lib/mysql -d mysql

$ docker exec -it [MySQL 컨테이너 ID] bash
$ mysql -u root -p # 접속이 안 됨...
```

> 분명 `MYSQL_ROOT_PASSWORD` 값을 바꿔서 새로 컨테이너를 띄웠는데 비밀번호는 바뀌지 않은걸까? 이 부분 때문에 많은 분들이 헤맨다.

그 이유는 Volume으로 설정해둔 폴더에 이미 비밀번호 정보가 저장되버렸기 때문이다.
이럴 때는 이미 저장된 MySQL에 접속해서 비밀번호를 바꾸거나 mysql_data에 저장된 것을 모두 삭제하고 다시 올려야한다.

## 3. 주의할 점
만약 mysql_data 라는 폴더가 이미 존재하거나 해당 폴더 안에 파일까지 존재한다면 컨테이너로 덮어씌우기 때문에 에러가 날 수 있다.