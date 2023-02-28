# Sort

- Bubble_sort

```python
def bubble_sort(numbers):
    count = len(numbers)
    # 총 패스 수
    for i in range(count - 1):
        # 한 패스당 비교 횟수
        for j in range(count - i - 1):
            if numbers[j] > numbers[j + 1]:
                numbers[j], numbers[j + 1] = numbers[j + 1], numbers[j]
                # C 스타일
                # temp = numbers[j]
                # number[j + 1] = numbers[j]
                # numbers[j] = temp
    return numbers

```

- counting_sort


```python
def counting_sort(numbers):
    k = max(numbers)
    counts = [0] * (k+1)
    number_count = len(numbers)

    # counts 원소 채워주기
    for i in range(number_count):
        counts[numbers[i]] += 1

    # counts 누적합
    for i in range(number_count - 1):
        # 직전합 더하기
        counts[i + 1] += counts[i]

    # 반환용
    result = [0] * number_count
    # 끝에서 부터 앞으로 한칸씩 오면서 반환하기기
    for i in range(number_count - 1, -1, -1):
        counts[numbers[i]] -= 1
        result[counts[numbers[i]]] = numbers[i]

    return result

# counts = [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
number_list = [2, 4, 7, 1, 3, 5, 6, 9, 8, 0]
print(counting_sort(number_list))
```

- selection sort(선택 정렬)

```python
def selection_sort(numbers):
    number_count = len(numbers)
    # 지금 넣을 위치 i
    for i in range(number_count - 1):
        # 비교 대상 index
        min_index = i
        # 나보다 뒤에 애들을 비교
        for j in range(i, number_count - 1):
            # 가장 작은 애가 어디 있었는지 기록
            if numbers[j + 1] < numbers[min_index]:
                min_index = j + 1
        # 가장 작은 얘랑 현재 (미정렬) 위치와 교환
        numbers[min_index], numbers[i] = numbers[i], numbers[min_index]

    return numbers

number_list = [2, 4, 7, 1, 3, 5, 6, 9, 8, 0]
print(selection_sort(number_list))
```