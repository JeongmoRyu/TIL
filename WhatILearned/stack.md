# Stack (스택)

- 스택의 특성
    - 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조
    - 선형 구조를 갖는다
        - 선형 구조 : 자료 간의 관계가 1대1의 관계를 갖는다.
        - 비선형 구조 : 자료 간의 관게가 1대 N의 관계를 갖는다. (tree형)
    - 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.
    - 마지막에 삽입한 자료를 가장 먼저 꺼낸다.
    - **후입선출** (LIFO, Last-In-First_Out)

- 스택을 프로그램에서 구현하기 위해서 필요한 자료구조와 연산
    - 자료구조 : 자료를 선형으로 저장할 수 있는 저장소
        - 배열 사용 가능
        - 마지막에 삽입된 원소의 위치를 top
    - 연산
        - 삽입 : push
        - 삭제 : pop 자료를 저장소에서 역순으로 꺼낸다.
        - isEmpty : 공백인지 확인
        - peek : top에 있는 원소를 반환하는 연산

- 스택의 push 알고리즘
    - append 메소드를 통해 리스트의 마지막에 데이터를 삽입
        
        ```python
        def push(item):
        	s.append(item)
        
        ```
        
    
    예시 구현
    
    ```python
    def push(item, size):
    	global top
    	top += 1
    	if top == size:
    		print('overflow!')
    	else:
    		stack[top] = item
    
    size  = 10
    stack = [0]*size
    top = -1
    
    push(10, size)
    top += 1
    stack[top] = 20
    ```
    

### 스택 구현 고려 사항

- 1차원 배열을 사용하여 구현할 경우 구현이 용이하다는 장점이 있지만 스택의 크기를 변경하기가 어렵다는 단점이 있다.
- 이를 해결하기 위해 저장소를 동적으로 할당하여 스택을 구현한다. 구현이 복잡하다는 단점이 있지만 메모리를 효율적으로 사용한다

- 괄호검사
    - 대괄호, 중괄호, 소괄호
    - 괄호를 조사하는 알고리즘 개요
        - 문자열에 있는 괄호를 차례대로 조사하면서 왼쪽 괄호를 만나면 스택에 삽입하고 오른쪽 괄호를 만나면 스택에서 top 괄호를 삭제한 후 오른쪽 괄호와 짝이 맞는지 검사한다.
        - 이 때 스택이 비어 있으면 조건 1 또는 조건 2에 위배되어 괄호의 짝이 맞지 않으면 조건 3에 위배된다.
        
- Function call
    - 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
    - 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로 스택을 이용하여 수행 순서 관리
    - 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수 , 매개변수 및 수행 후 복귀할 주소 등의 정보를 스택 프레임에 저장하여 시스템 스택에 삽입
    - 함수의 실행이 끝나면 시스템 스택의 top원소를 삭제하면서 프레임에 저장되어 있던 복귀 주소를 확인하고 복귀
    - 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다.

```python
class Stack:
    def __init__(self, arr):
        self.arr = arr
        self.top = -1

    def push(self, item):
        self.top += 1
        self.arr[self.top] = item
    def pop(self):
        self.top -= 1
        return self.arr[self.top + 1]

    def is_empty(self):
        return self.top == -1

    def peek(self):
        return self.arr[self.top]

data = input()
stack = Stack([0] * len(data))
result = -1
for i in range(len(data)):
    # 시작
    # 아무것도 없고 데이터가 (로 시작할 때 # 시작이 좌괄호
    if stack.top == -1 and data[i] == '(':
        stack.push(data[i])
        # 그냥 좌괄호가 나올 때
    elif data[i] == '(':
        stack.push(data[i])
        # 스택이 비어있지 않은 상태의 우괄호
    elif data[i] == ')':
        if stack.peek() == '(':
            stack.pop()
        else:
            break
    elif stack.top == -1 and data[i] == ')':
        break
    # 그 외
    else:
        continue
# for - else는 break 없이 반복이 종료된 for에 대해서는 else가 실해
else:
    # 괄호가 다 검사한 후의 시점
    if stack.is_empty():
        # 스택이 비었다면 다 검사한거
        result = 1
print(result)
```