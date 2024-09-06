# @NoArgsConstructor
## 1) `@NoArgsConstructor` 란?
- Lombok 라이브러리에서 제공하는 어노테이션이다.
- 매개변수가 없는 기본 생성자 (default constructor)를 클래스에 자동으로 추가한다.
- 클래스에 명시적으로 매개변수 없는 생성자를 직접 작성하지 않아도 Lombok이 컴파일 시점에 해당 생성자를 자동으로 추가해준다.

## 2) 사용 예시
```java
import lombok.NoArgsConstructor;

@NoArgsConstructor
public class ExampleClass {
    private int someField;
    private String anotherField;
}

// @NoArgsConstructor와 동일한 효과
public ExampleClass() {
}
```

## 3) 언제 사용하는가?
- JPA 엔티티 클래스에서 사용한다.
	- JPA 스펙에서는 엔티티 클래스에 매개변수 없는 기본 생성자를 요구한다.
	- `@NoArgsConstructor`를 사용하여 이 요구 사항을 쉽게 충족시킬 수 있다.
- 빈 클래스 생성 필요 시 사용한다.
	- Spring 프레임워크와 같은 컨테이너에서 관리되는 빈을 정의할 때, 매개변수 없는 생성자를 통해 인스턴스를 생성할 수 있어야 한다.
- 데이터 바인딩에 사용한다.
	- JSON/XML과 같은 외부 데이터 포맷을 객체로 변환할 때, 매개변수 없는 생성자를 사용하여 객체 인스턴스를 생성하는 라이브러리가 많다.

## 4) 사용 시 장점
- 클래스에 다른 생성자들이 정의되어 있어도 매개변수 없는 기본 생성자를 쉽게 추가할 수 있다.
- 코드의 양을 줄이고 가독성을 높일 수 있다.
- JPA, Spring, 데이터 바인딩 라이브러리 등에서 요구하는 기본 생성자를 간편하게 제공할 수 있다.

## 5) 주의사항
- `final` 필드가 있는 클래스에 `@NoArgsConstructor`를 사용하면, 해당 필드들은 초기화될 수 없다.
	- 이 경우, Lombok은 컴파일 에러를 발생시키거나, `final` 필드를 초기화하지 않는 기본 생성자를 생성할 수 있다.
	- 따라서 `final` 필드를 가진 클래스에서는 `@NoArgsConstructor` 사용에 주의가 필요하다.
- `@NoArgsConstructor`가 생성하는 기본 생성자는 `protected` 또는 `private`과 같은 다른 접근 수준을 가질 수 있도록 설정할 수 있다.(`force = true` 옵션 사용)
	- 이러한 세부적인 설정을 통해 클래스의 인스턴스 생성 방식을 더 세밀하게 제어할 수 있다.