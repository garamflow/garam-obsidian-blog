# Redis 사용법 익히기
## 1. 로컬에서 Redis 설치하기 (MacOS)
1. homebrew 설치하기
2. Redis 설치하기
```shell
brew install redis
brew services info redis
// 실행중이 아니라서 `x`라고 보인다.
```

3. Redis 시작하기
```shell
brew services start redis
brew services info redis
실행중이면 `v`가 보인다.
```

4. Redis 중지하기
```shell
brew services stop redis
```

5. Redis 접속하기
- 접속 시 `ping`이라고 입력 시, `PONG`이라고 응답이 오면 정상 접속한 것이다.
```shell
brew services start redis
redis-cli

127.0.0.1:xxxx> ping
PONG
```

## 2. Redis 기본 명령어 익히기
### 데이터(Key, Val)