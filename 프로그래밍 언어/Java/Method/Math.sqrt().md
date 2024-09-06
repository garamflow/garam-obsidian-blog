# Math.sqrt()
- 어떤 수의 제곱근을 계산할 수 있다.
- `double` 타입을 반환하며, 매개변수로도 `double` 타입을 받는다.
	- 정수에 대해 구하려면 적절한 타입 변환이 필요하다.

## 예시
```java
public class Main {
    public static void main(String[] args) {
        double result1 = Math.sqrt(25);  // 5.0
        double result2 = Math.sqrt(36);  // 6.0
        double result3 = Math.sqrt(49);  // 7.0

        System.out.println("The square root of 25 is " + result1);
        System.out.println("The square root of 36 is " + result2);
        System.out.println("The square root of 49 is " + result3);
    }
}
```

## 사용법
- 약수를 구할 때 제곱근을 이용한다.
	- 약수들이 쌍으로 존재하기 때문이다.
	- `n`의 약수가 `n`의 제곱근보다 크다면, 그에 상응하는 쌍의 약수는 반드시 `n`의 제곱근보다 작다.
	- 즉, `n`의 제곱근까지만 약수를 검사하면, 그 이상의 수에 대해서는 검사할 필요가 없다.
- 해당 방법으로 복잡성을 O(n^1/2) 로 줄일 수 있다.