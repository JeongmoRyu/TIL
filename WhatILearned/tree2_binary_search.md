# tree(트리) 2

## 이진 탐색 트리

- 탐색작업을 효율적으로 하기 위한 자료구조
- 모든 원소는 서로 다른 유일한 키를 갖는다.
- key(왼쪽 서브트리) < key(루트 노드) < key(오른쪽 서브트리)
- 중위순회를 한다면 오름차순으로 정렬된 값을 얻을 수 있다.

### 연산

- 루트에서 시작
- 탐색할 키 값 x를 루트 노드의 키 값과 비교
    - 키 값과 같을 때 : 성공
    - 키 값보다 클 경우 : 왼쪽 서브트리에 대해 탐색 연산 수행
    - 키 값보다 작을 경우 : 오른쪽 서브트리에 대한 탐색 연산 수행

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b5fd795-c87f-4068-8a9c-11d7c79246ea/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230228%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230228T000507Z&X-Amz-Expires=86400&X-Amz-Signature=369edd884f8509b9312a52e95f90fe4121dc889e38a0215294b5451867d34b7b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 삽입 연산
    - 탐색 자리에 원소가 없어서 탐색 실패가 되었을 때 탐색 실패가 결정되는 위치가 삽입 위치가 된다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ef88b6c-67e8-4849-94c5-bf8360cadd1b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230228%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230228T000521Z&X-Amz-Expires=86400&X-Amz-Signature=81061f3171984b74d6e1b13d790f6c1f3d51b422035974c6a547e45f9c04b502&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- visualization 통해 구현되는 모습들을 찾아보자

- 구현 사이트
    - [https://www.cs.usfca.edu/~galles/visualization/BST.html](https://www.cs.usfca.edu/~galles/visualization/BST.html)

    - [http://btv.melezinek.cz/binary-search-tree.html](http://btv.melezinek.cz/binary-search-tree.html)

- 성능
    - 탐색, 삽입, 삭제 시간은 트리의 높이만큼 시간이 걸린다.
        - O(h), h : BST의 깊이
    - 평균의 경우
        - O(log n)
    - 최악의 시간이 걸릴 경우
        - O(n)
        - 순차 탐색과 시간 복잡도가 같다.

## 힙(heap)

- 완전 이진 트리에 있는 노드 중에서 키 값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해서 만든 자료구조
- 최대 힙(max)
    - 키 값이 가장 큰 노드를 찾기 위한 완전 이진 트리
    - 부모노드 > 자식노드
    - 루트 노트 : 키 값이 가장 큰 노드

```python
# 삽입
def enq(n):
    global last
    # 완전 이진트리에 마지막 정점을 추가하고
    last += 1
    # 마지막 정점에 저장
    heap[last] = n
    # 부모가 있고, 부모 > 자식
    child = last
    parent = child//2
    # 부모가 존재하고 부모
    while parent > 0 and heap[parent] < heap[child]:
        heap[parent], heap[child] = heap[child], heap[parent]
        # 옮긴 자리에서 부모와 비교하기 위해
        child = parent
        parent = child//2
    return

```

- 최소 힙(min)
    - 키 값이 가장 작은 노드를 찾기 위한 완전 이진 트리
    - 부모노드 < 자식노드
    - 루트 노드 : 키 값이 가장 작은 노드

```python

# 삽입
def enq(n):
    global last
    # 완전 이진트리에 마지막 정점을 추가하고
    last += 1
    # 마지막 정점에 저장
    heap[last] = n
    # 부모가 있고, 부모 > 자식
    parent = last
    child = parent//2
    # 부모가 존재하고 부모
    while parent > 0 and heap[parent] < heap[child]:
        heap[parent], heap[child] = heap[child], heap[parent]
        # 옮긴 자리에서 부모와 비교하기 위해
        parent = child
        child = parent//2
    return
```

### 삽입

- 힙 삽입 방법
    - 삽입할 자리를 확장한다.
    - 노드에 따라 자리를 바꾸어서 트리를 완성시켜준다.
    - 비교할 부모 노드가 없으면 자리를 확장하여 최대 힙 방식이면 루트노드가 된다.

### 삭제

- 힙에서는 루트 노드의 원소만을 삭제할 수 있다.
- 루트 노드의 원소를 삭제하여 반환

- 힙의 종류에 따라 최대값 혹은 최소값을 구할 수 있다.
- 힙 삭제 방법
    - 루트 노드의 원소를 삭제
    - 마지막 노드 삭제해서 루트 노드에 넣어준다.
    - 힙의 종류에 따라 자리 바꾸기

practice

```python
# 최대 100개의 key

# 최대합 방식

# 삽입
def enq(n):
    global last
    # 완전 이진트리에 마지막 정점을 추가하고
    last += 1
    # 마지막 정점에 저장
    heap[last] = n
    # 부모가 있고, 부모 > 자식
    child = last
    parent = child//2
    # 부모가 존재하고 부모
    while parent > 0 and heap[parent] < heap[child]:
        heap[parent], heap[child] = heap[child], heap[parent]
        # 옮긴 자리에서 부모와 비교하기 위해
        child = parent
        parent = child//2
    return

# 삭제
def deq():
    global last
    # 루트 임시 저장
    tmp = heap[1]
    # 마지막 정점의 값을 루트로 이동
    heap[1] = heap[last]
    # 마지막 정점 삭제
    last -= 1
    parent = 1
    # 왼쪽 자식 번호
    child = parent * 2
    # 자식이 하나 이상 있으면
    while child <= last:
        # 오른쪽 자식도 있고, 오른 쪽 자식의 값이 더 크면
        if child+1 <= last and heap[child] < heap[child+1]:
            # 비교대상을 오른쪽 자식으로 변경
            child += 1
        # 자식의 값이 부모의 값보다 더 크다면 자리 바꾸기
        if heap[child] > heap[parent]:
            heap[child], heap[parent] = heap[parent], heap[child]
            parent = child
            child = parent * 2
        else:
            break
    return tmp

# 완전이진트리 1번-100번 인덱스 준비
heap = [0] * 101
# 완전이진트리의 마지막 정점 번호
last = 0

enq(5)
print(heap[1])
enq(15)
print(heap[1])
enq(8)
print(heap[1])
enq(20)
print(heap[1])

while last > 0:
    print(deq())
```

output

```python
# enq
5
15
15
20
# deq
20
15
8
5
```