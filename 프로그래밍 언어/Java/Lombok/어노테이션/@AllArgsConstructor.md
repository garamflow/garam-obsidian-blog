# @AllArgsConstructor
## 1) `@AllArgsConstructor` 란?
- Lombok 라이브러리에서 제공하는 어노테이션이다.
- 클래스에 선언된 모든 필드를 인자로 받는 생성자를 자동으로 생성해준다.
- 클래스에 적용하면, 클래스의 모든 필드를 초기화하는 생성자를 직접 작성하지 않아도 Lombok이 컴파일 시점에 해당 생성자를 자동으로 추가해준다.

## 2) 사용 예시
```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
public class Student {
    private String name;
    private int age;
    private String major;
}

----

// @AllArgsConstructor와 같은 효과
public Student(String name, int age, String major) {
    this.name = name;
    this.age = age;
    this.major = major;
}
```

## 3) 언제 사용하는가?
- 클래스의 모든 필드를 한 번에 초기화해야 할 때 사용한다.
	- 객체를 생성할 때 모든 필드에 값을 할당해야 하는 경우, `@AllArgsConstructor`를 사용하면 간편하게 생성자를 통해 이를 수행할 수 있다.
- 불변 객체를 생성할 때 사용한다.
	- 클래스의 필드를 `final`로 선언하고, `@AllArgsConstructor`를 사용하여 불변 객체를 쉽게 생성할 수 있다.
- DTO(Data Transfer Object)나 POJO(Plain Old Java Object)와 같이 데이터를 저장하는 용도의 간단한 클래스를 작성할 때 사용한다.
	- 이러한 클래스는 일반적으로 여러 필드를 가지고 있으며, `@AllArgsConstructor`를 사용하여 생성자 코드를 줄일 수 있다.

## 4) 사용 시 장점
- 클래스의 모든 필드를 초기화하는 생성자를 명시적으로 작성하지 않아도 되므로, 코드의 양을 줄이고 가독성을 높일 수 있다.
- 클래스의 필드가 변경될 때마다 생성자를 수동으로 수정하는 번거로움을 줄일 수 있다.

## 5) 주의사항
- 모든 필드를 초기화하는 생성자가 항상 적절한 것은 아니다.
	- 특정 필드에 대해 기본값을 사용하고 싶은 경우나, 일부 필드만 초기화하고 싶은 경우에는 `@AllArgsConstructor` 대신 `@RequiredArgsConstructor`나 `@NoArgsConstructor`와 같은 다른 Lombok 어노테이션을 고려할 수 있다.