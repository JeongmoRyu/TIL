## 데이터 구조



- 여러 데이터를 효과적으로 사용, 관리하기 위한 구조

- List, Tuple, Dict, Set

## 문자열(String)



```jsx
String 메서드

- s.find(x) : 첫번째 위치 반환 없으면 -1 반환
- s.index(x) : 첫번째 위치 반환
- s.isaplha() : 알파벳 문자 여부
- s.isupper() : 대문자
- s.islower() : 소문자
- s.istitle() : 타이틀 형식 여부
- s.replace(x, y[,count]) : x를 y로 바꿔서 반환
- s.strip() : 특정 문자 제거
- s.split() : 공백 기준으로 분리
- s.capitalize() : 첫 글자 대문자
- s.title() : 각 단어 첫 글자 대문자
- s.upper() : 대문자
- s.lower() : 소문자
- s.swapcase() : 대소문자 서로 변경
```

## LIST



- 순서가 있는 구조로 여러 개의 값을 저장
- [  ] , list()

```jsx
List 메서드

- L.append(x) : x 추가
- L.insert(a, x) : a에 x추가
- L.remove(x) : x 제거
- L.pop() : 리스트 가장 오른쪽 반환 후 제거
- L.pop(a) : a번째 반환 후 제거
- L.reverse() : 거꾸로
- L.sort() : 리스트를 정렬
- L.count(x) : X가 몇개인지 카운트

```

## TUPLE



- 여러 개의 값을 순서가 있는 구조로 저장
- 소괄호 () 형태

```jsx
Tuple 메서드
- in : 포함여부
- + : 튜플에 추가하기
- * : 튜플 내용 반복하기
```

## DICT



- 키(key)와 값(value)을 쌍으로 이루어진 자료
- key
    - string
    - interger
    - float
    - boolean
    - tuple
    - range

```jsx
Dictionary 메서드
- d.clear() : 모든 항목 제거
- d.copy() : 복사본 반환
- d.keys() : 키를 반환
- d.values() : 값을 반환
- d.items() : 키와 값의 쌍을 반환
- d.get(key) : key의 값을 반환
- d.get(key, value) : key의 값을 반환 없을 경우 value 반환
	- ex) d.get(key[,default])
- d.pop(key) : key의 값 반환 후 삭제
- d.pop(key, value) : key의 값 반환 후 삭제 없을 경우 value 반환
- d.update(x, y, z) : 값들을 매핑하여 반환
```

### Key Value와 관련한 것 구하기

```python
count=Counter(result)
print(count)
print(count.most_common())
print(sorted(count.items()))
X = sorted(results, key = lambda x : x.get('vote_average'), reverse = True)
평점에 따른 랭킹 구하기

from collections import Counter 카운트 해주는 모듈

Counter_entry.most_common()
Counter_entry
Counter_entry.values()
Counter_exit.keys()
max(Counter_entry.values()
```

## SET



- 중복되는 요소가 없고 순서에 상관없는 데이터들의 묶음
- 가변 자료형

```jsx
SET 메서드

- s.add(x) : 항목x 추가
- s.update(x, y, z) : 여러 항목 x, y, z 추가
- s.copy() : 복사본을 반환
- s.pop() : 랜덤하게 항목 반환하고 항목제거
- s.remove(x) : 항목x 삭제
- s.discard(x) : 항목x 삭제 없어도 에러 발생하지 않음
- s.clear() : 모든 항목 제거
- s.isdisjoint(x) : x의 서로 같은 항목이 없다면 TRUE
	- issubset, issuperset

```
