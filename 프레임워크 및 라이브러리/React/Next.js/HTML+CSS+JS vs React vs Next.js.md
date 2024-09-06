# HTML+CSS+JS vs React vs Next.js
## 1. HTML+CSS+JS
- 작은 프로젝트나 간단한 웹 페이지 제작에 알맞다.
- 단일 페이지 애플리케이션(SPA)을 구축하기는 어렵다.
- 결과물: HTML + CSS + JS
- 가장 빠르지만 큰 프로젝트 개발이 어렵다.

## 2. React
- SEO가 상관 없는 인터렉션이 많은 웹에서 자주 사용된다.
	- 어드민 페이지, B2B 페이지, Gmail, 지도 앱 등
- 결과물: JS 정적 파일 (+ HTML, CSS)
- 웹에서 앱처럼 UI 상호작용이 가능하다.
- 그러나 SEO가 불리하고 초기 JS 로딩이 느리다. (빈 화면이 보일 수 있음)

## 3. Next.js
- MPA (Multiple Page Application)
- React 기반 서버 사이드 렌더링(SSR) 및 정적 사이트 생성(Static Site Generation, SSG)을 지원하는 프레임워크이다.
- SEO 최적화를 할 수 있고 초기 로딩 속도가 향상된다.
- FullStack 가능하다. (서버 API, DB 조회 등)
- 결과물: 서버 Application (+ HTML 정적 파일)
- 웹과 서버 전반에 대한 지식이 필요하다.