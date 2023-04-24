# javascript index


## function 함수

- 함수 선언식(Function declaration)
    - function 함수(    ) {   }
- 함수 표현식
    - 변수 키워드 함수 = function (   ) {   }
    - 표현식에서 함수 이름을 명시하는 것도 가능
    - 표현식에서 함수 이름을 명시하는 것도 가능하지만 - 보통 디버깅 용도로 사용된다.
    
- 인자 작성시 = 문자 뒤 기본인자를 선언 가능하다.

```python
const hello = function (name = 'Anonymous') {
	return `Hi ${name}`
}

hello(  )
// Hi Anonymous
```

- 매개변수와 인자의 개수가 불일치하는 것도 허용된다.

### 함수들의 정의

- Spread syntax(…)
    - 전개 구문
        - 배열과 사용
        - 함수와 사용

## 선언식과 표현식

- Hoisting ( 호이스팅 ) 선언식
    - 함수 표현 후 function : 오류 발생 X
    - 함수 표현 후 const : 오류 발생 O

## Arrow Function

- 화살표 함수
- 함수를 비교적 간결하게 정의할 수 있는 문법
    - function 생략 가능
    - 매개변수 (  ) 생략 가능
    - 내용이 한줄이라면 {   } ,   return 도 생략 가능하다.
- 화살표 함수는 익명 함수
    - === 함수 표현식에서만 사용가능하다.

```jsx
const arrow1 = function (name) {
	return `hello ${name}`
}

// function 키워드 삭제
const arrow2 = (name) => {return `hello ${name}`}

// 인자가 1개인 경우 (  ) 생략 가능
const arrow3 = name => {return `hello ${name}`}

// 함수 바디가 return을 포함한 표현식 1개일 경우 { } 과 return 생략 가능
const arrow4 = name => `hello ${name}`
// + object를 return하면 명시적으로 적어줘야한다.
let Objects = () => {return {key:'value'}}
// + 적지 않을려면 괄호를 붙여야한다.
Objects = ( ) => ({key:'value'})

// 인자가 없다면 (  ) , _ 으로 표현 가능하다.
let Args = () => 'No args'
Args = _ => 'No args'

```

## This

- object를 가리키는 키워드
- javascript에서  암묵적으로 전달받는다.
    - 해당 함수 호출 방식에 따라 this에 바인딩 되는 객체가 달라진다.
- 전역 문맥에서 this
    - window를 가리킨다.
        
        ```jsx
        console.log(this)
        // window
        ```
        
- 함수 문맥에서 this : 함수를 호출한 방법에 의해서 결정된다.
    - 단순 호출
        - 전역 객체를 가리킨다.
        - 브라우저에서 전역은 window를 의미한다.
    - Method (객체 메서드)
        - Function in Object
        - 메서드로 선언하고 호출한다면 객체의 메서드이므로 해당 객체가 바인딩한다.
    - Nested
        - forEach의 콜백 함수에서의 this가 메서드의 객체를 가리키지 못하고 전역 객체 window를 가리킨다.
        - 이를 해결하기 위해 ⇒ (화살표 함수)
            - 자신을 감싼 정적 범위
            - 화살표 함수는 호출의 위치와 상관 없이 상위 스코프를 가리킨다.

## Array 와 Object

### Array

- 키와 속성들을 담고 있는 참조 타입의 객체
- 순서를 보장하는 특징이 있다.
- [   ]를 이용해서 생성하고 0을 포함한 양의 정수 idx로 특정 값에 접근 가능하다.
- array.length : 길이
    - 마지막 원소 : arrat[array.length -1]
- reverse : 원본 배열의 요소들을 순서를 반대로 정렬
- push & pop : 가장 뒤에 요소를 추가 또는 제거
- unshift & shift : 가장 앞의 요소들을 추가 또는 제거
- includes : 특정 값이 존재하는지 판별 후 true / false
- indexOf : 특정 값이 존재하는지 판별 후 인덱스 반환 , 없는 경우 -1

```jsx
const numbers = [1, 2, 3, 4, 5]
numbers.reverse()
console.log(numbers) // [5, 4, 3, 2, 1]
number.push(100)
console.log(numbers) // [1, 2, 3, 4, 5, 100]
console.log(numbers.pop()) // 100
console.log(numbers) // [1, 2, 3, 4, 5]
console.log(numbers.includes(1)) // true
console.log(numbers.indexOf(2)) // 1
console.log(numbers.indexOf(7)) // -1
```

