# 스프링 탄생 배경과 Bean, Bean 컨테이너
## 1. 스프링 프레임워크
### 1) 스프링 프레임워크 등장 이유
- (1) 스프링 프레임워크 이전에는 EJB(Enterprise JavaBeans)가 있었다.
	- EJB는 애플리케이션 작성을 쉽게 해준다.
		- 쉽다 = 미들웨어보다는 쉽다 = 객관적인 난이도는 높았음
	- EJB는 선언적 프로그래밍 모델이다.
		- 선언적 프로그래밍 = 설정만 해두면 자동으로 해준다.
	- 트랜잭션, 보안, 분산컴퓨팅 등을 쉽게 할 수 있다.
	- EJB를 구동할 수 있는 Web Application Server가 등장한다.
- (2) Expert One-onOne: J2EE Design and Development 책 발간
	- Spring 소개
	- EJB가 했던 일을 더 간단한 Java Bean이 처리할 수 있게된다.

## 2. Bean이 무엇인가
- (1) Java에서 인스턴스 생성
	- `Book book = new Book();`
	- 프로그래머가 직접 인스턴스를 생성한다.
- (2) Bean은 컨테이너가 관리하는 객체
	- 객체의 생성주기를 컨테이너가 관리한다.
		- 객체를 싱글턴으로 만들 것인지, 프로토타입으로 만들 것인지 등

## 3. 스프링의 핵심 기능 1
- 관점 지향 컨테이너
	- Bean을 생성, 관리해준다.
	- 관점 지향(AOP, Aspect-Oriented Programing)

### 1) 사용자가 직접 인스턴스 생성
```java
public class Book {
	private String title; // title 인스턴스 field(속성)
	private int price; // price 인스턴스 field
	// 인스턴스 필드는 Book이라는 클래스의 인스턴스가 만들어져야 사용할 수 있다.

	// 생성자
	public Book(String title, int price) { // Book 클래스
		this.title = title;
		this.price = price;
	}

	public String getTitle() {
		this.title = title;
	}

	public String setTitle(String title) {
		this.title = title;
	}

	public int getPrice() {
		this.price = price;
	}

	public int setPrice(int price) {
		this.price = price;
	}
}
```

```java
// Book 클래스의 인스턴스 생성
Book book1 = new Book("자바", 2000);
```
1. `new Book("자바", 2000)`
	- 생성자
	- 생성자가 호출되면 Heap 메모리에 인스턴스가 생성된다.
2. book1 은 1번에서 생성한 인스턴스를 참조한다.
	- book1은 참조 변수

### 2) 스프링
```java
public class ApplicationContext {
	Properties props;
	public ApplicationContext() {
		Properties props = new Properties();
		try {
			props.load(new FileInputStream("src/main/resources/Beans.properties"));
		} catch (IOEception e) {
			e.printStackTrace();
		}
	}

	public Object getBean(String id) {
		String className = props.getProperty(id);
		// class name에 해당하는 무자열을 가지고 인스턴스를 생성할 수 있다.
		// Class.forName(className)은 CLASSPATH부터 className에 해당하는 클래스를 찾은 후
		// 그 클래스 정보를 반환한다.
		Class clazz = class.forName(className);

		// ClassLoader를 이용한 인스턴스 생성. 기본 생성자가 있어야 한다.
		Object o = clazz.getInstance(); // clazz정보를 이용해 인스턴스를 생성한다.
		return o;
	}
}
```

- Bean을 만들 때 규칙
	- 기본 생성자가 있어야 한다.
		- classLoader가 인스턴스 만들기 쉽다.

## 3. Bean은 관리된다는 말은 무슨 의미일까?
