# equals()
- 객체 간 값을 비교하기 위한 메서드이다.
- `Object` 클래스에서 정의되며, 모든 클래스에서 오버라이드하여 사용할 수 있다.
- 두 객체의 참조가 같은지, 즉 메모리 상 같은 위치를 가리키는지 확인한다.
- == 연산자와 같은 행동을 한다.

## 예시
```java
String a = new String("test");
String b = new String("test");

boolean result = a.equals(b); // true, 두 문자열의 내용이 같기 때문입니다.
```