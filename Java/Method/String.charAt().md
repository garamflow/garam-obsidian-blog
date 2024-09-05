# String.charAt()
- String 클래스에서 제공하는 메서드로, 문자열의 특정 인덱스에 있는 문자(char)를 반환한다.
- 문자열의 각 문자를 개별적으로 처리할 때 유용하다.

## 기본 문법
```java
char charAt(int index);
```
- 매개변수: index는 문자열에서 반환할 문자의 위치를 나타낸다.
- 반환값: 지정한 인덱스의 문자를 반환한다.
- 예외: 인덱스가 문자열의 길이를 초과하거나 음수이면 `StringIndexOutOfBoundsException` 이 발생한다.

## 예시 코드
```java
public class CharAtExample {
    public static void main(String[] args) {
        String str = "Hello, World!";

        // 문자열의 특정 위치의 문자 출력
        char ch1 = str.charAt(0);  // 첫 번째 문자 'H'
        char ch2 = str.charAt(7);  // 8번째 문자 'W'

        System.out.println("첫 번째 문자: " + ch1);
        System.out.println("8번째 문자: " + ch2);
        
        // charAt과 반복문을 이용하여 문자열의 각 문자 출력
        for (int i = 0; i < str.length(); i++) {
            System.out.println("인덱스 " + i + "의 문자: " + str.charAt(i));
        }
    }
}
```