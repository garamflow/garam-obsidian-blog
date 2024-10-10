# Collection
## 1. String Collection
- 레디스는 기본적으로 다양한 타입을 지원한다.
- `SET`: 해당 명령어를 이용해서 문자열로 저장 가능하다. 이진 데이터도 포함되기에 이미지 저장도 가능하다.
- `SETnx`: 해당 키가 레디스 인스턴스에 존재하지 않을 때만 저장한다. 일반적인 `SET`에 비해 성능이 조금 더 우수하다.
- `MSet`: 레디스에서 Bulk Write 방법, 네트워크 IO를 줄여주기 때문에 성능적으로 우수하다.
	- `NX`와 `M`을 조합하여 `MSETNX`로도 활용 가능하다.
- `INCRBY`, `DECRBY`: 데이터가 정수형인 경우에 대해서 동작한다.

## 2. List Collection
- Linked List와 동일하다.
- Head와 Tail에 데이터를 삽입 할 때 성능을 보장한다.
- Job Queue 또는 Pub/Sub 모델을 구현하는데 일부 사용되는데, BRPOP, BLPOP과 함께 사용된다.
	- 친구 목록 등을 구현할 때 사용하곤 한다.
- lpos, lean 인덱스?

## 3. Set, Sorted Sets Collection
- `Set`은 중복되지 않고 정렬되지 않은 문자열의 모음을 말한다. 즉, 하나의 Key에 대해서 여러개의 Value가 중복되지 않고 정렬되지 않은 채 들어가있다.
- 특정 Key에 대한 여러개의 Value를 고유하게 저장할 때 사용된다.
- SADD, SREM, SSCAN, SMIXMEMBER 같은 명령어를 일반 Set에 적용할 수 있다.

- `Sorted Set`은 랭킹과 같은 기능을 구현하는데 매우 효과적이다.
- ZADD, ZRANGE같은 명령어를 Sorted Set에 활용할 수 있다.

## 4. Hashes Collection



## 5. BitMaps Collection