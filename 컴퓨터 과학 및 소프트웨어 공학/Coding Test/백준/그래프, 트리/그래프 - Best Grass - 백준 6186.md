## 코드
```java
package W2.D5;  
  
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.StringTokenizer;  
  
public class _1_BestGrass6186 {  
    static int[][] DIRECTION = {{0, 1}, {1, 0}};  
  
    static boolean[][] visited;  
    static char[][] graph;  
    static int R, C; // 행, 열  
  
    public static void main(String[] args) throws IOException {  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringTokenizer st = new StringTokenizer(br.readLine());  
        R = Integer.parseInt(st.nextToken());  
        C = Integer.parseInt(st.nextToken());  
  
        graph = new char[R][C];  
        visited = new boolean[R][C];  
        for (int i = 0; i < R; i++) {  
            String line = br.readLine();  
            for (int j = 0; j < C; j++) {  
                graph[i][j] = line.charAt(j);  
            }  
        }  
  
        int count = 0;  
        for (int i = 0; i < R; i++) {  
            for (int j = 0; j < C; j++) {  
                if (graph[i][j] == '#' && !visited[i][j]) {  
                    dfs(i, j);  
                    count++;  
                }  
            }  
        }  
  
        System.out.println(count);  
    }  
  
    static void dfs(int x, int y) {  
        visited[x][y] = true;  
        char currentChar = graph[x][y];  
  
        for (int[] direction : DIRECTION) {  
            int newX = x + direction[0];  
            int newY = y + direction[1];  
  
            if (newX < R && newY < C && graph[newX][newY] == currentChar && !visited[newX][newY]) {  
                    dfs(newX, newY);  
            }  
        }  
    }  
}
```