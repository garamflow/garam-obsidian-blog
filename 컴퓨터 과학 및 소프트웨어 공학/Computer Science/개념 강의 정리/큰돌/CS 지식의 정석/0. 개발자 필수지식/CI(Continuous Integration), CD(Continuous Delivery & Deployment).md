# CI(Continuous Integration), CD(Continuous Delivery & Deployment)
- 개발자가 코드를 짜면 그 다음에는 지속적으로 코드를 합치고 코드를 배포해야 한다.
- 이를 CI/CD(Continuous Integration/Delivery & Deployment) 라고 한다.

## 1) CI/CD는 왜 필요할까?
- 여러 명의 개발자가 코드를 합치고 배포를 계속해서 시스템 없이 수동으로 한다면 여러가지 문제가 발생한다.

## 2) CI/CD 파이프라인
- 코드 구축부터 시작해서 배포까지 일련의 과정을 CI/CD 파이프라인이라고 한다.
- 파이프라인을 통해 코드 배포까지 체계적으로 만들 수 있고 테스트를 강제할 수 있다.
	- 파이프라인 자체에 테스트가 있어서 테스트 없이는 코드 머지 자체를 안되게 만들 수 있다.

### (1) CI (Continuous Integration)
- 코드를 빌드하고 테스트하고 합친다.
- Build -> Test -> Merge

#### 빌드 (Build)
- 대표적으로 웹팩(Webpack)이 있다.
- 웹 브라우저에서 사용할 수 없는 파일들을 웹 브라우저에서 사용할 수 있는 html, css, js로 바꿔준다.
#### 테스트 (Test)
- 함수 등 작은 단위를 테스팅하는 단위테스트, 모듈을 통합할 때 테스트하는 통합테스트, 사용자가 서비스를 사용하는 상황을 가정해서 테스트하는 엔드투엔드테스트가 대표적이다.
- 테스트를 위한 대표적인 프레임워크는 mochas가 있다.
#### 머지 (Merge)
- git이나 svn을 통해서 코드를 합친다.
- 요즘엔 보통 git을 사용한다.
- 작은 issue 단위를 기반으로 머지를 하게 된다.

### (2) CD (Continuous Delivery)
- 해당 레퍼지토리에 릴리스한다.
- Automatically release to repository

### (3) CD (Continuou Deployment)
- 프로덕션, 실제 서비스에 배포한다.
- Ayutomatically deploy to production

#### 배포 (Deploy)
- 그저 사용자를 위한 서비스를 배포할 수도 있지만 그뿐만 아니라 QA 엔지니어나 관리자 페이지를 위한 배포, 데이터웨어하우스로부터 데이터를 가공해서 백엔드 개발자를 위한 배포 등을 포함한다.

### (4) 툴
- giuthub action, genkins, circle ci가 유명하며 heroku를 이용해 CI, CD 설정 없이 자동으로도 가능하다.
	- heroku + github action도 가능하다.