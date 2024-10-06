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
### 데이터(Key, Value) 저장하기
```shell
# set key이름 value

set test:testvalue "test good"
set test:testvalue2 test
```

### Key로 Value 값 조회하기
```shell
# get key이름

get test:testvalue
"test good"

get test:testvalue2
"test"
```

### 저장 된 모든 Key 조회하기
```shell
# 모든 키 값 조회
keys *
1) test:testvalue
2) test:testvalue2
```

### Key로 데이터 삭제하기
```shell
# del key이름

del test:testvalue
(integer) 1 # 삭제가 잘 되었을 때 뜸
del test:testvalue
(nil) # 삭제할 게 없을 때 뜸
```

### 데이터 저장 시 만료시간(TTL, Time to Live) 설정하기
레디스는 RDBMS와는 다르게 데이터 저장 시 만료시간을 설정할 수 있다. 즉, 영구적으로 데이터를 저장하지 않고 일정 시간이 되면 데이터가 삭제되도록 셋팅할 수 있다.

레디스의 특성상 메모리 공간이 한정 되어 있기 때문에 모든 데이터를 레디스에 저장할 수 없다. 따라서 만료시간(TTL)을 활용해 자주 사용하는 데이터만 레디스에 저장해놓고 쓰는 식으로 활용한다.
```shell
# set key이름 value ex seconds

# ttl key이름
# 남은 시간 출력, 키가 삭제되면 -2가 반환된다.
# 키가 존재하지만 ttl이 설정되있지 않으면 -1이 반환된다.


```