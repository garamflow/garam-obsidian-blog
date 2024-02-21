# @Builder
## 1) `@Builder`란?
- Lombok 라이브러리에 속한 어노테이션이다.
- 빌더 패턴을 구현할 때 사용된다.
- 빌더 패턴은 복잡한 객체를 단계별로 구축할 수 있도록 하는 디자인 패턴이다.
	- 매개변수를 가진 객체를 생성할 때, 일부 매개변수에 대해 선택적인 값을 설정할 때 유용하다.

## 2) `@Builder`의 기본 작동 방식
- 클래스, 생성자, 메소드에 적용 가능하다.
- 해당 타입의 인스턴스를 생성하기 위한 API를 제공한다.
### 사용 예시
```java
import lombok.Builder;
import lombok.Data;

@Data
@Builder
public class Product {
    private final int id;
    private final String name;
    private final String description;
    private final double price;
    private final boolean inStock;
}

// 객체 생성 예시
Product product = Product.builder()
                         .id(1)
                         .name("Coffee")
                         .description("A cup of coffee")
                         .price(2.99)
                         .inStock(true)
                         .build();
```

## 3) `@Builder`의 주요 특징
### (1) 체이닝 메소드 호출
- 객체의 필드 값을 설정하기 위한 메소드를 연속적으로 호출할 수 있다.
- 코드의 가독성을 높이며, 객체 생성 과정을 보다 명확하게 만들어준다.

### (2) 불변성 (Immutability)
- 빌더 패턴은 객체의 불변성을 쉽게 구현할 수 있게 해준다.
- 한번 객체가 생성되면, 그 상태를 변경할 수 없게 만들 수 있다.

### (3) 선택적 매개변수
- 객체를 생성할 때 모든 필드를 명시적으로 설정할 필요가 없다.
- 필요한 필드만 설정하고 나머지는 기본값을 사용하거나 설정하지 않을 수 있다.

## 4) 사용 시 고려사항
### (1) 기본값 설정
- `@Builder`와 함께 `@Builder.Default`를 사용하여 필드에 기본값을 설정할 수 있다.
- 선택적 매개변수에 대해 기본값을 제공하고자 할 때 유용하다.

### (2) 커스텀 빌더
- 생성된 빌더 클래스를 직접 수정하거나 확장해야 할 필요가 있을 수 있을 때, Lombok은 `@Builder`를 사용자 정의하기 위한 여러 옵션을 제공한다.

## 5) `@Builder.Default`
- `@Builder.Default`는 `@Builder`를 사용하여 객체를 생성할 때 필드에 기본 값을 설정하는 데 사용된다.
- @Builder.Default는 특정 필드에 기본값을 명시적으로 지정하고자 할 때 필드 레벨에서 사용됩니다. 이를 통해 객체 생성 시 해당 필드가 명시적으로 값이 할당되지 않았을 경우, 지정한 기본값을 자동으로 사용하게 합니다.

사용 예시

import lombok.Data;
import lombok.Builder;
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class ExampleClass {
    private int id;
    private String name;
    @Builder.Default
    private boolean active = true; // 기본값으로 true 설정
}

위 예시에서는 ExampleClass에 대해 @Data를 사용하여 기본적인 메소드들을 자동으로 생성하고, @Builder와 @Builder.Default를 사용하여 객체 생성 시 active 필드에 기본값으로 true를 설정하게 합니다.

언제 사용하는가?


	•	@Builder.Default는 객체 생성 시 특정 필드에 기본값을 제공하고자 할 때 사용됩니다. 이는 불변 객체 생성 또는 복잡한 객체 생성에 있어서 유연성과 명확성을 제공합니다.

Lombok을 사용하면 개발자는 반복적인 코드 작성으로부터 해방되어, 더 중요한 로직에 집중할 수 있습니다. 단, Lombok은 컴파일 시에 코드를 조작하기 때문에 IDE나 빌드 도구에서 추가적인 설정이 필요할 수 있습니다.