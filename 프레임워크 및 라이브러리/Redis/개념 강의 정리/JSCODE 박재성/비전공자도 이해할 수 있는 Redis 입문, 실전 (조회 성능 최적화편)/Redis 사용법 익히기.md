# Redis 사용법 익히기
## 1. 로컬에서 Redis 설치하기 (MacOS)
1. homebrew 설치하기
2. Redis 설치하기
```t
brew install redis
brew services info redis
// 실행중이 아니라서 `x`라고 보인다.
```

1. Redis 시작하기
	- `brew services start redis`
	- `brew services info redis`
		- 실행중이면 `v`가 보인다.
2. Redis 중지하기
	- `brew services stop redis`