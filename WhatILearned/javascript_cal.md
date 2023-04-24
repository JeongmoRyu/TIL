# Javascript calculator

## 연산자

- 할당 연산자
    - 더하기 :+=
    - 빼기 : - =
    - 곱하기 : *=
    - Increment : ++(증감식)
    - Decrement:   —(증감식)
- 비교 연산자
- 동등 연산자( ==)
    - 비교할 때 암묵적 타입 변환을 통해 타입을 일치 시킨 후 같은 값인지 비교한다.
    - 두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별
- 일치 연산자 (===)
    - 두 피연산자의 값과 타입이 모두 같은 경우 true
    - 엄격한 비교가 이워지며 암묵적 타입변환이 발생하지 않는다.
- 논리 연산자
    - and : &&
    - or : ||
    - not : !
    - false && true → false
    - true || flase → true
- 삼항 연산자(Ternary Operator)
    - 3개의 피연산자를 사용하여 조건에 따라 값을 반환하는 연산자
    - 가장 앞의 조건식이 참이면 콜론 앞의 값이 반환되며 반대일 경우 뒤의 값이 반환되는 연산자

```jsx
true ? 1:2 //1
false ? 1:2 //2
const result = 3 > 4 ? 'YES':'NO'
console.log(result) //NO

```

- 스프레드 연산자 (Spread Operator)
    - 배열이나 객체를 전개하여 각 요소를 개별적인 값으로 분리하는 연산자
    - 얕은 복사를 위해서도 활용 가능하다.
    

## 조건문

- IF statement
    - 조건은 소괄호 안에 작성한다.(   )
    - 실행할 코드는 중괄호 {   }
        - if
        - else if
        - else

## 반복문

- while
    - 조건문이 참이기만 하면 문장을 계속해서 수행
    
    ```jsx
    // while
    let i = 0
    while(i<10){
      console.log(i) // 0~9
      i = i + 1
    }
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    
    ```
    
- for
    - 특정 조건이 거짓이 될때까지 반복
    
    ```jsx
    //for
    // for (시작조건 ; 종료조건 ; 순회마다 실행코드)
    for (let i = 0; i<6; i++) {
        console.log(i)
    }
    
     0
     1
     2
     3
     4
     5
    
    -> 몇개 조건 생략 가능
    for (; i < 6; i++) {
    		console.log(i)
    }
    // 문법 조건이기 때문에 ;;은 생략하면 안된다.
    
    ```
    
- for … in
    - 객체의 속성을 순회할 때 사용 (속성 이름을 통해 반복)
- for … of
    - 반복 가능한 객체를 순회할 때 사용 (속성 값을 통해 반복)
    - 반복 가능한 객체의 종류 : Array, Set, String 등등
- Array.forEach