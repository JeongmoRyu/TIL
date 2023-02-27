# Tree(트리)


## 트리의 개념

- 비선형 구조
- 원소들 간에 1:n 관계를 가지는 자료구조
- 원소들 간에 계층 관계를 가지는 계층형 자료구조
- 상위 원소에서 하위 원소로 내려가면서 확장되는 트리구조

## 정의

- 한 개 이상의 노드로 이루어진 유한 집합
    - 최상위 노드 루트(root)
    - 나머지 노드들은 n개의 분리 집합으로 분리될 수 있다.
- 각각 하나의 트리가 되며 루트의 부트리(subtree)라고 한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a984ed50-307a-4917-9111-69c66c3b6469/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230227%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230227T021915Z&X-Amz-Expires=86400&X-Amz-Signature=b2e51364224a55f4867eac294d13fcc6ce946d1f27fdc973a9c86a491ab99202&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## 용어 정리

- 노드 : 트리의 원소
    - 간선(edge) : 노드를 연결하는 선
    - 루트 노드 : 시작 노드
    - 형제 노드 : 같은 부모 노드의 자식 노드들
    - 조상 노드 : 간선에 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
    - 서브 트리 : 부모와의 간선을 끊을 때 생기는 트리
    - 자손 트리 : 서브 트리에 있는 하위 레벨의 노드들
- 차수(degree)
    - 노드의 차수 : 노드에 연결된 자식 노드의 수
    - 트리의 차수 : 트리에 있는 차수 중에서 가장 큰 값
    - 단말 노드(리프 노드) : 차수가 0인 노드, 자식 노드가 없는 노드
- 높이(level)
    - 루트에서 노드에 이르는 간선의 수, 노드의 레벨
    - 트리의 높이 : 노드의 높이 중에서 가장 큰 값

## 이진트리

- 모든 노드들이 2개의 서브트리를 갖는 형태의 트리
- 노드의 최소 개수는 h+1개, 최대 2**(h+1) -1개
- 포화이진트리(Full Binary Tree)
    - 모든 레벨의 노드가 포화상태로 차 있는 이진 트리 (2**(h+1) -1)
- 완전 이진 트리(Complete Binary Tree)
    - 높이가 h 이고 노드의 수가 n개일 때 포화 이진트리의 노드 번호가 1번부터 n번까지 빈 자리가 없는 이진트리 (중간번호가 빠지지 않은 이진트리)
- 편향 이진 트리(Skewed Binary Tree)
    - 높이 h에 대해 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진트리
        - 왼쪽 편향
        - 오른쪽 편향

### 이진트리 - 순회

- 트리의 노드들을 체계적으로 방문하는 것
- 3가지 방법
    - 전위순회 : VLR
        - 부모노드 방문 후 자식노드를 좌, 우 순서로 방문한다.
    - 중위순회 : LVR
        - 왼쪽 자식노드, 부모노드, 오른쪽 자식노드 순서로 방문한다.
    - 후위순회 : LRV
        - 자식노드를 좌우 선서로 방문한 후 부모노드로 순서로 방문한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c8c33150-f32a-448c-a072-6d965a7e1a3b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230227%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230227T021947Z&X-Amz-Expires=86400&X-Amz-Signature=b17101a99162220355dbb266edfc4ab4259abc61f32d9eb5e506052b94408753&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

전위 순회 - A B D H I E J C F K G L K

중위 순회 - H I D B J E A F K C L G M

후위 순회 - H I D J E B K F L M G C A

## 이진트리의 배열

- 노드 번호의 성질
    - 노드 번호가 i 인 노드의 부모 노드 번호 [i/2]
    - 노드 번호가 i 인 노드의 왼쪽 자식 노드 번호 2*i
    - 노드 번호가 i 인 노드의 오른쪽 자식 노드 번호 2*i + 1
    - 레벨 n의 노드 번호 시작 2**n
    - 높이가 h인 이진트리의 배열 크기
        - 레벨 i의 최대 노드 수 2**i
        
        → 2**(h+1) -1
        
    
