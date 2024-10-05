# 그래프와 그래프 검색 (BFS, DFS)
## 1. 그래프(Graph)
- 노드와 간선을 이용한 비선형 데이터 구조이다.
- 데이터 간 관계를 표현하는 데, 노드는 데이터를, 노드 간의 관계나 흐름을 간선으로 표현한다.
- 관계나 흐름에서 정도를 표현할 때는 가중치라는 개념을 추가하여 표현한다.

### 1.1 그래프 용어 정리
- 보통 그림에서 동그라미로 표현한 것이 노드, 화살표로 표현한 것이 간선, 간선 위에 숫자로 표현한 것이 가중치이다.

### 1.2 그래프 특징과 종류



## 너비 우선 탐색(BFS, Breadth-First Search)
- 너비 우선 탐색도 그래프를 완전 탐색하는 방법 중 하나로, **시작 노드에서 출발해 시작 노드를 기준으로 가까운 노드를 먼저 방문하면서 탐색하는 알고리즘**이다.
- 특징: FIFO 탐색
- Queue 자료구조를 이용한다.
- 시간복잡도는 O(V + E)로 V는 노드의 수, E는 엣지의 수이다.
- 탐색 시작 노드와 가까운 노드를 우선하여 탐색하므로, 목표 노드에 도착하는 경로가 여러 개일 때 최단 경로를 보장한다.
- 모든 노드를 방문하므로 완전 탐색 문제에 적합하다.
- 특히, 최단 경로를 찾거나 레벨별 정보가 필요한 경우에 효율적이다.
- 소셜 네트워크에서의 친구 추천, 최단 경로 찾기 등에 적합하다.

### 핵심 이론
#### 1. BFS 시작할 노드를 정한 후 사용할 자료구조 초기화하기
- 방문한 노드를 체크하기 위한 배열이 필요하다.
- 그래프를 인접 리스트로 표현한다.
- 탐색을 위해 큐를 사용한다.
![BFS_1](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/BFS_1.png)

#### 2. 큐에서 노드를 꺼낸 후 꺼낸 노드의 인접 노드를 다시 큐에 삽입하기
- 이미 방문한 노드는 큐에 삽입하지 않는다.
![BFS_2](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/BFS_2.png)

#### 3. 큐 자료구조에 값이 없을 때까지 반복하기
- DFS와는 탐색 순서가 다르다.
![BFS_3](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/BFS_3.png)

### 주로 사용하는 틀
```java
import java.io.*;
import java.util.*;

public class BFSExample {
    static boolean[] visited; // 방문 여부를 기록하는 배열
    static List<Integer>[] graph; // 그래프의 인접 리스트 표현
    static int n; // 노드의 개수

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken()); // 노드의 개수
        int m = Integer.parseInt(st.nextToken()); // 간선의 개수
        int start = Integer.parseInt(st.nextToken()); // 시작 정점

        graph = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            graph[u].add(v);
            graph[v].add(u); // 무방향 그래프이므로 양쪽에 추가
        }

        visited = new boolean[n + 1]; // 방문 여부 초기화
        bfs(start);
    }

    static void bfs(int start) {
        Deque<Integer> queue = new ArrayDeque<>();
        queue.offer(start);
        visited[start] = true; // 시작 정점을 방문했다고 표시

        while (!queue.isEmpty()) {
            int currentNode = queue.poll();
            System.out.println("Visited node: " + currentNode);

            for (int nextNode : graph[currentNode]) {
                if (!visited[nextNode]) {
                    visited[nextNode] = true; // 인접 노드를 방문했다고 표시
                    queue.offer(nextNode);
                }
            }
        }
    }
}

```



## 깊이 우선 탐색(DFS, Depth-First Search)
- 그래프 완전 탐색 기법 중 하나이다. 트리 완전 탐색 시 사용한다.
- 그래프의 시작 노드에서 출발하여 탐색할 한 쪽 분기를 정하여 최대 깊이까지 탐색을 마친 후 다른 쪽 분기로 이동하여 다시 탐색을 수행하는 알고리즘이다.
- 재귀 함수로 구현, 스택 자료구조로 이용한다.
- 스택이나 재귀를 사용하여 구현되므로, 메모리 사용량이 BFS보다 적을 수 있다.
	- 재귀 함수를 이용하므로 스택 오버 플로에 유의해야 한다.
- 시간복잡도는 O(V + E)로 V는 노드의 수, E는 엣지의 수이다.

### 핵심 이론
- 한 번 방문한 노드를 다시 방문하면 안되므로, 노드 방문 여부를 체크할 배열이 필요하다.
- 그래프는 인접 리스트로 표현한다.

### 유리한 문제
- 깊이 우선 탐색이 경로의 가능성을 탐색할 때 유리하다.
- 단, 사이클이 있는 그래프에서는 무한 루프에 빠질 위험이 있으므로, 추가적인 조치가 필요하다.
	- 이미 방문한 노드를 다시 방문할 가능성이 있다.
- 미로 찾기, 퍼즐 게임 등에 유용하다.
	- 가능한 모든 경로를 탐색하며, 해결책을 찾을 때까지 깊이 탐색한다.
- 대표 문제로 단절점 찾기, 단절선 찾기, 사이클 찾기, 위상 정렬 등이 있다.

### 동작 원리 (스택 사용 시)
#### 1. 시작할 노드를 정한 후 사용할 자료구조(인접리스트) 초기화한다
- 인접리스트로 그래프를 표현할 때, 1->2,3 에서 2,3은 엣지를 말한다.
![DFS_1_초기화](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/DFS_1_초기화.png)

#### 2. 스택에서 노드를 꺼낸 후 꺼낸 노드의 인접 노드를 다시 스택에 삽입하기
![DFS_2](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/DFS_2.png)

#### 3. 스택 자료구조에 값이 없을 때까지 반복하기
- 다녀간 노드는 방문 배열을 바탕으로 재삽입하지 않는 것이 핵심이다.
- 스택에 노드를 삽입할 때 방문 배열을 체크하고, 스택에서 노드를 뺄 때 탐색 순서에 기록하며 인접 노드를 방문 배열과 대조하여 살펴본다.
![DFS_3](/media/컴퓨터%20과학%20및%20소프트웨어%20공학/Algorithm/DFS_3.png)