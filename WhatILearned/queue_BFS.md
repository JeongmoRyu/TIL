# Queue2

## BFS(Breadth First Search)

- 그래프 탐색 방법
    - 깊이 우선 탐색(Depth First Search, DFS)
    - 너비 우선 탐색(Breadth First Search, BFS)
        - 탐색 시작점의 인접한 정점들을 차례로 찾은 후에 방문했던 점을 시작점으로 다시 인접한 점들에서 찾는 방식
- BFS 알고리즘

```python
def BFS(G, v, n):
    # 그래프 G, 탐색시작점 v
    visited = [0] * (n+1)
    # n은 정점의 갯수
    queue = []
    # 큐 생성
    queue.append(v)
    # 시작점에 v를 큐에 삽입
    visited[v] = 1
    while queue:
        # 큐가 비어있지 않다면 진행
        t = queue.pop(0)
        visit(t)
        for i in G[t]:
            # t와 연결된 모든 정점에 대해
            if not visited[i]:
                # 방문하지 않으면
                queue.append(i)
                # 큐에 추가하가ㅣ
                visited[i] = visited[n] + 1
                # n부터 1만큼 이동
```

practice

![line](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a963bbb2-7c2c-4e52-a8ad-341f7e252409/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230226%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230226T014730Z&X-Amz-Expires=86400&X-Amz-Signature=8e0b3c45c0f8527434e111d901c30f45440b7d87a6c54394ecd4d874a59f34f0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def bfs(v, N):
    visited = [0]*(N+1)
    q = [v]
    visited[v] = 1
    while q:
        # q가 비어있지 않으면
        t = q.pop(0)
        print(t, end = '-')
        for v in adjL[t]:
            # t에 인접하고 방문한적 없는 v
            if visited[v] == 0:
                q.append(v)
                # v 인큐
                visited[v] = visited[t] + 1
                # v 인큐되었음을 표시

V, E = map(int, input().split())
arr = list(map(int, input().split()))
adjL = [[] for _ in range(V+1)]
for i in range(E):
    n1, n2 = arr[i*2], arr[i*2 + 1]
    adjL[n1].append(n2)
    adjL[n2].append(n1)
    # 방향성을 가지고 있지 않기 때문에 둘다 입력해준다.
bfs(1, V) # 시작점정 1, V 마지막 정점
```

함수를 사용하지 않고

```python
# 노드와 간선
V, E = 7, 8
S = 1

# 연결 정보 (1, 2)
connected = [1, 2, 1, 3, 2, 4, 2, 5, 4, 6, 5, 6, 6, 7, 3, 7]

# 연결 정보 전처리
# 1부터 시작 (0 index는 다 0)
connection_map = [[0] * (V + 1) for _ in range(V + 1)]

# 간선 개수 만큼 반복
for i in range(E):
    n1, n2 = connected[i * 2], connected[i * 2 + 1]
    connection_map[n1][n2] = 1
    connection_map[n2][n1] = 1

# visited 방문 체크
visited = [0 for _ in range(V + 1)]

# BFS 용 큐, 시작은 1
queue = [S]
visited[S] = 1

while queue:
    now = queue.pop(0)
    current_distance = visited[now]
    # 지금 방문한 곳
    # 정답용 출력
    print(f'-{now}', end='')

    # 방문한 곳과 인접한 곳들 찾기
    for next in range(1, V + 1):
        # 연결되어 있는가?, 방문한 적 없는가?
        if connection_map[now][next] == 1 and visited[next] == 0:
            queue.append(next)
            # 방문 정보에 거리 정보 포함
            visited[next] = current_distance + 1
    # new line 개행 문자
print()

# 방문 정보에 거리 정보 포함
print(visited)
```