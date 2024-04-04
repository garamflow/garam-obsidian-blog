# toUpperCase(), toLowerCase()
- `String` 객체의 문자들을 각각 대문자와 소문자로 변환하는 데 사용된다.
- 문자열 내 모든 문자에 대해 대문자 또는 소문자 변환을 수행해서 새로운 문자열을 반환한다.
	- 원본 문자열을 변경되지 않는다.

## 예시
```java
String str = "Hello World";
String upperStr = str.toUpperCase();
System.out.println(upperStr); // HELLO WORLD

String str = "Hello World";
String lowerStr = str.toLowerCase();
System.out.println(lowerStr); // hello world
```

## Character.toUpperCase(char ch), Character.toLowerCase(char ch)
- 단일 문자 char에 대해 대문자, 소문자 변환을 수행하기 위해서 사용된다.
- 단일 문자를 인자로 받아 해당 문자를 변환시키는데, `Character` 클래스의 메소드를 사용하게 된다.

```java
char lowerCase = 'a';
char upperCase = Character.toUpperCase(lowerCase);
System.out.println(upperCase); // 출력: A
```