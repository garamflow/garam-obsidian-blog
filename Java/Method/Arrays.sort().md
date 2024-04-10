# Arrays.sort()
- `Arrays` 클래스에서 제공하는 정렬 메소드이다.
- 배열의 요소들을 오름차순으로 정렬한다.
- 다양하게 오버로드된 형태로 제공되어서, 기본 데이터 타입 배열뿐 아니라 객체 배열에 대해서도 사용할 수 있다.
	- 객체 배열은 해당 객체 클래스가 `Comparable` 인터페이스를 구현하거나, `Comparator`를 메소드 인자로 제공해야 한다.

## 사용법
```java
int[] arr = {5, 3, 2, 1, 4};
Arrays.sort(arr);
// arr는 이제 {1, 2, 3, 4, 5}로 정렬됩니다.

String[] strings = {"banana", "apple", "cherry"};
Arrays.sort(strings);
// strings는 이제 {"apple", "banana", "cherry"}로 정렬됩니다.

Integer[] numbers = {5, 3, 2, 1, 4};
Arrays.sort(numbers, Comparator.reverseOrder());
// numbers는 이제 {5, 4, 3, 2, 1}로 역순으로 정렬됩니다.
```

## 성능
- 내부적으로 두 가지 정렬 알고리즘을 사용한다.
- 듀얼 피봇 퀵소트(Dual-Pivot Quicksort): 기본 데이터 타입 배열에 대해 사용된다. 평균 시간 복잡도는 `O(nlogn)`이다.
- 팀소트(Timsort): 객체 배열에 대해 사용된다. 병합 정렬과 삽입 정렬의 변형을 결합한 알고리즘으로, 최악의 경우에도 시간 복잡도는 `O(nlogn)`을 보장한다.

## 주의사항
- 원본 배열을 직접 수정하기 때문에 원본 배열의 순서를 유지하려면, 정렬하기 전에 복사해야 한다.
- 객체 배열을 정렬 시 모든 요소가 사