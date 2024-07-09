# Node.js와 NPM
## 1. Node.js
- 브라우저 밖에서도 자바스크립트를 실행할 수 있는 환경을 말한다.

## 2. NPM (Node Package Manager)
- 명령어로 자바스크립트 라이브러리를 설치하고 관리할 수 있게 해주는 패키지 매니저이다.
- Node.js를 설치하면 자동으로 설치된다.

### 2.1 NPM 시작하기
#### NPM 설치된 지 확인하기
- Node.js를 설치하면 자동으로 NPM이 설치되어 있다.
- `npm -v`

#### NPM 초기화하기
- `npm init`
	- 생성되는 package.json 파일에 대한 정보를 입력할 수 있다.
- `npm init -y`
	- package.json 파일을 기본값으로 바로 생성해준다.

#### NPM으로 라이브러리 설치하기
- `npm install 라이브러리 이름`
	- = `npm i 라이브러리 이름`
- 라이브러리를 설치하면 `node_modules` 밑에 라이브러리가 설치된다.
- package.json의 `dependencies`에도 라이브러리 이름과 버전이 추가된다.

### 2.2 NPM을 사용하는 이유와 장점
- 이전에는 라이브러리를 관리하기도 어려웠고 협업할 때도 문제가 생겼다.
	- HTML에 `script`로 라이브러리들을 직접 넣어주기도 했다.
- NPM을 사용하면 package.json을 통해 간편하게 관리할 수 있다.
- 또한 라이브러리를 추가할 때도 CDN을 하나씩 검색해서 추가해줘야 했다.
- 하지만 NPM을 사용하면 필요한 라이브러리를 명령어로 바로 설치해줄 수 있다.

### 2.3 NPM 제거, 전역 설치
#### 제거 명령어
- `npm uninsall 라이브러리 이름`
- 설치된 라이브러리가 `node_modules`와 package.json에서 제거된다.

#### 전역 설치 명령어
- `npm install 라이브러리 이름 --gloabal`
	- = `npm i 라이브러리 이름 -g`
- 전역 설치는 OS별로 특정 경로로 설치된다.
- 시스템 레벨에서 사용하는 라이브러리들을 전역으로 설치하곤 한다.
```
# window
%USERPROFILE%\AppData\Roaming\npm\node_modules

# mac
/usr/local/lib/node_modules
```

### 2.4 NPM 지역 설치
- 지역 설치에 자주 사용되는 옵션은 두 개가 있다.
```shell
# dependencies
npm install jquery --save-prod
= npm i jquery

# devDependencies
npm install jquery --save-dev
= npm i jquery -D
```

### 2.5 dependencies vs devDependencies
- denpendencies는 애플리케이션 로직과 직접적으로 연관이 있는 라이브러리이다.
	- 배포용 라이브러리
	- react, vue, chart, jquery, ...
- devDependencies는 개발 시 도움을 주는 보조 라이브러리이다.
	- 개발용 라이브러리
	- webpack, sass, eslint, ...