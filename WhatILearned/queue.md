# Queue(큐)

## Queue

- 특성
    - 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
    - 뒤에서는 삽입만 앞에서는 삭제만 이루어지는 구조
- 선입선출구조(FIFO)
    - 순서대로 원소 저장되고 가장 먼저 삽입되는 원소는 가장 먼저 삭제된다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/57fca3da-0216-4725-a341-6062e725e665/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230225%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230225T013735Z&X-Amz-Expires=86400&X-Amz-Signature=16a826b35c42fa787c6ddfa7370d66b8f33c068c585cd8cc9765be1dc70349fd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject
)
- 연산 종류
    - enQueue(item) : 큐의 뒤쪽에 원소를 삽입하는 연산
    - deQueue() : 큐의 앞쪽에서 원소를 삭제하고 반환
    - createQueue() : 큐를 생성
    - isEmpty() : 큐가 비어있는지 확인
    - isFull() : 큐가 포화상태인지 확인
    - Qpeek() : 앞쪽에서 원소를 삭제 없이 반환하는 연산

```python
class Queue:
    # createQueue, 만들 큐의 크기를 받자
    def __init__(self, n):
        self.size = n
        self.items = [None] * n
        self.rear = -1
        self.front = -1

    # 큐에 아이템 추가
    def en_queue(self, item):
        # 가득차면 추가할 수 없다
        if self.is_full():
            print("Queue is full")
        else:
            self.rear += 1
            self.items[self.rear] = item

    # 큐에 아이템 제거
    def de_queue(self):
        if self.is_empty():
            print("Queue is empty")
        else:
            self.front += 1
            return self.items[self.front]

    # 큐가 비어있는지
    def is_empty(self):
        return self.front == self.rear

    # 큐가 가득찼는지
    def is_full(self):
        return self.rear == self.rear -1

    def peek(self):
        return self.items[self.front]

    # dunder method로서,
    # len 함수의 인자로 활용되었을 때의 변환 정의
    def __len__(self):
        return self.rear - self.front
```

- 선형 큐
    - 1차원 배열을 이용한 큐
    - 크기 = 배열의 크기
    - front  : 첫 번째 원소의 인덱스
    - rear :  마지막 원소의 인덱스
- 상태 표현
    - 초기 상태 : front = -1, rear = -1
    - 공백 상태 : front == rear
    - 포화 상태 : rear == n-1

- 발생할 수 있는 아쉬운 문제점
    - 잘못된 포화 상태 인식
    - 배열이 앞 부분이 활용할 수 있는 공간이 있음에도 rear = n-1인 상태에서는 포화 상태로 인식하여 삽입 수행 x
        - 원소들의 배열을 매 연산마다 앞 부분으로 이동시키기
            - 많은 시간이 소요되어 큐의 효율성이 급격하게 떨어진다.
        - 1차원 배열을 원형 형태의 큐 사용
            - front = rear = 0
            - 마지막 인덱스 n-1 이후 0으로 인덱스를 이동시킨다. 이를 위해 나머지 연산자 mod를 사용한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ca48c4d9-8340-47bb-b4cf-4f307ae306b8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230225%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230225T013843Z&X-Amz-Expires=86400&X-Amz-Signature=2a1047a502550339aa740021f0b74af5f826759c13c09733641972a57b4f0796&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
원형 큐 구현

```python

def enqueue(item):
    global rear
    if isFull():
        print("Queue_Full")
    else:
        rear = (rear + 1) % len(cQ)
        cQ[rear] = item

def deQueue():
    global front
    if isEmpty():
        print("Queue_Empty")
    else:
        front (front + 1) % len(cQ)
        return cQ[front]

def isEmpty():
    return front = rear

def isFull():
    return (rear+1) % len(cQ) == front

```

- 큐의 활용 : 버퍼
    - 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역
    - 버퍼링 : 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작
- 버퍼의 자료 구조
    - 일시적으로 입출력 및 네트워크와 관련된 기능에서 이용
    - FIFO 방식의 자료구조