# Stack(스택) 3

### DFS 깊이 우선 탐색

- 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함
- 후입선출 구조의 스택을 사용한다.
- 방법
    - 깊이 우선 탐색 (DFS, Depth First Search)
    - 너비 우선 탐색(BFS, Breadth First Search)
    
  
    DFS 1-2-4-6-5-7-3 순으로 이동하며 DFS 탐색을 한다.
    

### DFS practice

input

```python
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
```

```python

# V = Vertice = 정점, E = Edge = 간선
# V : 갈 곳의 수 E : 길의 수
V, E = map(int, input().split())
arr = list(map(int, input().split()))

adjM = [[0]*(V+1) for _ in range(V+1)]
# 인접 정보 2차원 행렬
# index 0의 아이템 -> [1 if 인접 else 0 for i in range(V)]
adjL = [[] for _ in range(V+1)]
# index 0의 아이템 -> [0에 인접한 점의 인덱스]
# 인접 정보 리스트

# 인접 정보 정리
for i in range(E):
    v1, v2 = arr[i*2], arr[i*2 + 1]
    adjM[v1][v2] = 1
    adjM[v2][v1] = 1

    adjL[v1].append(v2)
    adjL[v2].append(v1)

import pprint
pprint.pprint(adjM)
print()
pprint.pprint(adjL)

# 점을 방문한적이 있는지에 대한 정보
visited = [0 for _ in range(V+1)]
# visited[i] == 1 이면 i에 방문한 적 있음을 기록하는 리스트

# start는 시작점
def depth_first_search(start):
    stack = [start]

    # stack이 빌때까지 반복
    while stack:
        # [] 는 Falsy하기 때문에
        now = stack.pop()

        #미방문
        if visited[now] == 0:
            print(now, end='-')
            visited[now] = 1

            # next는 다음점, V부터 1까지
            for next in range(V, 0, -1):
                # 연결되어 있고 아직 방문하지 않았으면
                if adjM[now][next] == 1 and visited[next] == 0:
                    stack.append(next)

    print()

depth_first_search(1)

```

- 재귀 함수로 간단하게 풀기(정의 부분부터 차이)
    - 컴퓨터가 대신 stack관리를 해준다고 생각하면 됨

```python
def depth_first_search(ver):
    # 함수 호출되면 거기 방문한 것
    visited[ver] = 1
    # 작은 숫자부터 세기
    print(ver, end = '-')
    for next in range(1, V + 1):
        # 인접하고 미방문이면
        if adjM[ver][next] == 1 and visited[next] == 0:
            # 다음 함수 호출

            depth_first_search(next)

depth_first_search(1)
```

```python
[[0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 1, 1, 0, 0, 0, 0],
 [0, 1, 0, 0, 1, 1, 0, 0],
 [0, 1, 0, 0, 0, 0, 0, 1],
 [0, 0, 1, 0, 0, 0, 1, 0],
 [0, 0, 1, 0, 0, 0, 1, 0],
 [0, 0, 0, 0, 1, 1, 0, 1],
 [0, 0, 0, 1, 0, 0, 1, 0]]

[[], [2, 3], [1, 4, 5], [1, 7], [2, 6], [2, 6], [4, 5, 7], [6, 3]]

1-2-4-6-5-7-3
```

## 계산

- 문자열로 된 계산식이 주어질 때, 스택을 이용하여 이 계산식의 값을 계산할 수 있다.

- 
- 문자열 수식 계산의 일반적 방법
    - step1 중위표기법의 수식을 후위 표기법으로 변경한다.(스택 이용) - 사람 식
        - 우선 순위에 따라 괄호를 사용하여 다시 표현한다.
        - 연산자를 그에 대응하는 오른쪽 괄호 뒤로 이동시킨다.
        - A*B-C/D
        - AB*CD/-

input

```python
2+3*4/5
(6+5*(2-8)/2)
3-2*5+4/2-2
```

