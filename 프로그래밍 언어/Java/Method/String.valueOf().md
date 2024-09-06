# String.valueOf()
- 다양한 데이터 타입의 값을 문자열로 변환할 수 있다.
- `null`, 기본 데이터 타입, 객체 등 거의 모든 종류의 입력을 받아 해당 입력을 적절하게 문자열로 표현한다.

## 주요 기능
- 다형성: `String.valueOf()` 는 오버로드된 여러 버전을 가지고 있어서, `char`, `int`, `long` 등 다양한 타입의 인자를 받을 수 있다.
- 널 안전: `String.valueOf()` 는 `null`을 입력받아서 `"null"` 문자열로 변환 가능하다.
	- `toString()` 메서드를 직접 호출할 때 발생하는 `NullPointException`을 방지한다.

## 예시
```java
int i = 10;
String str = String.valueOf(i);  // "10"

Object obj = null;
String str = String.valueOf(obj);  // "null"

char[] data = {'J', 'a', 'v', 'a'};
String str = String.valueOf(data);  // "Java"
```

## 구현 원리
- 대부분 기본 타입의 경우 Java 내부적으로 적절한 `toString()` 메서드를 호출하거나 새로운 `String` 인스턴스를 생성해서 값을 문자열로 변환한다.
- 객체의 경우 `toString()` 메서드가 호출되고, 이 메서드가 `null` 을 안전하게 처리하도록 설계되어 있다.