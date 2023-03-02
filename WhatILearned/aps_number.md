# APS_number

## 진수

- 2진수, 8진수, 10진수, 16진수
- 10진수 → 타진수
    - 원하는 타진법의 수로 나눈 뒤 나머지를 거꾸로 읽는다.
- 타진수 → 10진수
    - 각 수 마다 타진수의 제곱수들을 곱해주면서 더한다.
- 소수점이 있을 때
    - 양수의 정수 값들은 일반적으로 구해주고
    - 소수점이 있을 떄에는
        - 0.123(2진법)  = 1*2**-1 + 2*2**-2 + 3*2**-3

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c3bc13c-cd59-44dc-88ba-4134bbedd58e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230302%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230302T235020Z&X-Amz-Expires=86400&X-Amz-Signature=25c8b5cacd1917c0b71e0e8b31eb1f2898ec83db87bf57ca31d9cb361dadf373&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 컴퓨터에서의 음의 정수 표현 방법
    - 1의 보수
        - 부호와 절대값으로 표현된 값으 ㄹ부호 비트를 제외한 나머지 비트들을 0은 1로 1은 0으로 변환한다.
    - 2의 보수
        - 1의 보수방법으로 표현된 값의 최하위 비트에 1을 더한다.

```python
arr = list(map(int, input())
N = len(arr)
num = 0
for i in range(N):
		j = i%7
		num += arr[i]*(2**(6-j))
		if j == 6:
				print(num, end=' ')
				num = 0

print()

```

```python
'''
01D06079861D79F99F
'''

arr = input()
for x in arr:
		num = int(x, 16)
		for j in range(3, -1, -1):
				bit = 1 if num&(1<<j) else 0
				print(bit, end='')
		print(' ', end='')
```