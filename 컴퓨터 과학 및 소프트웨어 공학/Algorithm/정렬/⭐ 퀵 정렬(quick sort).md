# ⭐ 퀵 정렬(quick sort)
- 기준값(pivot)을 선정해 해당 값보다 작은 데이터와 큰 데이터로 분류하는 것을 반복해 정렬하는 알고리즘이다.
- 기준값에 따라서 시간 복잡도에 많은 영향을 미치고, 평균적으로 O(nlogn)이며 최악의 경우 O(n^2)가 된다.

## 핵심 이론
- pivot을 중심으로 계속 데이터를 2개의 집합으로 나누면서 정렬하는 것이 퀵 정렬의 핵심이다.

## 퀵 정렬 과정
1. 데이터를 분할하는 pivot을 설정한다.
	- 중간에 가까울수록 좋다.
2. pivot을 기준으로 다음 과정을 거쳐 데이터를 2개의 집합으로 분리한다.
	- start가 가리키는 데이터가 pivot이 가리키는 데이터보다 작으면 start를 오른쪽으로 1칸 이동한다.
	- end가 가리키는 데이터가 pivot이 가리키는 데이터보다 크면 end를 왼쪽으로 1칸 이동한다.
	- start가 가리키는 데이터가 pivot이 가리키는 데이터보다 크고, end가 가리키는 데이터가 pivot이 가리키는 데이터보다 작으면 start, end가 가리키는 데이터를 swap하고 start를 오른쪽, end는 왼쪽으로 1칸씩 이동한다.
	- start 와 end가 만날 때까지 반복한다.
3. 마지막에 start와 end가 서로 지나치면 이제 loop가 끝나고, start는 나눠진 2번 파티션의 시작위치가 된다.
4. 분리 집합에서 각각 다시 pivot을 선정한다.
5. 분리 집합이 1개 이하가 될 때까지 1~3 과정을 반복한다.

## 퀵 정렬 구현
```java
public class Main {
	private static void quickSort(int[] arr) {
		quickSort(arr, 0, arr.length - 1);
	}

	private static void quickSort(int[] arr, int start, int end) {
		int part2 = partition(arr, start, end);
		if (start < part2 - 1) {
			quickSort(arr, start, part2 - 1);
		}

		if (part2 < end) {
			quickSort(arr, part2, end);
		}
	}

	private static int partition(int[] arr, int start, int end) {
		int pivot = arr[(start + end) / 2];
		while (start <= end) {
			while (arr[start] < pivot) start++;
			while (arr[end] > pivot) end--;
			if (start <= end) {
				swap (arr, start, end);
				start++;
				end--;
			}
		}
		return start;
	}

	private static void swap(int[] arr, int start, int end) {
		int tmp = arr[start];
		arr[start] = arr[end];
		arr[end] = tmp;
	}

	private static void printArray(int[] arr) {
		for (int data: arr) {
			System.out.println(data + ", ");
		}
		System.out.println();
	}

	public static void main(String[] args) {
		int[] arr = {3,9,4,7,5,0,1,6,8,2};
		printArray(arr);
		quickSort(arr);
		printArray(arr);
	}
}
```

```java
public class QuickSort {

    /***
     * 배열을 받아 퀵 정렬을 수행하는 메서드
     * @param array 정렬할 배열
     */
    public static void sort(int[] array) {
        middlePivotSort(array, 0, array.length - 1);
    }
    
    /***
     * 중간 피벗을 사용하는 퀵 정렬 알고리즘
     * @param array       정렬할 배열
     * @param startIndex  현재 부분 배열의 시작 인덱스
     * @param endIndex    현재 부분 배열의 끝 인덱스
     */
    private static void middlePivotSort(int[] array, int startIndex, int endIndex) {
        
        /***
         * 만약 startIndex가 endIndex보다 크거나 같다면 정렬할 원소가 1개 이하이므로 종료
         */
        if (startIndex >= endIndex) {
            return;
        }
        
        /***
         * 배열을 분할하여 피벗의 위치를 얻은 후,
         * 피벗을 기준으로 왼쪽 부분과 오른쪽 부분을 재귀적으로 정렬
         */
        int pivotIndex = partition(array, startIndex, endIndex);   
        
        middlePivotSort(array, startIndex, pivotIndex);
        middlePivotSort(array, pivotIndex + 1, endIndex);
    }
    
    /***
     * 피벗을 기준으로 배열을 분할하는 메서드
     * @param array       정렬할 배열 
     * @param startIndex  현재 부분 배열의 시작 인덱스
     * @param endIndex    현재 부분 배열의 끝 인덱스
     * @return            피벗의 최종 위치 인덱스(rightPointer)를 반환
     */
    private static int partition(int[] array, int startIndex, int endIndex) {
        
        /***
         * leftPointer와 rightPointer를 설정
         * leftPointer는 startIndex - 1로 초기화
         * rightPointer는 endIndex + 1로 초기화
         */
        int leftPointer = startIndex - 1;
        int rightPointer = endIndex + 1;
        
        /***
         * 피벗을 부분 배열의 중간 요소로 설정
         */
        int pivot = array[(startIndex + endIndex) / 2];  // 중간 인덱스의 값 선택
     
        while (true) {
            
            /***
             * leftPointer를 증가시키면서 피벗보다 크거나 같은 요소를 찾음
             */
            do { 
                leftPointer++; 
            } while (array[leftPointer] < pivot);
     
            /***
             * rightPointer를 감소시키면서 피벗보다 작거나 같은 요소를 찾음
             * leftPointer가 rightPointer보다 작거나 같은 동안에만 반복
             */
            do {
                rightPointer--;
            } while (array[rightPointer] > pivot && leftPointer <= rightPointer);
            
            /***
             * 만약 leftPointer가 rightPointer보다 크거나 같다면 분할을 마치고 rightPointer 반환
             */
            if (leftPointer >= rightPointer) {
                return rightPointer;
            }
            
            /***
             * 찾은 leftPointer와 rightPointer의 요소를 교환
             */
            swap(array, leftPointer, rightPointer);
        }
        
    }
    
    /***
     * 배열의 두 요소를 교환하는 메서드
     * @param array 교환할 배열
     * @param index1 첫 번째 요소의 인덱스
     * @param index2 두 번째 요소의 인덱스
     */
    private static void swap(int[] array, int index1, int index2) {
        int temp = array[index1];  // 임시 변수에 array[index1] 저장
        array[index1] = array[index2];  // array[index1]에 array[index2] 값 대입
        array[index2] = temp;      // array[index2]에 임시 변수 값 대입
    }
    
}
```