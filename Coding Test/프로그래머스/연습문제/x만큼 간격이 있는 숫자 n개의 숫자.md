# x만큼 간격이 있는 숫자 n개의 숫자
## 문제
- [x만큼 간격이 있는 n개의 숫자](https://school.programmers.co.kr/learn/courses/30/lessons/12954?language=java)

## 수도 코드
- n개 길이의 배열을 초기화
- for문을 통해 인덱스 하나씩 값 집어넣기
- 제한조건에 따라 혹시라도 int의 범위를 벗어날 수 있으므로, long으로 형변환

## 풀이
```java
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        
        for(int i = 0; i < n; i++) {
            answer[i] = (long) x * (i + 1);
        }
        
        return answer;
    }
}
```