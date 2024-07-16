# 렌더링 종류 - CSR, SSR, Hydration
- HTML + CSS + JS
	- 해당 파일들을 바탕으로 RealDOM을 그리게 된다.
- React.js
	- index.html이라는 빈 화면이 들어오고 script 태그를 통해서 리액트 코드가 담겨있는 js bundle을 불러온다.
	- 리액트 코드를 바탕으로 VitualDOM을 만들고 VirtualDOM을 바탕으로 RealDOM을 그린다.
- Next.js (PageRouter)
	- 서버에서 리액트 코드를 바탕으로 HTML 파일을 만들어낸다.
	- 화면이 보이고 리액트 코드들을 받아온다.
	- 받아온 HTML 요소들을 Hydration 해서 리액트화 시킨다.
		- 이전까지는 사용자가 클릭해도 반응이 없다가 리액트화가 되면 반응한다.
	- 그리고 이후 React.js 와 같이 VirtualDOM을 만들고 그걸 바탕으로 RealDOM을 그린다.
- Next.js (AppRouter)
	- PageRouter 의 문제점은 페이지의 요소들이 많으면 다운받고 js bundle을 다운받을 때 까지 Hydration이 홀딩된다.
	- 그래서 페이지를 클릭해도 반응이 없을 가능성이 있다.
	- AppRouter에서는 Streaming Server Rendering을 통해서 Hydration을 부분적으로 하게 된다.
	- 사용자가 

## 1. CSR


## 2. SSR

## 3. Hydration
