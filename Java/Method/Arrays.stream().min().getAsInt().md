# Arrays.stream().min().getAsInt()
- 스트림 API의 일부로, 스트림에 있는 요소들 중 가장 작은 값을 찾은 다음 그 값을 `int` 형태로 반환하는 과정을 수행한다.
- 주로 `int` 데이터를 다루는 `IntStream` 과 같은 스트림에서 사용된다.

## 과정
### stream().min()
- `min()` 메서드는 스트림의 요소 중 최소값을 찾기 위해 사용된다.
- `IntStream`, `LongStream`, `DoubleStream` 같은 기본형 특수화 스트림에서는 `min()` 메서드가 추가 매개변수 없이 사용될 수 있으며, 자동으로 요소들을 자연 순서대로 비교한다.
- 이 메서드는 `OptionalInt`, `OptionalLong`, `OptionalDouble` 등을 반환한다.
	- 최소값이 존재할 수도 있고, 스트림이 비어 있을 경우 존재하지 않을 수도 있음을 안전하게 처리하기 위함입니다.
- `Comparator` 인터페이스를 이용해서 요소들을 비교하고, 스트림의 요소 중 최소값을 선택한다.

### getAsInt()
- `OptionalInt` 객체에서 `getAsInt()` 메서드를 호출하면, 해당 객체가 포함하고 있는 값을 `int` 형태로 반환한다.
- 이 메서드를 호출하기 전에는 반드시 `isPresent()` 메서드를 사용하여 값의 존재 여부를 확인해야 한다. 만약 `OptionalInt`가 값을 포함하고 있지 않은 상태에서 `getAsInt()`를 호출하면 `NoSuchElementException`이 발생할 수 있다.

## 사용법
```java
import java.util.Arrays;
import java.util.OptionalInt;

public class Main {
    public static void main(String[] args) {
        int[] numbers = {5, 3, 9, 1, 6};

        OptionalInt min = Arrays.stream(numbers).min();

        if (min.isPresent()) {
            System.out.println("The minimum value is: " + min.getAsInt());
        } else {
            System.out.println("Stream is empty");
        }
    }
}
```