- 순회 함수 짜기
    - (L, V, R 순서를 바꾸면 된다.)

```python
def pre_order(tree, node):
    # (V - L - R)
    if node != 0:
        # 0이 아니라면 순회를 하지 않는다.
        print(f'{node}', end=' ')
        pre_order(tree, tree[node][0])
        # 왼쪽
        pre_order(tree, tree[node][1])
        # 오른쪽
# 순서만 바꾸면 된다.
# 중위순회(L - V - R)
def in_order(tree, node):
    if node != 0:
        in_order(tree, tree[node][0])
        print(f'{node}', end=' ')
        in_order(tree, tree[node][1])

# 후위순회(L - R - V)
def post_order(tree, node):
    if node != 0:
        in_order(tree, tree[node][0])
        in_order(tree, tree[node][1])
				print(f'{node}', end=' ')

```

practice

```python
'''
13
1 2 1 3 2 4 3 5 3 6 4 7 5 8 5 9 6 10 6 11 7 12 11 13
'''

# tree는 전위순회하기 위한 tree
# node는 시작점
def pre_order(tree, node):
    # (V - L - R)
    if node != 0:
        # 0이 아니라면 순회를 하지 않는다.
        print(f'{node}', end=' ')
        pre_order(tree, tree[node][0])
        # 왼쪽
        pre_order(tree, tree[node][1])
        # 오른쪽
# 순서만 바꾸면 된다.
# 중위순회(L - V - R)
def in_order(tree, node):
    if node != 0:
        in_order(tree, tree[node][0])
        print(f'{node}', end=' ')
        in_order(tree, tree[node][1])

# 후위순회(L - R - V)

V = int(input())
E = V - 1
# 간선은 하나를 제외하고 자동적으로 생성되기에 V - 1

# 0 ~ V 까지의 노드의 [왼쪽, 오른쪽, 부모] 정보
# [l, r, p]의 값 중 0은 없다는 의미
tree = [[0 for _ in range(3)] for _ in range(V + 1)]

# 입력부는 문제에 따라 다르게 해줄것 잊지말자
temp_input = list(map(int, input().split()))

for i in range(E):
    # parent, child로 입력을 구분
    parent, child = temp_input[i*2], temp_input[i*2 + 1]

    # 왼쪽 자식이 없다면
    if not tree[parent][0]:
        # tree[parent][0] == 0
        tree[parent][0] = child
    # 입력에 따라 오른쪽 자식은 없어야한다.
    else:
        tree[parent][1] = child

    # 부모정보 업데이트
    tree[child][2] = parent

print(tree)
pre_order(tree, 1)
print()

```

output

```python
[[0, 0, 0], [2, 3, 0], [4, 0, 1], [5, 6, 1], [7, 0, 2], [8, 9, 3], [10, 11, 3], [12, 0, 4], [0, 0, 5], [0, 0, 5], [
0, 0, 6], [13, 0, 6], [0, 0, 7], [0, 0, 11]]
1 2 4 7 12 3 5 8 9 6 10 11 13
```

- 배열
    - 배열을 이용한 이진 트리의 단점
        - 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생
        - 트리의 중간에 새로운 노드를 삽입하거나 기존의 노드를 삭제할 경우 크기 변경이 어려워 비효율적
- 연결리스트
    - 배열의 단점을 보완하기 위해 연결리스트를 이용하여 트리를 표현

```python
ex)
[[0, 0, 0], [2, 3, 0], [4, 0, 1], [5, 6, 1], [7, 0, 2], [8, 9, 3], [10, 11, 3], [12, 0, 4], [0, 0, 5], [0, 0, 5], [
0, 0, 6], [13, 0, 6], [0, 0, 7], [0, 0, 11]]

```