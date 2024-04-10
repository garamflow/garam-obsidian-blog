# Arrays.copyOfRange()
- `Arrays` 유틸리티 클래스에서 제공하는 메소드이다.
- 배열의 특정 범위를 복사해서 새로운 배열을 생성하는 데 사용한다.

## 사용법
```java
public static T[] copyOfRange(T[] original, int from, int to)
```
- `T[] original`: 복사할 원본 배열
- `int from`: 복사를 시작할 인덱스. 해당 값도 포함되며 0부터 시작한다.
- `int to`: 복사를 종료할 인덱스. 이 값은 범위에 포함되지 않는다.
- 반환 값으로 원본 배열의 `from` 인덱스 부터 `to - 1` 인덱스까지 요소를 포함하는 새 배열을 반환한다.

## 예제
```java
int[] original = {1, 2, 3, 4, 5};
int[] copied = Arrays.copyOfRange(original, 1, 4); // {2, 3, 4}
```

## 주의사항
- `to` 인덱스가 원본 배열의 길이보다 크면, `ArrayIndexOutOfBoundsException`이 발생할 수 있다.
- 이 메소드는 기본 타입 배열과 참조 타입 배열 모두에 사용할 수 있는 오버로드된 버전을 제공한다 (예: `int[]`, `long[]`, `Object[]` 등).