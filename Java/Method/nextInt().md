# nextInt()
- Java에서 `Scanner` 클래스의 일부이다.
- 사용자로부터 입력받은 다음 정수를 반환한다.
- 콘솔 및 UI에서 사용자 입력을 받을 때, 사용되며 해당 메소드를 사용하기 위해서는 `Scanner` 객체를 생성해야 한다.

## 예시
```java
import java.util.Scanner;

public class Main() {
	public static void main(String[] args) {
		// Scanner 객체 생성
		Scanner scanner = new Scanner(System.in);

		// 사용자로부터 정수를 입력받는다.
		int number = scanner.nextInt();

		// 스캐너 사용이 끝났으므로 자원을 해제한다.
		scanner.close();
	}
}
```
- 정수를 제외한 문자열, 실수 등을 입력받으면 `InputMismatchException`을 발생시킨다.