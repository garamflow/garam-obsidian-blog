# toCharArray()
- `String` 클래스의 메서드로 해당 문자열을 구성하는 문자들을 포함하는 새로운 `char` 배열을 반환하는 메서드이다.
- 문자열 내 모든 문자를 순서대로 배열에 저장해서 반환하므로, 문자열의 각 문자에 대해 개별적으로 접근하거나 수정할 작업을 할 때 유용하다.

## 사용 방법
- 매개변수를 필요로 하지 않고, 호출하는 문자열의 내용을 기반으로 `char` 배열을 생성한다.
- 반환된 배열은 문자열의 각 문자를 차례대로 포함한다.

## 예시
```java
public class Main {
    public static void main(String[] args) {
        String greeting = "Hello, World!";
        char[] characters = greeting.toCharArray();  // String을 char 배열로 변환
        
        // 변환된 char 배열의 내용을 출력
        for (char c : characters) {
            System.out.print(c + " ");
        }
    }
}
```