# static 키워드는 왜 사용하며 단점은 무엇인가?
- static 키워드는 클래스의 인스턴스가 아닌 클래스에 속하며 클래스의 변수, 메서드 등을 공유하는데 사용된다.
- 이를 통해 해당 클래스로 만들어지는 객체 사이에서 중복되는 메서드, 속성을 효율적으로 정의할 때 쓰인다.
- 메모리의 효율성을 증가시킬 수 있다.
```java
...
public static void talk(Person a, Person b) {
	...
}

Person a = new Person();
Person b = new Person();
Person.talk(b, a);
```
- a나 b의 특정한 메소닥 아니라 Person끼리 대화하는 메서드라는 명시성을 지니게 된다.

## 단점
- 선언을 하자마자 메모리에 올라가게 된다.
	- 메모리가 낭비될 수 있다.
- Java
	- static을 사용하지 않은 변수는 heap에 할당되어서 GC가 메모리 관리차원에서 회수까지 한다.
	- static을 사용하면 MethodArea에 할당되어서 프로그램을 종료될 때 까진서 회수가 안된다.