- Array Helper Methods
    - 배열을 순회하며 특정 로직을 수행하는 메서드
    - 메서드 호출시 인자로 callback 함수를 받는 것이 특정
        - callback 함수 :  함수 내부에서 실행될 목적으로 인자를 넘겨받는 함수
    - forEach : 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
        
        ```jsx
        const numbers = ['one', 'two', 'three']
        
        Func = function (number) {
        	console.log(number)
        }
        numbers.forEach(Func)
        // one
        // two
        // three
        
        // 함수 정의를 인자로 넣을 수도 있다.
        numbers.forEach(function (number) {
        	console.log(number)
        }
        
        // 화살표 함수를 적용할 수 있다.
        numbers.forEach((number) => {
        	return console.log(number)
        })
        ```
        
    - map :  콜백 함수의 반환 값을 요소로 하는 새로운 배열을 반환한다.
        
        ```jsx
        array.map(function (element, index, array) {
        	// do
        })
        
        array.map(callback(element[, index[, array]]))
        
        const numbers = [1, 2, 3]
        // 정의 표현식
        const squareFunc = function (number) {
        	return number ** 2
        }
        // [1, 4, 9]
        
        // 함수를 다른 함수의 인자로 넣기 (콜백 함수)
        const squareNumbers = numbers.map(squareFunc)
        console.log(squareNumbers)
        // [1, 4, 9]
        
        // 함수 정의를 인자로 넣기
        const squareNumbers = numbers.map(function (number) {
        	return number ** 2 
        })
        console.log(squareNumbers)
        // [1, 4, 9]
        
        // 화살표 함수로도 표현해보자
        const squareNumbers = numbers.map((number)) => {
        	return number ** 2
        })
        console.log(squareNumbers)
        // [1, 4, 9]
        ```
        
    - filter :  콜백 함수의 반환 값이 참인 요소들만 모아서 새로운 배열을 반환한다.
        
        ```jsx
        array.filter(function (element, index, array) {
        	// do
        })
        array.filter(callback(element[, index[, array]]))
        ```
        
    - reduce :  콜백 함수의 반환 값들을 하나의 값(acc)에 누적한 후 반환한다.
        
        ```jsx
        array.reduce(function (acc, element, index, array) {
        	// do
        }, initialValue)
        array.reduce(callback(acc, element, [index[, array]])[, initialValue])
        
        // acc : 이전 callback 함수의 반환 값이 누적되는 변수
        // initialValue (optional) : 최초 callback 함수 호출 시 acc에 할당되는 값, default 값은 배열의 첫번째 값
        
        const numbers = [1, 2, 3]
        const result = numbers.reduce(function (acc, num) {
        	return acc + num
        }, 0)
        
        // acc + num
        // 0   + 1
        // 1   + 2
        // 3   + 3
        // 6
        
        ```
        
    - find : 콜백 함수의 반환 값이 true이면 해당 요소를 반환한다.
        
        ```jsx
        array.find(function (element, index, array) {
        	// do
        }
        array.find(callback(element[, index[, array]]))
        // 찾는 값이 배열에 없으면 undefinded
        ```
        
    - some : 배열의 요소 중 하나라도 판별 함수를 통과하면 true을 반환한다.
        
        ```jsx
        array.some(function (element, index, array) {
        	// do
        })
        array.some(callback(element[, index[, array]]))
        
        const arr = [1, 2, 3, 4, 5]
        const result = arr.some((elem) => {
        	return elem % 2 === 0
        })
        // true
        ```
        
    - every : 배열의 모든 요소가 판별 함수를 통과하면 true을 반환한다.
        
        ```jsx
        array.every(function (element, index, array) {
        	// do
        })
        array.every(callback(element[, index[, array]]))
        
        const arr = [1, 2, 3, 4, 5]
        const result = arr.every((elem) => {
        	return elem % 2 === 0
        })
        // false
        
        ```
        

### Object(객체)

- key
    - 문자열 타입만 가능
    - 띄어쓰기 등의 구분자가 있으면 “   ” 묶어서 표현한다.
- value
    - 모든 타입이 가능하다 (함수 포함)
- 접근을 할때 . [   ] 두다 가능하다.
    - 띄어쓰기가 있으면 대괄호만이 접근 가능하다.
- new
    - 생성자 함수를 사용할 때 사용한다.
    - 함수 이름은 대문자!!
    

### 객체 관련 문법

- ES6
    1. 속성명 축약
        1. 객체를 정의할 때 key와 할당하는 변수의 이름이 같으면 예시와 같이 축약 가능하다.
    2. 메서드명 축약
        1. 메서드 선언 시 function 키워드 생략 가능하다.
    3. 계산된 속성명 사용
        1. 객체를 정의할 때 key의 이름을 표현식을 이용하여 동적으로 생성 가능하다. 
    4. 구조 분해 할당
        1. 배열 또는 객체를 분해하여 속성을 변수에 쉽게 할당할 수 있다.
        
        ```jsx
        const Information = {
        	name: 'Ryu',
        	Id : 'hellojm',
        	email : admin@admin.com
        }
        
        const {name} = Information
        const {Id, email} = Information
        ```
        
    5. 객체 전개 구문(spread operator)
        
        ```jsx
        const arr = {b:2, c:3, d:4}
        const newArr = {a:1, ...arr, e:5}
        console.log(newArr)
        // {a:1, b:2, c:3, d:4, e:5}
        ```