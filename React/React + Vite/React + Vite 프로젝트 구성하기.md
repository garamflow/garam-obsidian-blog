# React + Vite 프로젝트 구성하기
## 1. vite를 통해 리액트 프로젝트 생성하기
- 아래 명령어를 통해 프로젝트를 설치한다.
```shell
npm create vite@latest
```
- 프로젝트 이름, 프레임워크, 언어까지 선택하면 생성된다.

## 2. 프로젝트 구성 알아보기
### package.json
- npm으로 프로젝트 생성 시 생성되는 라이브러리 관리 파일
```json
{
  "name": "react-todo",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.3.1",
    "react-dom": "^18.3.1"
  },
  "devDependencies": {
    "@types/react": "^18.3.3",
    "@types/react-dom": "^18.3.0",
    "@vitejs/plugin-react": "^4.3.1",
    "eslint": "^8.57.0",
    "eslint-plugin-react": "^7.34.2",
    "eslint-plugin-react-hooks": "^4.6.2",
    "eslint-plugin-react-refresh": "^0.4.7",
    "vite": "^5.3.1"
  }
}
```
- `scripts`
	- 프로젝트에서 사용하는 명령어 모음
	- 사용자가 원하는대로 수정할 수 있다.
	- `npm run dev`, `npm run build` 등의 명령어를 이용해서 vite로 개발 서버를 실행하거나 빌드시킨다.
- `dependencies`
	- 프로젝트에 생성된 라이브러리 목록
	- 빌드 시 포함되는 라이브러리이다.
- `devDependencies`
	- 개발할 때 필요한 구성환경라이브러리 정보이다.
	- 코드나 빌드와 같은 곳에 관련있다.

### node_modules, pakage-lock.json
- `npm install`
	- 해당 명령어를 입력하면 `dependencies`와 `devDependencies`에 있는 라이브러리를 npm에서 받아온다.
- node_modules
	- 설치된 파일들과 라이브러리들이 모여있는 곳
- package-lock.json
	- 파일들의 연관관계를 관리하는 파일

## 3. 프로젝트 진입점
### main.jsx
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
	<React.StrictMode>
	<App />
	</React.StrictMode>,
)
```
- `root`라는 ID를 찾아서 리액트가 해당 컴포넌트를 보여준다.
	- `root`는 index.html의 `div` 태그의 아이디이다. 즉, 그곳에 리액트 내용물을 그린다는 의미이다.
- `<React.StrictMode>`
	- 개발 시 더 엄격한 모드 적용
- `<App />`
	- 실질적으로 작업할 앱 컴포넌트이다.
	- 사실상 프로젝트 시작 시 가장 먼저 건들여야할 컴포넌트이다.

## 4. 컴포넌트와 jsx
- 리액트의 컴포넌트 파일은 `App.jsx`와 같이 첫번째 단어를 대문자로 쓴다.
- `.jsx`는 자바스크립트 익스텐션이다.
	- 자바스크립트의 return문 안에 HTML, CSS 문법을 사용할 수 있다.
	- 자바스크립트 문법과 HTML, CSS를 혼합해서 화면을 구성할 수 있다.