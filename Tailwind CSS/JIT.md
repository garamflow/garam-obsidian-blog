# JIT
## 1. JIT (Just-in-time Compiler)
- Tailwind CSS는 컴파일러와 같은 역할을 한다.
- 파일을 저장할 때마다 스캔해서 class name들을 추출하고 실제로 CSS 코드로 변환시킨다.
- `tailwind.config.ts`가 class name의 위치를 알고 있어서 컴파일러가 경로들을 검색하고 변환시킨다.
- 원하는 값들을 지정해두고

## 2. Directives
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

.btn {
	@apply w-full bg-black h-10
}

@layer base {
	a {
		@apply text-blue-500;
	}
}
```
- 컴파일러가 생성된 CSS를 어디에 두냐는 것을 알 수  있는 부분이다.
- utilities directive
	- 우리가 className에 적은 것을 컴파일러가 변환시키고, 그 코드들을 넣는 plcaholder이다.
- base directive
	- 모든 base style이 담겨져 있다.
	- reset, 기본 값들을 설정하는 곳
- apply directive
	- class name들을 CSS 코드에서 사용할 수 있게 해준다.
	- style을 재사용할 수 있다.
- layer directive
	- base, utilities 등의 layer를 확장하고 싶을 때 사용한다.
- components directive

## 3. plugin
- 