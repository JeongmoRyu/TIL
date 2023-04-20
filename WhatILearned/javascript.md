# JavaScript

- JavaScript는 클라이언트 측 웹(브라우저)에서 실행한다.
- 웹 페이지가 어떻게 작동하는지 디자인/프로그래밍 등 웹 페이지 동작을 제어하는데 널리 사용한다.
- WEB 기술의 기반이 되는 언어
    - HTML 문서의 콘텐츠를 동적으로 변경할 수 있는 언어
    - 가장 인기 있는 언어

## JavaScript Engine

- 자바 스크립트 코드를 실행하는 프로그램 또는 인터프리터(대체적으로 웹 브라우저에서 사용한다.)
- HTML/CSS/Javascript를 이해한 뒤 해석한다.
- 각 브라우저마다 자체 javascript engine을 개발, 사용한다.
    - V8 - Chrome
    - Chakra - Microsoft Edge
    - JSC (Javascript Core) - Apple(safari)
    - SpiderMonkey - FireFox

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

</head>
<body>

  <!-- body 바로 위에 script태그를 써줘야한다. -->
  <script>
		console.log('hello')
  </script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

</head>
<body>

  <!-- body 바로 위에 script태그를 써줘야한다. -->
  <script type="text/javascript" src="index.js">
  </script>
</body>
</html>
```

```jsx
console.log('hello')
```

## EcmaScript

- Ecma International(전자 정보 통신 시스템 표준화 기수)이 ECMA-262 규격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어를 뜻한다.
- JavaScript의 기본적인 문법, 데이터 타입, 객체 모델, 함수, 연산자 등을 정의
- 한줄 주석 (//), 여러 줄 (/**/)
- 들여쓰기 2칸
- 블럭(block)은 if , for, 함수에서 중괄호 {   } 내부를 말한다.
    - python은 들여쓰기를 이용해서 코드 블럭 구분
    
- 다양한 코드 스타일
    - Airbnb Javascript style guide
    - Google Javascript style guide
    - Javascript standard style

## 변수와 식별자

- 식별자 - 문자, 달러, 밑줄로 시작한다.
- 대소문자 구분하고 클래스 명 외에는 소문자로 시작한다.
- 예약어 사용 불가능
    - for, if, function
- 카멜 케이스(Camel case)
    - 변수, 객체, 함수에 사용
- 파스칼 케이스(Pascal case)
    - 클래스, 생성자에 사용
- 대문자 스네이크 케이스(SNAKE CASE)
    - 상수에 사용한다.
        - 변경될 가능성이 없는 값
        
- 변수 선언 키워드
    - let
        - 블록 스코프 지역 변수를 선언 (추가로 동시에 값을 초기화)
        - 재할당 가능 & 재선성 불가능
        - 블록 스코프를 갖는 지역 변수를 선언
            - 선언과 동시에 원하는 값으로 초기화 할 수 있음
    
    - const
        - 블록 스코프 읽기 전용 상수를 선언 (추가로 동시에 값을 초기화)
        - 재할당 불가능 & 재선언 불가능
        - 선언 시 반드시 초기값을 설정해야하며 이후 값 변경이 불가능하다.
            - 블록 스코프를 가진다.
        
        ```jsx
        const me = {
            me:'RYU'
        }
        console.log(me)
        
        {me: 'RYU'}
        ```
        
    
    - var
        - 변수를 선언
            - 추가로 동시에 값을 초기화
        - 재할당 가능 & 재선언 가능
        - hoisting(호이스팅) 되는 특성으로 인해 예기치 못한 문제를 발생할 수 있다.
            - 최근 버젼에서는 const, let을 사용하는 것을 권장한다.
- practice

```jsx
const element = document.getElementById('target')
element.style.height = '100px'
element.style.width = '100px'
element.style.backgroundColor = 'blue'

function funcReturn() {
  let a = 1
  let b = 2
  return a + b
}

console.log(funcReturn())

function funcRetParams(paramsA, paramsB, paramsC) {
  return `${paramsA}-${paramsB}-${paramsC}`
}

