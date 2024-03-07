# @RequiredArgsConstructor
## 1) `@RequiredArgsConstructor` 란?
- Lombok 라이브러리에서 제공하는 어노테이션이다.
- `final`이나 `@NonNull` 어노테이션이 붙은 필드들을 인자로 받는 생성자를 자동으로 생성해준다.
- 해당 어노테이션을 클래스에 적용하면 명시적으로 생성자를 작성하지 않아도 Lombok이 컴파일 시점에 필요한 생성자를 생성해준다.

## 2) 사용 예시
```java
import lombok.NonNull;
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class ExampleClass {
    private final int someField;
    private final String anotherField;
    @NonNull
    private String nullableField;
}

// @RequiredArgsConstructor를 통해 생성되는 생성자
public ExampleClass(int someField, String anotherField, String nullableField) {
    if (nullableField == null) {
        throw new NullPointerException("nullableField is marked non-null but is null");
    }
    this.someField = someField;
    this.anotherField = anotherField;
    this.nullableField = nullableField;
}
```

## 3) 언제 사용하는가?
- 클래스가 하나 이상의 `final` 필드를 포함하고 있으며, 이 필드들을 초기화하기 위한 생성자가 필요한 경우
- 필드가 `@NonNull` 애노테이션으로 표시되어 있으며, 이 필드에 대한 null 체크를 자동으로 추가하고 싶은 경우
- 생성자 코드를 직접 작성하는 것보다 코드를 간결하게 유지하고 싶은 경우

## 4) 사용 시 장점
- 코드의 반복을 줄이고, 생성자 코드를 자동으로 관리하여 코드의 가독성과 유지보수성을 향상시킨다.
- `final` 필드나 `@NonNull` 필드에 대한 생성자를 명시적으로 작성할 필요가 없어 개발 효율성이 증가한다.
- `@NonNull` 필드에 대해 자동으로 null 체크를 추가하여, NullPointerException을 방지하는 안전한 코드를 생성한다.