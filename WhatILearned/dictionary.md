
## Dict

- dictionary 만들기, 가져오기, 바꾸기

```python
# 만들기
dict_a = {}
dict_b = dict()
dict_a = {
    'a' : 'apple',
    'b' : 'banana',
    'list' : [1, 2, 3]
}

# 값 가져오기

print(dict_a['list'][0])
print(dict_a['a'])
dict_b = dict(a='apple', b='banana', list=[1, 2, 3])
print(dict_b['list'][1])
print(dict_b['b'])

# 값 바꾸기
dict_a['b'] = 'bread'
dict_a['c'] = 'chocolate'
```

- 딕셔너리 - 리스트

```python
dict_to_list = {'a': 10, 'b': 20,}
print(list(dict_to_list))
print(dict_to_list)
print(tuple(dict_to_list))
```

- **추가 메서드 활용**

```python 
points = {'A': 20, 'B': 25}
print(points.keys())   # key로 구성된 결과
print(points.values()) # value로 구성된 결과
print(points.items())

for student in points:
    print(student, points[student])
```

- **enumerate 활용**

```python
lists = ['A', 'B', 'C']
for idx, number in enumerate(lists):
    print(idx,number)
```

= 

```python 
0 A
1 B
2 C
```

**List 활용하기**

- **code for 변수 in iterable**
    - ex) list = [number**2 for number in range(1,5)]
    - ex) list_dict = {number: number**2 for number in range(1,5)}
        - dictionary 로도 가능하다.
        
- **code for 변수 in iterable if 조건 식**

**리스트에서 혈액형 딕셔너리 만들기**

```python
blood_types = [ 'A','A','O', 'B', 'A', 'O', 'AB','O', 'A', 'B', 'O', 'B', 'AB']

blood_dict = {}
for x in blood_types:
    try: blood_dict[x] += 1
    except: blood_dict[x] = 1
print(blood_dict)
```