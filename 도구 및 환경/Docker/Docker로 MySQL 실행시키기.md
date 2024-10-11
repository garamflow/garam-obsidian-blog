# Docker로 MySQL 실행시키기
## 1. MySQL 이미지로 컨테이너 실행시키기
```bash
docker run -e MYSQL_ROOT_PASSWORD=password123 -p 3306:3306 -d mysql
```
- **참고)** `docker pull` 과정은 생략해도 상관없다. 왜냐하면 `docker run mysql`로 실행시켰을 때, 로컬에 이미지가 없으면 Dockerhub으로부터 MySQL 이미지를 알아서 다운받아서 실행시키기 때문이다.
- `-e MYSQL_ROOT_PASSWORD=password123` : `-e` 옵션은 컨테이너의 환경 변수를 설정하는 옵션이다.
- Dockerhub의 MySQL 공식 문서를 보면 환경 변수로 `MYSQL_ROOT_PASSWORD`를 정해주어야만 정상적으로 컨테이너가 실행된다고 적혀져있다.
- 