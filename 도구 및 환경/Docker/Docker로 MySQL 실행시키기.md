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

## 2. 