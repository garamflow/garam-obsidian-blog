# 투 포인터(Two Pointer)
- 배열, 리스트와 같은 자료구조에서 두 개의 포인터를 사용해서 문제를 해결하는 알고리즘 기법
- 특정 조건을 만족하는 두 값이나 구간을 찾는 데 사용된다.
- 대부분 O(n)의 시간 복잡도를 가진다.

## 개념
- 서로 다른 위치에 포인터(인덱스)를 설정하고, 상황에 따라 포인터를 이동시키면서 문제를 해결한다.

### 두 포인터가 서로 다른 방향으로 이동
- 배열의 앞과 뒤에서 두 포인터를 시작해, 특정 조건을 만족할 때까지 이동시킨다.
- **정렬된 배열**에서 주로 사용되며, 두 포인터의 값을 비교하면서 조건을 만족하는 경우 포이터를 이동시킨다.

### 두 포인터가 같은 방향으로 이동
- 두 포인터가 동시에 배열의 시작에서 시작해서 서로를 비교하거나 특정 구간을 추적하며 이동한다.
- 슬라이딩 윈도우와 비슷하게 구간이나 연속된 범위를 추적할 때 사용된다.

## 응용
### 정렬된 배열에서 두 수의 합
- 두 수의 합이 특정 목표값이 되는 쌍을 찾는 문제
- 배열이 정렬되어 있다면 하나의 포인터는 배열의 시작에서, 다른 하나는 끝에서 시작한다.
- 두 값을 더한 결과가 목표값보다 크면 뒤쪽 포인터를 왼쪽으로 이동하고, 작으면 앞쪽 포인터를 오른쪽으로 이동시키며 탐색한다.

```java
public boolean twoSum(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return true;  // 두 수의 합이 target인 경우
        } else if (sum < target) {
            left++;  // 합이 target보다 작으면 왼쪽 포인터를 오른쪽으로 이동
        } else {
            right--; // 합이 target보다 크면 오른쪽 포인터를 왼쪽으로 이동
        }
    }
    return false;
}
```

### 팰린드롬 문자열 검사
- 주어진 문자열이 팰린드롬(앞뒤가 똑같은 문자열)인지 확인하는 문제
- 문자열의 앞에서 시작하는 포인터와 뒤에서 시작하는 포인터가 서로를 향해 이동하면서, 각 문자가 동일한지 확인한다.

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;  // 팰린드롬이 아닌 경우
        }
        left++;
        right--;
    }
    return true;
}
```

## 투 포인터 사용 시 고려할 점
- 배열이나 리스트의 정렬이 필요할 수 있다.
	- 시간 복잡도인 O(nlogn)이 추가된다.
- 요구 사항에 따라 두 포인터를 어떻게 설정하고 움직일지 계획해야한다.