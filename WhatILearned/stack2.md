# Stack(스택) 2



## 재귀 호출()

- 자기 자신을 호출하여 순환 수행되는 것
- 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출 방식보다 재귀 호출 방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성
- 대표적인 예시
    - factorial

피보나치 수를 구하는 재귀함수

```python
def fibo(n):
    if n < 2:
        return n
    else:
        return fibo(n-1) + fibo(n-2)
```

### memorize

memoize를 사용하면 실행시간 O(n)을 줄일 수 있다.

```python
def fibo1(n):
    global memo
    if n >= 2 and mono[n] == 0:
        memo[n] = (fibo1(n-1) + fibo1(n-2))
    return memo[n]

memo = [0] * (n+1)
memo[0] = 0
memo[1] = 1
```

### DP(dynamic programming)

- 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.
- 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.
- 구현방식
    - recursive : fibo1()
    - iterative : fibo2()

```python
def fibo2(n):
    f = [0] * (n+1)
    f[0] = 0
    f[1] = 1
    for i in range(2, n+1):
        f[i] = f[i-1] + f[i-2]

    return f[n]
```

- 재귀 prac

```
def f(i, k):
    if i == k:
        # 목표에 도달하면
        print(B)
        return
    else:
        B[i] = A[i]
        f(i+1, k)

A = [i*10 for i in range(1, 4)]
B = [0] * 3
f(0,3)
```

range 1000으로 B = [0]*1000, f(0, 1000)  바꿔서 큰 숫자도 재귀가 되는지 확인을 해보면 오류가 뜨게 된다.

```python
RecursionError: maximum recursion depth exceeded in comparison
```