# Function 함수

- 분해(Decomposition)
- 추상화(Abstraction)


## 종류

- **내장함수**
    - python 내에 내장되어 있는 함수
- **외장함수**
    - import 사용
- **사용자 정의 함수**

+@ 함수를 사용하기 위해서는 함수를 **정의**해야한다.

```python
ex)
def list(number):
	return value
```

## 결과

- viod function
    - return 이 없을 경우 None
- value returning function
    - return 을 통한 값 반환

## 범위

### Namespace(N)

- Built-in N : 내장된
- Global N : program이 생성될 때 실행되는 N
- Enclosing N : 중첩되어서 사용
- Local N : 함수를 실행하면 함수 안쪽에서 실행되는 N

```python
검색규칙
L > E > G > B 순서!
함수와 변수가 어디에 걸리고 정해지는지 확인!!
```

```python
x = 'Global N'

def namespace():
    x= 'Enclosing N'
    def namespace2():
        x= 'Local N'
        print(x)
    namespace2()
namespace()
```

+@ global 변수 변화할 때 무작위로 쓰기보다는 조심해서 써야한다!!