```python
# 받아올 수식 문자열
expression = input()
stack = []
# 출력문자열
result = ''

# 한글자씩 알아보자
for token in expression:
    if token.isdecimal():
        result += token
    else:
        # 첫 연산자
        if not stack:
            # 기록
            stack.append(token)
        elif token == '(':
            # 무조건 push
            stack.append(token)
        elif token in '*/':
            # last_operator = stack[-1]
            # 나보다 느린애가 나올때 까지
            while stack and stack[-1] in '*/':
                result += stack.pop()
            # 그다음 나
            stack.append(token)
        elif token in '+-':
            # 더하기 빼기는 여는 괄호보다만 빠르다.
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.append(token)
        # 닫는 괄호
        elif token == ')':
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.pop()
            # 남는 괄호는 버린다.
    # 아직 계산 안한 남은 연산자
while stack:
    result += stack.pop()
print(result)

```

output

```python
234*5/+
6528-*2/+
325422-/+*-
```

- step2 후위 표기법의 수식을 스택을 이용하여 계산 - 컴퓨터 식
    - 피연산자를 만나면 스택에 push
    - 연산자를 만나면 필요한 만큼의 피연산자를 스택에서 pop하여 연산하고 연산결과를 다시 스택에 push한다.
    - 수식이 끝나면 마지막으로 스택을 pop하여 출력한다.
    - (6 + 5 *(2 - 8) / 2)
    - (6 + 5 * -6 / 2)
    - (6 + -30 / 2)
    - (6 + -15)
    - -9
    

## 백트래킹(Backtracking)

- 기법은 해를 찾는 도중에 막히면 되돌아가서 다시 해를 찾아 가는 기법이다.
- 최적화 문제와 결정 문제를 해결할 수 있다.

- 백트래킹과 깊이 우선 탐색과의 차이
    - 시도의 횟수를 줄임 (prunning 가지치기)
    - 깊이 우선 탐색은 모든 경로를 추적하는데 비해 백트래킹은 불필요한 경로를 조기에 차단

```python
def checknode(v) :
    if promising(v):
        if there is a solution at v:
            write the solution
        else:
            for u in each child of v:
                checknode(u)
```

backtrack prac

```python
MAXCANDIDATES = 6
NMAX = 6
data = [range(10)]
a = [0] * NMAX
cnt = 0
total_cnt = 0

def backtrack(a, k, input_):
    c = [0] * MAXCANDIDATES

    # k==input_ 일때 순열에 사용할 데이터 다 고름
    if k == input_:
        for i in range(1, k + 1):
            print(a[i], end=' ')
        print()
    # 아직 다 못고른 경우
    else:
        k += 1
        new_candidates = construct_candidates(a, k, input_, c)
        for i in range(new_candidates):
            a[k] = c[i]
            backtrack(a, k, input_)
def construct_candidates(a, k, input_, c):
    # 이 숫자가 이미 사용되었는가
    in_perm = [False] * NMAX
    for i in range(1, k):
        in_perm[a[i]] = True

    count = 0
    for i in range(1, input_ + 1):
        if not in_perm[i]:
            c[count] = i
            count += 1

    return count

a = [0] * NMAX
backtrack(a, 0, 5)
```

## 부분집합 구하기

- 부분집합의 갯수 2**n

```python
bit = [0, 0, 0, 0]
for i in range(2):
    bit[0] = i
    for j in range(2):
        bit[1] = j
        for k in range(2):
            bit[2] = k
            for l in range(2):
                bit[3] = l
                print(bit)
```

- 백트래킹 기법으로 powerset을 구해보자

부분 집합을 구하자

```python
def f(i, k):
    if i == k:
        print(bit)
    else:
        bit[i] = 1
        f(i+1, k)
        bit[i] = 0
        f(i+1, k)

A = {1, 2, 3, 4, 5}
N = len(A)
bit = [0]*N

f(0, N)
```

