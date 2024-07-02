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

## 3. 프로젝트 진입점, 컴포넌트 알아보기
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
- root라는 ID를 찾아서 리액트가 해당 컴포넌트를 보여준다.
- 