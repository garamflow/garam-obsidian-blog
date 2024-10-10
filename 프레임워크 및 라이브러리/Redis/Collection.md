# Collection
## 1. String Collection
Redis에서 **기본적으로 사용하는 데이터 타입**입니다. 문자열뿐만 아니라, 숫자나 이진 데이터도 저장할 수 있습니다.
![String Collection](/media/프레임워크%20및%20라이브러리/Redis/String%20Collection.png)
- `SET`: 문자열 데이터를 저장하는 기본 명령어. 이진 데이터도 지원하지만, 이미지 파일과 같은 대용량 파일을 저장하는 것은 비효율적일 수 있습니다.
- `SETnx`: 지정된 키가 없을 때만 데이터를 저장. 경쟁 상태를 방지하는 데 유용합니다. 일반적인 `SET`에 비해 성능이 조금 더 우수합니다.
- `MSET`: 여러 키에 값을 한 번에 저장하는 명령어로, 네트워크 IO를 줄여 성능을 향상시킵니다.
	- `NX`와 `M`을 조합하여 `MSETNX`로도 활용 가능하다.
- `INCRBY`, `DECRBY`: 저장된 데이터가 숫자일 경우 증가 또는 감소시킵니다.


## 2. List Collection
![List Collection](/media/프레임워크%20및%20라이브러리/Redis/List%20Collection.png)
- Linked List와 동일하다.
- Head와 Tail에 데이터를 삽입 할 때 성능을 보장한다.
- Job Queue 또는 Pub/Sub 모델을 구현하는데 일부 사용되는데, BRPOP, BLPOP과 함께 사용된다.
	- 친구 목록 등을 구현할 때 사용하곤 한다.
- lpos, lean 인덱스?

## 3. Set, Sorted Sets Collection
![Set, Sorted Sets Collection](/media/프레임워크%20및%20라이브러리/Redis/Set,%20Sorted%20Sets%20Collection.png)
- `Set`은 중복되지 않고 정렬되지 않은 문자열의 모음을 말한다. 즉, 하나의 Key에 대해서 여러개의 Value가 중복되지 않고 정렬되지 않은 채 들어가있다.
- 특정 Key에 대한 여러개의 Value를 고유하게 저장할 때 사용된다.
- SADD, SREM, SSCAN, SMIXMEMBER 같은 명령어를 일반 Set에 적용할 수 있다.

- `Sorted Set`은 랭킹과 같은 기능을 구현하는데 매우 효과적이다.
- ZADD, ZRANGE같은 명령어를 Sorted Set에 활용할 수 있다.

## 4. Hashes Collection
![Hashes Collection](/media/프레임워크%20및%20라이브러리/Redis/Hashes%20Collection.png)
- 하나의 Key에 대해서 여러개의 Field와 Value로 구성되어 있다. 마치 RDB의 테이블과 유사하다.
	- Key는 PK, Field는 Column, Value는 Raw
	- 단, 여기서는 레디스의 필드는 40억개까지 가능하다. 또한 RDB에 비해서 레디스가 더 자유롭다.
- HSET: 저장
	- HSETNX, HMSET: 
- HGET key field: 
- HSCAN
- HEXISTS
- HKEYS
	- 사용하지 않는걸 추천한다. 단일 스레드?


## 5. BitMaps Collection
![BitMaps](/media/프레임워크%20및%20라이브러리/Redis/BitMaps.png)
- 쿠폰 발급과 같은 서비스에서 유무를 확인 할 때, 유용하게 사용된다.
- String보다 매우 적은 메모리가 사용되고 시간 복잡도도 낮다.
	- 메모리 절약 전략은 사용되는 범위에 따라 달라지므로 조심해야한다.
