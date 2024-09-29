# ThreadLocal
- Java에서 제공하는 클래스로, 각 스레드마다 고유한 변수를 가질 수 있도록 해주는 기능을 제공한다.
- 멀티스레드 환경에서 데이터를 안전하게 저장하고 사용할 수 있다.

## 개념 및 특징

1. **스레드별 독립적인 변수 저장**:
    - `ThreadLocal` 객체에 저장된 값은 각 스레드마다 독립적인 복사본을 가짐.
    - 여러 스레드가 동시에 같은 `ThreadLocal` 객체에 접근하더라도, 각 스레드는 자신만의 값을 사용하게 됨. 이를 통해 멀티스레드 환경에서 동시성 문제를 방지할 수 있음.
2. **사용 예**:
    - 멀티스레드 환경에서 **공유되지 않아야 할 데이터**(예: 사용자 인증 정보, 트랜잭션 컨텍스트, 세션 데이터 등)를 저장할 때 사용됨.
    - `ThreadLocal`은 스레드가 종료될 때까지 유지되는 스레드 전용 저장소 역할을 함.

## 사용 방법
- `ThreadLocal`을 사용하기 위해서는 아래와 같은 단계를 따름:
1. **ThreadLocal 객체 생성**:
```java
private static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);
```
	-  `ThreadLocal.withInitial()` 메서드를 사용해 초기값을 설정할 수 있음.
	- `withInitial()`을 통해 초기 값을 지정하면 스레드가 처음 접근할 때 해당 값이 설정됨.


2. **값 설정 및 가져오기**:
```java
threadLocal.set(100); // 현재 스레드의 값 설정
Integer value = threadLocal.get(); // 현재 스레드의 값 가져오기
threadLocal.remove(); // 현재 스레드의 값 제거
```
	- `set()`: 현재 스레드에 특정 값을 저장함.
	- `get()`: 현재 스레드의 값을 가져옴.
	- `remove()`: 현재 스레드의 값이 더 이상 필요하지 않을 경우 제거하여 메모리 누수를 방지.

## 예제 코드
```java
public class ThreadLocalExample {
    private static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 0);

    public static void main(String[] args) {
        Runnable task = () -> {
            int value = threadLocal.get();
            threadLocal.set(value + 1);
            System.out.println(Thread.currentThread().getName() + ": " + threadLocal.get());
        };

        Thread thread1 = new Thread(task, "Thread-1");
        Thread thread2 = new Thread(task, "Thread-2");

        thread1.start();
        thread2.start();
    }
}
```

### 설명
1. **`ThreadLocal<Integer> threadLocal`**:
    - 스레드별로 독립적인 정수를 저장하는 `ThreadLocal` 객체를 정의함.
    - 초기값을 `0`으로 설정.
2. **각 스레드가 값을 설정하고 출력**:
    - `task`를 실행하는 각 스레드는 자기만의 `threadLocal` 값을 가짐.
    - `set()`을 통해 값을 1 증가시켜 저장한 후 출력함.
    - `Thread-1`과 `Thread-2`는 독립적인 값을 다루므로 서로의 값을 공유하지 않음.

## 주요 사용 사례

1. **트랜잭션 관리**:
    - 트랜잭션 컨텍스트와 같은 정보는 스레드별로 분리되어야 하므로 `ThreadLocal`로 관리.
2. **세션 정보 유지**:
    - 요청-응답 처리 시, 사용자 세션 정보나 요청 관련 데이터도 스레드별로 유지해야 할 때 사용.
3. **로그 처리**:
    - 로깅 시, 요청별로 구분된 로그 컨텍스트를 `ThreadLocal`에 저장하여 각 스레드가 독립적인 로그를 작성할 수 있도록 함.

## 주의사항
1. **메모리 누수**:
    - `ThreadLocal`에 저장된 객체는 스레드가 종료되지 않는 한 계속 참조되므로, 사용 후 `remove()`를 호출해주는 것이 좋음.
    - 특히, 서블릿이나 스레드 풀과 같이 스레드가 재사용되는 환경에서는 꼭 `remove()`로 값을 제거하여 메모리 누수를 방지해야 함.
2. **복잡성 증가**:
    - `ThreadLocal`을 남용하면 코드의 이해가 어려워지고 유지보수에 문제가 생길 수 있음. 필요할 때만 신중하게 사용해야 함.