# Rest API 타입 정의
## 1. API 함수 타입 정의해보기
- 데이터의 유형에 맞게 인터페이스를 정의해서 사용해준다.
- 보통 데이터는 `[{}, {}, ...]` 형식으로 객체+배열 형식이 많다.
- `fetch()`의 경우 프로미스(Promise)를 리턴한다는 점을 알아야한다.
```typescript
const apiUrl: string = 'https://jsonplaceholder.typicode.com/todos';

interface Todo {
	userId: number;
	id: number;
	title: string;
	completed: boolean;
}

// TODO: 아래 API 함수의 타입을 정의해 보세요.
async function fetchTodos(): Promise<Todo[]> {
	const response = await fetch(apiUrl);
	const data = await response.json();
	return data;
}


fetchTodo().then(todos => todos[0].id);
```

## 2. ChatGPT를 이용한 타입 정의하기
- 챗지피티를 잘 사용하면 지난한 과정을 줄일 수 있다.
- 챗지피티에 예시 데이터를 프롬프트에 붙여넣어주고 '위 코드의 타입을 타입스크립트 코드로 작성해줘' 라는 식으로 요청하면 타입을 정의해준다.

## 3. TypeScript Fatigue
- 나는 애플리케이션 로직을 작성하고 있나?
- 타입에 의한 타입을 위한 타입 코드를 작성하고 있나?

## 4. 타입 단언으로 생기는 구멍들
- 타입 단언은 타입스크립트 컴파일러를 속이는 행위이다.
- 에러가 날 가능성이 높다.
- 하지만 현실적으로 안쓰기는 어렵다.
- 런타임 오류에 주의해야 한다.

```typescript
function fetchProduct() {
	// ...
}

const product = fetchProduct() as Product;
product.getId(); // 에러 발생 확률 높음
```

```typescript
interface Developer {
	name: string;
	coding: () => void;
}

const capt = {
	name: '캡틴'
} as Developer;
capt.coding(); // 에러 발생
```