console.log(funcRetParams(1, 2, 3))
console.log(funcRetParams(4, 5))
console.log(funcRetParams(6))
```

## 데이터 타입

- JavaScript의 모든 값은 특정한 데이터 타입을 가진다.
    - 크게 원시 타입(Primitive type)과 참조 타입(Reference type)으로 분류된다.
- 원시 타입
    - Number : 정수, 실수형 숫자
        - NaN을 반환하는 경우
            - 숫자로서 읽을 수 없다.
            - 결과가 허수인 수학 계산식
            - 피연산자가 NaN
            - 정의할 수 없는 계산식
            - 문자열을 포함하면서 덧셈이 아닌 계산식
            
            ```jsx
            const a = 13
            let b = 1.3
            const PI = 3.14
            
            // floating point 표현
            const f = 1.2345e8
            console.log(f)
            
            // 특이 숫자
            const inf = Infinity
            console.log(inf)
            const infNegativate = -Infinity
            const NotANumber = NaN
            console.log(NotANumber)
            
            Number.isFinite(a) // true
            Number.isFinite(inf) //false
            
            Number.isNaN(NotANumber) // true
            Number.isNaN(f) //false
            
            console.log(parseInt("1234"))
            console.log(parseInt("NaN"))
            console.log(parseInt("Infinite"))
            ```
            
            ```jsx
            123450000
            Infinity
            NaN
            1234
            NaN
            NaN
            ```
            
    - String : 문자열
        - 작은 따옴표, 큰 따옴표 모두 가능
        - 덧셈을 통해 문자열 끼리 붙일 수 있다.
        - escape key를 통해 줄 바꿈 가능
            
            ```jsx
            console.log('안녕 \n 하세요')
             안녕 
             하세요
            ```
            
        - Template Literal을 사용하면 줄 바꿈 가능하다. 문자열 사이에 변수도 삽입할 수 있다. ${  expression  }
        
        ```jsx
        // 문자열
        const sentence = "lorem ipsum sit dolor amet"
        const naver = "Global searching website"
        console.log(sentence)
        console.log(naver)
        
        // template literal(문자 그대로)
        const literal = `${ naver } is wow` 
        // backtick을 사용하는 것
        console.log(literal)
        
        const expression = `${1+2+4 / 0}`
        console.log(expression)
        
        // Boolean
        const varTrue = true // 대문자 안씀
        const varFalse = false
        ```
        
    
    - empty value : 값이 존재하지 않음을 표현하는 값
        - null : 값이 없음
            - 변수의 값이 없음을 의도적으로 표현
        - undefined : 값이 할당되지 않은 변수
            - 변수 선언 이후 직접 값을 할당하지 않으면 자동으로 할당된다.
        - null vs undefined
            - typeof 연산자를 통해 타입을 확인 했을 때 object vs undefined로 확인 가능하다.
    - Boolean : 참(True)과 거짓(False)
        - 조건문 또는 반복문에서 유용하게 사용가능하다.
        - 자동 형변환 규칙에 따라 true, false로 변환된다.
    - Symbol : 유일한 값을 표현하는 자료형

- 참조타입( Reference type)
    - object : 이름과 값을 가진 속성들의 집합으로 이루어진 자료구조
        - key
            - 문자열 타입만 가능
            - key 이름에 띄어쓰기 등의 구분자가 있으면 따옴표로 묶어서 표현
        - value
            - 모든 타입 가능(함수 포함)
        - 객체 요소 접근
            - . , []
    
    - array : 여러 개의 값을 순서대로 저장하는 자료구조
        - 순서를 보장하는 특징이 있음
        - [   ]를 이용해 생성하고 0을 포함한 양의 정수 인덱스로 특정 값에 접근 가능하다.
        - 길이 : array.length
    - function : function 키워드를 통해 생성하며, 호출 시 실행될 코드를 정의
        - 함수 선언식(function declaration)
            - 표현식 내에서 함수를 정의하는 방식
            - 함수 표현식은 함수의 이름을 생략한 익명 함수로 정의 가능하다.
            - 함수 이름을 명시하는 것도 가능하다.
                - 호출에 사용되지 못하고 디버깅 용도로 사용된다.
        - 함수 표현식(function expression)