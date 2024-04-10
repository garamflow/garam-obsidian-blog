# K번째수
## 문제
- [K번째수](https://school.programmers.co.kr/learn/courses/30/lessons/42748)

## 수도 코드
- commands의 길이만큼의 answer 정수 배열을 초기화
- commands의 길이만큼 순회하면서 array의 부분에 해당하는 새로운 배열을 생성
- 해당 배열을 정렬
- answer 배열에 새롭게 정렬된 배열 중 선택된 값을 집어넣기

## 풀이
```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        for(int i = 0; i < commands.length; i++) {
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }
        
        return answer;
    }
}
```