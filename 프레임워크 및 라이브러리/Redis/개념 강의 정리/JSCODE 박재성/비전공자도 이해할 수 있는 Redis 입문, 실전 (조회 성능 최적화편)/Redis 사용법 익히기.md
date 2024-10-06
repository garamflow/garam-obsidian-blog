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
set test:testvalue3 test ex 30

# ttl key이름
# 남은 시간 출력
# 키가 삭제되면 -2가 반환된다.
# 키가 존재하지만 ttl이 설정되있지 않으면 -1이 반환된다.
ttl test:testvalue3
-2
```

### 모든 데이터 삭제
```shell
# flushall

# 삭제 후
keys *
(empty array)
```

## 3. Redis에서 Key 네이밍 컨벤션 익히기
꼭 지켜야하는 건 아니지만 추천하는 방식이다.
- 콜론(`:`)을 사용해서 계층적으로 의미를 구분해서 사용한다.

예시를 보면 알기 쉽다
- `users:100:profile` : 사용자들(users) 중에서 PK가 100인 사용자(user)의 프로필(profile)
- `products:123:details` : 상품들(products) 중에서 PK가 123인 상품(product)의 세부사항(details)

이런 식으로 컨벤션을 정했을 때의 장점이 있다.
1. **가독성** : 데이터의 의미와 용도를 쉽게 파악할 수 있다.
2. **일관성** : 컨벤션을 따름으로써 코드의 일관성이 높아지고 유지보수가 쉬워진다.
3. **검색 및 필터링 용이성** : 패턴 매칭을 사용해 특정 유형의 Key를 쉽게 찾을 수 있다 .
4. **확장성** : 서로 다른 Key와 이름이 겹쳐 충돌할 일이 적어진다.