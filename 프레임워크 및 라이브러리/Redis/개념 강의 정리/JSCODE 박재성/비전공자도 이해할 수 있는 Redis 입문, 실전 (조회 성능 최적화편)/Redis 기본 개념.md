# Redis 기본 개념
## 1. Redis란?, Redis의 장점 알아보기
### 1. Redis란?
Redis는 인터넷에 검색 시, 아래와 같이 나온다.
- 레디스(Redis)는 Remote Dictionary Server의 약자로서, “키-값” 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템(DBMS)이다. - 위키백과 -
이 내용을 좀 더 쉽게 변환해보면 아래와 같다.
- Redis는 데이터 처리 속도가 엄청 빠른 NoSQL 데이터베이스이다.
	- key-value 형태로 저장하는 데이터베이스

### 2. Redis의 장점
#### 2.1 처리 성능
레디스(Redis)는 **인메모리(in-memory)에 모든 데이터를 저장**한다. 그래서 데이터의 처리 성능이 굉장히 빠르다. MySQL과 같은 RDBMS의 데이터베이스는 대부분 디스크(Disk)에 데이터를 저장한다. 하지만 Redis는 메모리(RAM)에 데이터를 저장한다. 디스크(Disk)보다 메모리(RAM)에서의 데이터 처리속도가 월등하게 빠르다. 이 때문에 Redis의 데이터 처리 속도가 RDBMS에 비해 훨씬 빠르다.

## 2. Redis 주요 사용 사례
Redis는 사용 사례가 아주 다양하다.
- 캐싱 (Caching)
- 세션 관리 (Session Management)
- 실시간 분석 및 통계 (Real-time Analystics)
- 메시지 큐 (Message Queue)
- 지리공간 인덱싱 (Geospatial Indexing)
- 속도 제한 (Rate Limiting)
- 실시간 채팅 및 메시징 (Real-time Chat And Messaging)

## 3. 백엔드 채용 공고
