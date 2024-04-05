# StringBuilder
- String은 불변(immutable)이어서 객체가 그 값을 변경할 수 없다 보니, 문자열 조작 시 새로운 String 객체가 생성된다.
	- 메모리 사용량 상승, 성능 저하 발생
- 그러나 StringBuilder를 사용하면 변경 가능한(mutable) 문자열을 다룰 수 있다.

## 주요 특징과 장점
- 변경 가능: 내부적으로 문자 배열을 유지하며, 문자열 추가 및 변경 시 새로운 객체를 생성하지 않고 기존 데이터를 변경한다.
- 성능: 문자열 조작 연산이 많을 시, String에 비해 더 높은 성능을 제공한다. 특히, 크기가 큰 문자열을 다루거나 반복적으로 문자열을 변경할 때 유용하다.
- 메모리 효율성: 불필요한 문자열 객체를 생성하지 않아서 메모리 사용을 최적화한다.
- 유연성: `append()`, `insert()` 등의 메소드들을 제공해서 문자열을 다양한 방식으로 쉽게 조작할 수 있다.

## 예시
```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World!");

String result = sb.toString(); // "Hello World!"
```