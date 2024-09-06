# 캐스팅 (Casting)
- 데이터 타입을 변환하는 것을 말하며, 형변환이라고도 말한다.
- 자바에서 상속 관계가 있는 특정 객체는 상황에 따라 더 넓은 범위로 해석(업캐스팅, upcasting)될 수도, 좁은 범위로 해석(다운캐스팅, downcasting)될 수도 있다.
- 주로 기본 타입의 변수 또는 객체 사이에서 사용된다.
  
## 1) 업캐스팅 (Upcasting)
- 서브 클래스의 객체를 슈퍼 클래스 타입으로 변환하는 것을 의미한다.
- 이 과정은 자동으로 일어나며, 명시적으로 캐스팅을 할 필요가 없다.
- 업캐스팅을 통해, 서브 클래스 객체를 슈퍼 클래스 타입의 참조 변수에 할당할 수 있다.
	- 이렇게 하면 슈퍼 클래스의 메서드와 필드에만 접근할 수 있으며, 서브 클래스에 추가된 메서드와 필드에는 접근할 수 없다.
```java
class Animal {
    void walk() {
        System.out.println("Animal walks");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Animal animal = dog; // 업캐스팅, 명시적 캐스팅 필요 없음
        animal.walk(); // 가능
        // animal.bark(); // 컴파일 에러
    }
}
```

## 2) 다운캐스팅 (Downcasting)
- 다운캐스팅은 슈퍼 클래스 타입의 객체를 서브 클래스 타입으로 변환하는 것을 의미한다.
- 다운캐스팅은 명시적으로 캐스팅 연산자를 사용해야 한다.
- 다운캐스팅을 잘못 사용하면, 실행 시간에 `ClassCastException`이 발생할 수 있다.
	- 따라서 다운캐스팅하기 전에 객체가 실제로 해당 서브 클래스 타입인지 확인하는 것이 좋다.
	- 이를 위해 `instanceof` 연산자를 사용할 수 있다.

```java
Animal animal = new Dog(); // 업캐스팅

if (animal instanceof Dog) {
    Dog dog = (Dog) animal; // 다운캐스팅, 명시적 캐스팅 필요
    dog.bark(); // 가능
}
```

## 3) 기본 타입 캐스팅
- Java에서는 또한 기본 타입(primitive types) 변수 사이에서 캐스팅을 할 수 있다.
- 더 넓은 범위의 타입으로 변환하는 것은 자동으로 일어난다.
	- (예: int에서 long으로)
- 더 좁은 범위의 타입으로 변환할 때는 데이터 손실이 발생할 수 있으므로 명시적으로 캐스팅해야 한다
	- (예: long에서 int로)

```java
int myInt = 10;
long myLong = myInt; // 자동 캐스팅
int myNewInt = (int) myLong; // 명시적 캐스팅 필요
```