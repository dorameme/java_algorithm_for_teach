


#### 1. 너비 우선 탐색(BFS)
BFS(Breadth-First Search)는 그래프에서 최단 경로를 찾는 알고리즘.

##### BFS 예시
```
입력:
    A 
   / \ 
  B   C 
 /   / \ 
D   E   F

산출: A, B, C, D, E, F
```
산출: 너비 우선 순회는 ABCDEF이다.

#### 2. 깊이 우선 탐색(DFS)
DFS(Depth First Search)는 그래프탐색에 이용되는 알고리즘.

##### DFS 예시
```
입력:
    A 
   / \ 
  B   D 
 / \ / \
C  E F
산출: A, B, C, D, E, F
```
산출: 깊이 우선 순회는 ABCDEF이다.

#### 3. BFS와 DFS의 차이점
| 매개변수 | BFS | DFS |
|----------|-----|-----|
| 정의 | BFS는 너비 우선 검색을 나타낸다. | DFS는 깊이 우선 탐색을 나타낸다. |
| 데이터 구조 | 큐(Queue)  | 스택(Stack)  |
| 개념적 차이 | BFS는 레벨별로 트리를 구축한다. | DFS는 하위 트리별로 트리 하위 트리를 구축한다. |
| 접근법 | FIFO(First In First Out | LIFO(Last In First Out)  |
| 적합성 | BFS는 주어진 타겟에 더 가까운 정점을 검색하는 데 적합 | DFS는 타겟과 떨어진 곳에 솔루션이 있을 때 적합 |
| 응용 |  최단 경로 | 검색 대상 그래프가 큰 경우 |




#### 4. DFS와 BFS의 적합한 유형

####  ✨ DFS, BFS 모두 적합한 유형
 -모든 정점을 방문하는 것이 중요한 경우.

####  ✨ DFS가 적합한 유형
-검색 그래프가 큰 경우(정점과 간선의 개수가 많은 경우) -> 이런경우 BFS로 풀면 시간초과날 수 있음.


#### ✨ BFS가 적합한 유형
 -최단 경로를 구해야 할 때.경로 탐색 시 첫 번째로 찾아지는 해답이 곧 최단거리이다.

 
#### 6. 반복적DFS vs재귀적DFS
일반적으로 반복적 DFS보다 재귀적 DFS가 필요에 더 적합하다. 

1. **코드는 단순하고 자연스럽게 유지하는 것이 중요하다**: 재귀적 구현은 코드가 간결하고 이해하기 쉬우며, 유지보수가 용이하다.
2. **소프트웨어 엔지니어링에서는 대부분 성능보다 유지 관리가 중요하다**: 성능보다는 유지 관리 측면에서 재귀적 구현이 더 자연스럽고 유지보수가 편하므로, DFS는 대부분 재귀적으로 구현한다.
   
#### 5. 반복적 DFS와 재귀적 DFS의 차이점

| **매개변수**           | **반복적 DFS**                           | **재귀적 DFS**                        |
|------------------------|-----------------------------------------|--------------------------------------|
| **구현 방법**          |  스택 자료구조               | 함수 호출을 통한 재귀적 접근         |
| **코드 복잡도**        | 약간 복잡함                               | 간결하고 이해하기 쉬움               |
| **메모리 사용**        | 명시적인 스택 사용, 시스템 호출 스택 사용 안 함 | 시스템 호출 스택 사용                |
| **스택 오버플로우 위험**| 낮음                                      | 탐색 깊이가 깊으면 스택 오버플로우 발생 가능 |
| **유지보수**           | 상대적으로 복잡                           | 유지보수 용이                         |
| **사용 편의성**        | 큰 그래프에서 유리                         | 코드 가독성이 좋음                    |
| **적합성**             | 탐색 깊이가 깊은 경우                     | 일반적인 경우                         |


반복적 DFS와 재귀적 DFS는 각각의 특성과 장단점이 있으므로, 
문제의 성격에 따라 적절히 선택하여 사용할 수 있다. (왠만한 알고리즘에선 거의 재귀적DFS사용) 

일반적으로 코드의 단순성과 유지보수를 고려하여 재귀적 DFS를 많이 사용하지만, 탐색 깊이가 깊어질 경우에는 반복적 DFS가 더 유리할 수 있다.

#### 7.  반복적DFS vs재귀적DFS 코드 비교

```
public class Main {

    static int N, M, R, cnt = 1;
    static int[] vis;
    static ArrayList<Integer>[] arr;
    static ArrayDeque<Integer> stack = new ArrayDeque<>();
    static int[] answer;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer tk = new StringTokenizer(br.readLine());
        N = Integer.parseInt(tk.nextToken());
        M = Integer.parseInt(tk.nextToken());
        R = Integer.parseInt(tk.nextToken());
        answer = new int[N + 1];

        arr = new ArrayList[N + 1];
        for (int i = 0; i <= N; i++) {
            arr[i] = new ArrayList<>();
        }

        vis = new int[N + 1];

        stack.add(R);
        for (int i = 0; i < M; i++) {
            tk = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(tk.nextToken());
            int y = Integer.parseInt(tk.nextToken());
            arr[x].add(y);
            arr[y].add(x);
        }
        Arrays.stream(arr).forEach(Collections::sort);

        dfs();
        IntStream.range(1, N + 1).forEach(x -> System.out.println(answer[x]));
    }

    static void dfs() {
        stack.add(R);
        while (!stack.isEmpty()) {
            int cur = stack.pollLast();
            if (vis[cur] == 1) {
                continue;
            } else {
                vis[cur] = 1;
                answer[cur] = cnt++;
                for (int i = arr[cur].size() - 1; i >= 0; i--) {
                    stack.add(arr[cur].get(i));
                }
            }
        }
    }

    static void recursive_dfs(int cur) {
        if (vis[cur] == 1) {
            return;
        } else {
            vis[cur] = 1;
            answer[cur] = cnt++;
        }
        arr[cur].forEach(Main::recursive_dfs);
    }
}
```
