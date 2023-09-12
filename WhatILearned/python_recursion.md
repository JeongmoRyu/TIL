# python recursion

## 파이썬 재귀 함수 제한 풀기 / 파이썬 최대 재귀 제한 해제

파이썬 재귀 limit은 일반적으로 1000으로 설정되어 있다.

일반적인 코딩 테스트를 하거나 재귀 문제를 해결할 때에 코드 맨 위에서

```python
import sys
sys.setrecursionlimit(10**6)
```

을 설정해주면 재귀 한계로 인한 문제는 발생하지 않을 것 같습니다.
