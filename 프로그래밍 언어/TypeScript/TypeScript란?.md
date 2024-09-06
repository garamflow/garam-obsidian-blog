# TypeScript 란?
- 자바스크립트에 타입을 부여한 언어이다.
```typescript
const message: string = 'hi';

function sum(a: number, b: number): number {
	return a + b;
}
```

## 왜 타입스크립트를 사용할까?
### 1. 사용자 경험
- 실행 시점의 에러를 어느정도 미리 잡아준다.
- 아래와 같은 경우에 사용자에게 노출되는 에러 메시지가 줄어든다.

```javascript
function sum(a ,b) {
	return a + b;
}

sum(10, 20); // 30
sum(10, '20'); // '1020'
```

```typescript
function sum(a: number, b: number): number {
	return a + b;
}

sum(10, 20);
sum(10, '20'); // error
```

### 2 개발자 경험
- 코드 자동 완성, 코드 역할에 대한 정보 제공 등
- 아래와 같이 타입스크립트를 이용하면 타입 추론을 통해 자연스럽게 코드 역할과 설명을 알 수 있고, 자동완성도 사용할 수 있다.

```typescript
const divElement = document.querySelector('div');
divElement?.메소드
```