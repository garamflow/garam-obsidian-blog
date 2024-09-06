# Lombok에 대하여
- 롬복은 아래와 같은 순서로 코드를 만든다.

1. java 컴파일러가 소스파일을 파싱해 AST 트리를 만든다.
2. Lombok은 AnnotationProcessor에 따라 AST트리를 동적으로 수정하고 새 노드를 추가하고 마지막으로 바이트 코드를 분석 및 생성한다.
3. 최종적으로 자바 컴파일러는 Lombok Annotation Processor에 의해 수정된 AST를 기반으로 Byte Code를 생성한다.