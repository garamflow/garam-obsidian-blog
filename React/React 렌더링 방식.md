# React 렌더링 방식

## 1. 브라우저는 어떻게 동작할까?

### 1.1 Critical Redering Path를 통해서 렌더링된다.
1. 브라우저가 HTML, CSS코드를 DOM, CSSOM로 변환한다.
	- DOM (Document Object Model, 문서 객체 모델): HTML을 브라우저가 해석하기 편한 방식으로 변환한 객체 트리
2. DOM과 CSSOM을 합쳐서 Render Tree를 만든다. 요소들의 배치와 모양, 스타일을 모두 갖고 있는 청사진이다.
3. Layout 과정. HTML 요소들이 어떤 위치에 어떤 사이즈로 등장할 것인지 정한다.
4. Painting 과정. 실제로 요소들을 그려낸다.
