# filter()
- 주로 `Stream` API를 사용할 때 언급된다.
	- 컬렉션, 배열 또는 다른 연속된 데이터 소스에 대해 선언적으로 처리를 수행할 수 있는 방법을 제공한다.
- `filter()` 메서드는 이런 스트림의 중간 연산 중 하나로, 주어진 조건에 맞는 요소만을 선택하여 새로운 스트림을 생성하는 데 사용된다.

## 사용법
- `Predicate<T>` 인터페이스를 구현하는 람다 표현식을 인자로 받으며, 스트림의 각 요소에 적용되어 `true`를 반환하는 요소만을 포함하는 새로운 스트림을 생성한다.
- 중간 연산이므로 다른 스트림 연산과 연결될 수 있으며, 최종 연산 호출될 때까지 실제 필터링 작업이 수행되지 않는다.

## 예시
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FilterExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
        
        List<Integer> evenNumbers = numbers.stream()  // 스트림 생성
                                            .filter(n -> n % 2 == 0)  // 짝수 조건으로 필터링
                                            .collect(Collectors.toList());  // 결과를 리스트로 수집

        System.out.println(evenNumbers);  // 출력: [2, 4, 6]
    }
}
```