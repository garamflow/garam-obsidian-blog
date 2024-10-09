# @RequestParam vs @RequestBody vs @RequestPart
Spring MVC에서 HTTP 요청 데이터를 컨트롤러 메서드의 파라미터로 바인딩하는 방식입니다.
각각의 어노테이션이 요청 데이터를 처리하는 방식이 다릅니다.

## 1. @RequestParam
- **역할**: HTTP 요청의 **쿼리 스트링** 또는 **폼 데이터**의 파라미터 값을 매핑하는 데 사용됩니다.
- **사용 사례**: `GET` 요청에서 URL의 쿼리 스트링, 또는 `POST` 요청에서 **폼 필드** 데이터를 처리할 때 사용합니다.
- **형식**: `x-www-form-urlencoded` 형식의 데이터를 처리합니다.

### 예시
```java
@GetMapping("/greet")
public String greet(@RequestParam String name) {
    return "Hello, " + name;
}
```
- URL 예시: `/greet?name=John`
	- `@RequestParam`은 `name=John` 부분을 매핑하여 컨트롤러 메서드에 전달합니다.

### 주요 특징
- 필수/선택 여부 설정 가능: `@RequestParam(required = false)`로 필수 여부 설정 가능.
- 기본값 설정 가능: `@RequestParam(defaultValue = "Guest")`로 기본값 설정 가능.

## 2. @RequestBody
- **역할**: HTTP 요청의 **본문(body)** 에 있는 데이터를 컨트롤러 메서드의 파라미터로 바인딩하는 데 사용됩니다.
- **사용 사례**: 주로 `POST`, `PUT`, `PATCH` 요청에서 **JSON, XML, 또는 다른 형식의 데이터를 처리**할 때 사용합니다.
- **형식**: JSON, XML 등 직렬화된 데이터 구조를 처리합니다. (Spring은 자동으로 객체로 변환해줍니다.)

### 예시
```java
@PostMapping("/users")
public User createUser(@RequestBody User user) {
    // JSON 본문이 User 객체로 자동 변환됨
    return userService.save(user);
}
```

```json
{
  "name": "John",
  "age": 25
}
```

### 주요 특징
- Spring은 **JSON** 데이터는 Jackson 라이브러리 등을 이용해 **자동으로 객체로 변환**합니다.
- **전체 HTTP 요청 본문**을 파라미터로 처리합니다.

## 3. @RequestPart
- **역할**: HTTP 요청에서 **멀티파트 요청**(파일 업로드 등)을 처리할 때 사용됩니다.
- **사용 사례**: 파일 업로드를 포함한 **멀티파트 요청**에서 파일 또는 데이터를 바인딩할 때 사용합니다.
- **형식**: `multipart/form-data` 형식을 처리합니다. 멀티파트 요청에서 **파일**이나 **비파일 데이터**를 각각 처리할 수 있습니다.

### 예시
```java
@PostMapping("/upload")
public String uploadFile(@RequestPart("file") MultipartFile file, 
                         @RequestPart("metadata") String metadata) {
    // 파일 및 추가 데이터를 처리
    return "File uploaded: " + file.getOriginalFilename() + ", metadata: " + metadata;
}
```
- **요청 예시**:
	- `file`: 업로드된 파일.
	- `metadata`: 추가적인 비파일 데이터.

### 주요 특징
- **파일 및 다른 요청 부분을 별도로 처리**할 수 있습니다.
- **MultipartFile**과 같은 파일 데이터도 처리 가능합니다.

## 4. 세가지 어노테이션의 차이점 요약
| 어노테이션               | 용도                                | 주로 사용되는 요청 방식           | 데이터 처리 방식                             |
| ------------------- | --------------------------------- | ----------------------- | ------------------------------------- |
| **`@RequestParam`** | **쿼리 스트링** 또는 **폼 데이터**를 파라미터로 받음 | `GET`, `POST`, `PUT`    | **쿼리 스트링** 또는 `x-www-form-urlencoded` |
| **`@RequestBody`**  | **HTTP 본문**에 있는 JSON, XML 데이터를 처리 | `POST`, `PUT`, `PATCH`  | **JSON, XML 등 직렬화된 데이터**              |
| **`@RequestPart`**  | **멀티파트** 요청의 부분 데이터를 처리 (파일 업로드)  | `POST`, `PUT` (멀티파트 요청) | **multipart/form-data**               |
### 실제 사용 시 고려할 점
- **`@RequestParam`**은 주로 URL 쿼리 파라미터 또는 `POST` 요청의 **폼 데이터를** 처리할 때 적합합니다.
- **`@RequestBody`**는 주로 **JSON**이나 **XML**을 통해 전송된 복잡한 데이터 구조를 객체로 변환하는 데 적합합니다.
- **`@RequestPart`**는 **파일 업로드** 같은 **멀티파트 데이터**를 처리할 때 유용합니다.