부분 집합의 합 구하는 방법 / 찾고자 하는 값과 같은 때 원소들도 확인하기

```python
def f(i, k, key):
    if i == k:
        # 하나의 부분집합 완성
        s = 0
        for j in range(k):
            if bit[j]:
                s += A[j]
                #부분 집합의 합
                # print(A[j], end = ' ')
                # 부분 집합의 원소들
        if s == key:
            for j in range(k):
                if bit[j]:
                    print(A[j], end = ' ')
                    # 합이 key랑 같은 때 원소들을 보여준다.

        print(bit, s)
        # 부분 집합 모양 및 합
    else:
        bit[i] = 1
        f(i + 1, k,  key)
        bit[i] = 0
        f(i + 1, k, key)

A = [1, 2, 3, 4, 5]
N = len(A)
key = 5
bit = [0]*N
f(0, N, key)

```

backtracking을 사용하여 함수 호출의 갯수를 줄이는 방법(고려한 구간의 합 S가 원하는 T값보다 클 경우 미리 중단)

```python

def f(i, k, s, t):
    global fcnt
    # i 원소, k 집합의 크기, s i-1까지의 고려된 원소들의 합, t 목표값
    global cnt
    fcnt += 1
    # 밑의 문장이 없으면 key 10일 때 함수 호출의 수가 2047 있을 경우 415
    if s > t:
        # 고려한 원소의 합이 찾는 합보다 큰 경우 뒤의 상황을 진행할 필요가 없다.
        return
    # 밑의 문장이 생기면서 415의 갯수가 349로 줄었다.
    elif s == k:
        # 남은 원소를 고려할 필요가 없는 경우
        cnt += 1
        return
    elif i == k:
        # 모든 원소 고려
        return
    else:

        f(i+1, k, s+A[i], t)
        # A[i] 포함
        f(i+1, k, s, t)
        # A[i] 미포함

A = [1, 2, 3, 4, 5, 6, 7, 8 ,9 ,10]

N = len(A)
key = 10
bit = [0]*N
cnt = 0
fcnt = 0
f(0,N,0,key)
print(cnt, fcnt)
# 합인 key인 부분집합의 수
# 호출된 함수의 갯수
```

 + 고려 사항

- 고려한 구간의 합 S에 남은 구간의 합을 더했을 경우 원하는 T값보다 작을 경우 미리 중단 가능하다.
- 위의 방식과 고려사항을 추가했을 경우

```python
arr = list(range(1, 11))
N = 10

# arr  = 원소후보들
# idx = idx번째 원소
# total = 여태까지 합
# powerset이라는 함수의 역할은 idx번째 원소를 부분집합에 포함시킬까를 결정
# + 현재 부분집합이 답이 될 가능서잉 남아있는지 판단
# + 현재 부분집합이 답인지 판단
def powerset(arr, idx, subset):
    # 현재 부분집합의 합이 답이 될 가능성이 남아있는지 판단
    if sum(subset) == 10:
        print(subset)
        return
    # 남은 것들과 현재의 것 다 포함해도 답이 안됨
    if sum(arr[idx:]) + sum(subset) < 10:
        return
    # 현재 부분집합의 합이 답이 될 가능성이 남아있는지 판단
    if sum(subset) > 10:
        return
    # 부분집합 다만듬
    if idx == N:
        if sum(subset) == 10:
            # print(True)
            print(subset)

        return

    powerset(arr, idx + 1, subset + arr[idx])
    powerset(arr, idx + 1, subset)

```

### 순열
```python

def f(i, k):
    if i == k:
        print(p)
    else:
        for j in range(i, k):
            p[i], p[j] = p[j], p[i]
            # p[i] 결정된 상태에서, p[i]와 관련된 작업이 가능하다.
            f(i+1, k)
            p[i], p[j] = p[j], p[i]

p = [1, 2, 3]
N = len(p)
f(i, N)
```