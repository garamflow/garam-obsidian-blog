# Spring Boot + MySQL + Redis
## 1. 의존성  설치하기
- 의존성 필요한 것들 설치하기
	- Spring Boot
	- JPA
	- MySQL
	- Redis
	- ...

## 2. 설정하기
### 2.1 application.yml
```yaml
spring:
	datasource:
		url: jdbc:mysql://my-db:3306/mydb
		username: root
		password: pwd1234
		dirver-class-name: com.mysql.cj.jdbc.Driver
	data:
		redis:
			host: localhost
			port: 6379
```

### 2.2 RedisConfig
```java
@Configuration
public class RedisConfig {

  @Bean
  public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(connectionFactory);
    template.setKeySerializer(new StringRedisSerializer());
    template.setValueSerializer(new GenericJackson2JsonRedisSerializer());
    return template;
  }
}
```

### 2.3 Redis 설정이 잘 되었는지 테스트하기위한 Controller
```java
@RestController
public class AppController {

  @Autowired
  private RedisTemplate<String, Object> redisTemplate;

  @GetMapping("/")
  public String home() {
    redisTemplate.opsForValue().set("abc", "def");
    return "Hello, World!";
  }
}
```

### 2.4 compose.yml
```yaml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
      my-cache-server:
        condition: service_healthy  
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd1234
      MYSQL_DATABASE: mydb
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping" ]
      interval: 5s
      retries: 10
  my-cache-server:
    image: redis
    ports:
      - 6379:6379
    healthcheck:
      test: [ "CMD", "redis-cli", "ping" ]
      interval: 5s
      retries: 10
```

## 3. Docker 컨테이너로 띄워보기
```bash
$ ./gradlew clean build
$ docker compose down
$ docker compose up --build -d
```

## 4. `Connection refused` 발생 시
- Redis와 연결이 안됐기 때문이다.
- applicayion.yml 파일을 수정해준다.

```yaml
spring:
  datasource:
    url: jdbc:mysql://my-db:3306/mydb
    username: root
    password: pwd1234
    driver-class-name: com.mysql.cj.jdbc.Driver
  data:
    redis:
      host: my-cache-server
      port: 6379
```
- 각 컨테이너는 각자의 네트워크를 가지고 있기 때문에, localhost가 아니라 Redis가 실행되고 있는 컨테이너로 통신을 해야 한다. Redis가 실행되고 있는 컨테이너의 주소는 service 이름으로 표현한다고 했다. compose.yml에서 Redis가 실행되고 있는 컨테이너의 service 이름을 my-cache-server라고 이름 붙였다.
- 이후 다시 빌드 후 compose down, compose up을 해주면 된다.