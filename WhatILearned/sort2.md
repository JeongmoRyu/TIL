

병합정렬

mergesort

```python

def merge_sort(numbers):

    if len(numbers) == 1:
        return numbers

    mid = len(numbers)//2
    left_numbers = merge_sort(numbers[:mid])
    right_numbers = merge_sort(numbers[mid:])

    left_idx = right_idx = k = 0

    while left_idx < len(left_numbers) and right_idx < len(right_numbers):
        if left_numbers[left_idx] < right_numbers[right_idx]:
            numbers[k] = left_numbers[left_idx]
            left_idx += 1
        else:
            numbers[k] = right_numbers[right_idx]
            right_idx += 1
        k += 1

    if left_idx < len(left_numbers):
        numbers[k:] = left_numbers[left_idx:]
    if right_idx < len(right_numbers):
        numbers[k:] = right_numbers[right_idx:]

    return numbers


    ans = 0

    merge_sort(arr)

```

분할정복

퀵정렬

```python



    def solve(board):

        if len(board) <= 1:
            return board

        ans = board[len(board) // 2]
        less = []
        more = []
        equal = []
        for num in board:
            if num < ans:
                less.append(num)
            elif num > ans:
                more.append(num)
            else:
                equal.append(num)
        return solve(less) + equal + solve(more)

    solve(arr)

```