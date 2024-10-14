# @Enumerated
JPA에서 `enum` 타입의 필드를 데이터베이스에 저장할 때 사용되는 방식입니다. 이 어노테이션을 이용해 `enum` 값을 어떻게 저장하고 불러올지를 결정할 수 있습니다.

## 1. 종류
### 1.1 `EnumType.ORDINAL`
- `enum`의 순서를 정수 값으로 저장합니다.
- `enum` 값의 순서가 바뀌거나 값이 추가되면 데이터 의미가 달라질 수 있습니다.

### 1.2 `EnumType.STRING`
- `enum`의 이름을 문자열로 저장합니다.
- `enum`의 값이 `IN_PROGRESS`라면 해당 값이 그대로 `"IN_PROGRESS"`로 데이터베이스에 저장됩니다.
- `enum`에 값이 추가되거나 순서가 변경되어도 데이터 무결성이 보장됩니다. 즉, 안전합니다.

## 2. 장점
1. **가독성**: `enum`을 문자열로 저장할 경우 데이터베이스에서 값을 읽었을 때 값이 의미하는 바를 쉽게 알 수 있습니다. 예를 들어 `IN_PROGRESS`나 `COMPLETED` 같은 값은 바로 그 상태를 나타냅니다.
2. **안전성**: `EnumType.STRING`을 사용하면 `enum` 값이 추가되거나 순서가 바뀌어도 데이터의 의미가 변하지 않기 때문에 안정성을 보장합니다. 반면 `ORDINAL`은 순서가 바뀌면 기존 데이터와 충돌할 수 있습니다.
3. **유지보수**: `enum`을 사용하면 상태를 하나의 타입으로 관리할 수 있기 때문에 변경 사항을 관리하기 쉽습니다. 상태가 바뀌거나 추가되더라도 코드베이스에서 `enum`을 일관되게 사용할 수 있습니다.
4. **타입 안정성**: `enum`을 사용하면 허용되지 않은 상태 값이 들어갈 가능성을 막아줍니다. 상태가 정해진 `enum` 값으로만 제한되므로 잘못된 값이 들어갈 가능성을 줄여줍니다.

## 3. 사용 예시
```java
@Entity
public class ProductUserNotificationHistory {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    @Enumerated(EnumType.STRING)
    private NotificationStatus status;

    private LocalDateTime createdAt;

    // 기본 생성자 및 기타 메서드
}
```

