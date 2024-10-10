# Collection
## 1. String Collection
Redis에서 **기본적으로 사용하는 데이터 타입**입니다. 문자열뿐만 아니라, 숫자나 이진 데이터도 저장할 수 있습니다.

![String Collection](/media/프레임워크%20및%20라이브러리/Redis/String%20Collection.png)
- 명령어
	- `SET`: 문자열 데이터를 저장하는 기본 명령어. 이진 데이터도 지원하지만, 이미지 파일과 같은 대용량 파일을 저장하는 것은 비효율적일 수 있습니다.
	- `SETnx`: 지정된 키가 없을 때만 데이터를 저장. 경쟁 상태를 방지하는 데 유용합니다. 일반적인 `SET`에 비해 성능이 조금 더 우수합니다.
	- `MSET`: 여러 키에 값을 한 번에 저장하는 명령어로, 네트워크 IO를 줄여 성능을 향상시킵니다.
		- `NX`와 `M`을 조합하여 `MSETNX`로도 활용 가능하다.
	- `INCRBY`, `DECRBY`: 저장된 데이터가 숫자일 경우 증가 또는 감소시킵니다.
- 활용 사례: 유저 세션 데이터 저장, 간단한 설정 값 저장

## 2. List Collection
**Linked List** 구조로, **FIFO** 또는 **LIFO** 방식으로 데이터를 처리할 수 있습니다. 또한 **Head**와 **Tail**에서의 데이터 삽입/삭제가 빠른 성능을 제공합니다.

![List Collection](/media/프레임워크%20및%20라이브러리/Redis/List%20Collection.png)
- 명령어
	- `LPUSH`, `RPUSH`: 리스트의 앞이나 뒤에 데이터를 추가합니다.
	- `LPOP`, `RPOP`: 리스트의 앞이나 뒤에서 데이터를 제거하고 반환합니다.
	- `BRPOP`, `BLPOP`: Blocking List 명령어로, 큐를 구현할 때 사용됩니다.
- 활용 사례: 메시지 큐, 작업 대기열, 친구 목록
- 주의사항: 리스트의 크기가 커지면, 중간 데이터 접근 시 성능 저하가 발생할 수 있습니다.

- Job Queue 또는 Pub/Sub 모델을 구현하는데 일부 사용되는데, BRPOP, BLPOP과 함께 사용된다.
	- 친구 목록 등을 구현할 때 사용하곤 한다.
- lpos, lean 인덱스?

## 3. Set, Sorted Sets Collection
![Set, Sorted Sets Collection](/media/프레임워크%20및%20라이브러리/Redis/Set,%20Sorted%20Sets%20Collection.png)

### 3.1 Set
**중복되지 않는 문자열 집합**을 저장하며, 순서가 없는 데이터입니다.
- 명령어:
    - `SADD`: Set에 요소 추가.
    - `SREM`: Set에서 요소 제거.
    - `SRANDMEMBER`: Set에서 무작위로 요소를 반환합니다.
    - `SMEMBERS`: Set의 모든 요소를 반환.
- 활용 사례: 태그 시스템, 유저 관심사 저장

### 3.2 Sorted Set
점수(Score)를 기준으로 자동 정렬된 Set입니다.
- 명령어:
    - `ZADD`: 요소와 점수를 추가합니다.
    - `ZRANGE`: 점수에 따라 정렬된 순서대로 요소를 반환합니다.
    - `ZREM`: 특정 요소를 제거합니다.
- 활용 사례: 리더보드, 랭킹 시스템
- 주의사항: Sorted Set은 메모리 사용량이 증가할 수 있으므로, 큰 데이터셋에 사용할 때 주의해야 합니다.

## 4. Hashes Collection
**Key-Value 쌍**을 다수 저장할 수 있는 구조로, 하나의 Key에 여러 Field-Value가 매핑된 구조입니다. 마치 RDB의 테이블과 유사합니다.
- Key는 PK, Field는 Column, Value는 Raw
- 단, 여기서는 레디스의 필드는 40억개까지 가능합니다. 또한 RDB에 비해서 레디스가 더 자유롭습니다.

![Hashes Collection](/media/프레임워크%20및%20라이브러리/Redis/Hashes%20Collection.png)
- 명령어:
    - `HSET`: 하나의 필드에 값을 저장합니다.
        - `HSETNX`, `HMSET`
    - `HGET`: 필드 값을 반환합니다.
    - `HDEL`: 필드를 삭제합니다.
    - `HSCAN`: 
    - `HEXISTS`: 
    - `HKEYS`: 
- 활용 사례: 유저 프로필 정보, 설정 값 저장
- 주의사항: 작은 데이터를 저장할 때 유용하지만, 필드가 많아지면 성능이 저하될 수 있습니다.

## 5. BitMaps Collection
**비트 연산**을 사용하여 데이터를 저장하는 방식입니다. 아주 작은 메모리 사용으로 대규모 데이터를 저장할 수 있습니다. String보다 매우 적은 메모리가 사용되고 시간 복잡도도 낮습니다. 메모리 절약 전략은 사용되는 범위에 따라 달라지므로 조심해야합니다.

![BitMaps](/media/프레임워크%20및%20라이브러리/Redis/BitMaps.png)
- 명령어:
	- `SETBIT`, `GETBIT`: 특정 위치의 비트를 설정하거나 가져옵니다.
	- `BITCOUNT`: 비트 집합에서 1로 설정된 비트 수를 계산합니다.
- 활용 사례: 출석 체크, 쿠폰 발급 여부, 플래그 상태 관리
	- 쿠폰 발급과 같은 서비스에서 유무를 확인 할 때, 유용하게 사용된다.