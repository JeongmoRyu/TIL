# Vue adv

## Basic of Syntax

- 랜더링 된 DOM을 Vue instance의 data에 선언적으로 바인딩할 수 있는 HTML 기반 template syntax를 사용한다.
    - 렌더링 된 DOM : 브라우저에 의해 보기 좋게 그려질 HTML 코드
    - HTML 기반 template syntax :  HTML  코드에 직점 작성할 수 있는 문법을 제공한다.
    - 선언적으로 바인딩 : Vue instance와 DOM을 연결한다.
- Text Interpolation
    - 가장 기본적인 바인딩(연결) 방법
    - 중괄호 2개로 표기
    - DTL과 동일한 형태로 작성
    - 모두 텍스트로 표현한다.
- RAW HTML
    - v-html directive를 사용하여 data와 바인딩
    - directive-HTML 기반 template syntax
    - HTML의 기본 속성이 아닌 Vue가 제공하는 특수 속성의 값으로 data를 작성한다.

## Directives

- v- 접두사가 있는 특수 속성에는 값을 할당할 수 있다.
    - 값에는JS 표현식을 작성할 수 있다.
- directive의 역할은 표현식의 값이 변경될 때 반응적으로 DOM에 적용한다.

```jsx
v-on : submit.prevent="onSubmit"
```

- v-text
    - template interpolation과 함께 가장 기본적인 바인딩 방법
    - {{   }}와 동일한 역할
- v-html
    - raw html을 표현할 수 있는 방법
    - 사용자가 입력하거나 제공하는 컨텐츠에서는 사용 금지
        - XSS 공격
- v-show
    - 표현식에 작성된 값에 따라 element를 보여줄 것 인지 결정
        - boolean 값이 변경 될 때 마다 반응
        - 대상 element의 display 속성을 기본 속성과 none으로 toggle
        - 요소 자체는 항상 DOM에 렌더링 된다.
        - 바인딩 된 isActive의 값이 false이므로 첫 방문에는 p tag가 보이지 않는다.
        - 화면에서만 display하지 못할 뿐 DOM에는 존재한다.
            - display 속성이 변경되었을 뿐이다.
    - 초기 렌더링 비용이 v-if보다 높을 수 있다.
- v-if
    - v-show와 사용 방법은 동일하다.
    - isActive의 값이 변경될 때 반응한다.
    - 값이 false일 경우 DOM에서 사라진다.
        - v-if, v-else-if, v-else 형태로 사용된다.
    - 초기 렌더링 비용이 v-show보다 낮을 수 있다.

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
  <!-- 1. Text interpolation -->
  <div id="app">
    <p>메시지: {{ msg }}</p>   
    <p>HTML 메시지 : {{ rawHTML }}</p>
    <p>HTML 메시지 : <span v-html="rawHTML"></span></p>
    <p>{{ msg.split('').reverse().join('') }}</p>
  </div>

  <hr>
  
  <!-- 2. v-text & v-html -->
  <div id="app2">
    <!-- 2-1. v-text & {{}} -->
    <p v-text="message"></p>
    <!-- 같음 -->
    <p>{{ message }}</p>

    <!-- 2-2. v-html -->
    <p v-html="html"></p>
  </div>

  <hr>

  <!-- 3. v-show && v-if -->
  <div id="app3">
    <p v-show="isActive">Appear?</p>
    <p v-if="isActive">Appear? or Not?</p>
  </div>
  <a href="https://www.google.com">Google</a>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    // 1. Text interpolation
    const app = new Vue({
      el: '#app',
      data: {
        msg: 'Text interpolation',
        rawHTML : '<span style="color : red">빨간 글씨</span>'
      }
    })

    // 2. v-text && v-html
    const app2 = new Vue({
      el: '#app2',
      data: {
        message : 'Hello!! Ryu',
        html: '<a href="https://www.google.com">Google</a>'
      }
    })

    // 3. v-show && v-if
    const app3 = new Vue ({
      el: '#app3',
      data: {
        isActive: false
      }
    })
    
  </script>
</body>
</html>
```

- v-for
    - for … in … 형식으로 작성한다.
    - 반복한 데이터 타입에 모두 사용 가능하다.
    - index를 함께 출력하고자 한다면  (char, index)형태로 사용가능하다.
    - 배열 역시 문자열과 동일하게 사용 가능하다.
    - 각 요소가 객체라면 dot notation(  .  ) 으로 접근가능하다.
    
    ```jsx
    v-for 사용시 반드시 key 속성을 
    각 요소에 작성해야한다.
    ```
    
    - 특수속성 key
        - 주로 v-for-directive 작성시 사용
        - vue 화면 구성 시 이전과 달라진 점을 확인하는 용도로 활용한다.
        - → key 중복 X
        - 각 요소가 고유한 값을 가지고 있다면 생략가능하다.

```jsx
<div v-for="(char, index) in myStr" :key="index">
      <p>{{ index }}번째 문자열 {{ char }}</p>
</div>
<div v-for="(item, index) in myArr" :key="`ssafy-${index}`">
  <p>{{ index }}번째 아이템 {{ item }}</p>
</div>
<div v-for="(value, key) in myObj" :key="key">
      <p>{{ key }} : {{ value }}</p>
</div>
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
  <!-- 3. v-for -->
  <div id="app">
    <h2>1. String</h2>
    <div v-for="char in myStr">
      {{ char }}
    </div>
    <div v-for="(char, index) in myStr" :key="index">
      <p>{{ index }}번째 문자열 {{ char }}</p>
    </div>

    <h2>2. Array</h2>
    <div v-for="(item, index) in myArr" :key="`ssafy-${index}`">
      <p>{{ index }}번째 아이템 {{ item }}</p>
    </div>

    <div v-for="(item, index) in myArr2" :key="`arry-${index}`">
      <p>{{ index }}번째 아이템</p>
		  <p>{{ item.name }}</p>
    </div>

    <h2>3. Object</h2>
    <div v-for="value in myObj">
      <p>{{ value }}</p>
    </div>

    <div v-for="(value, key) in myObj" :key="key">
      <p>{{ key }} : {{ value }}</p>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        // 1. String
        myStr: 'Hello, World!',

        // 2-1. Array
        myArr: ['python', 'django', 'vue.js'],

        // 2-2. Array with Object
        myArr2: [
          { id: 1, name: 'python', completed: true},
          { id: 2, name: 'django', completed: true},
          { id: 3, name: 'vue.js', completed: false},
			  ],
        
        // 3. Object
        myObj: {
          name: 'harry',
          age: 27
        },
      }
    })
  </script>
</body>
</html>
```

- v-on
    - ‘:’ 를 통해 전달받은 인자를 확인한다.
    - 값으로 JS 표현식 작성
    - addEventListener의 첫번째 인자와 동일한 값들로 구성한다.
    - 대기하고 있던 이벤트가 발생하면 할당된 표현식 실행한다.
    - method를 통한 data 조작도 가능하다.
    - method에 인자를 넘기는 방법은 일반 함수를 호출할 때와 동일한 방식
    - ‘:’ 을 통해 전달된 인자에 따라 특별한 modifiers (수식어)가 있을 수 있다.
        
        ```jsx
        v-on:keyup.enter
        ```
        
        - ‘@’ shortcut 제공 축약버전
        
        ```jsx
        @keyup.click
        ```
        

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .red-text {
      color: red;
    }
    .border-black {
			border: solid 1px black;
		}

    .dark-mode {
      color: white;
      background-color: black
    }

    .white-mode {
      color: black;
      background-color: white;
    }
  </style>
</head>
<body>
  <div id="app">
    <button v-on:click="number++">increase Number</button>
    <p>{{ number }}</p>

    <button v-on:click="toggleActive">toggle isActive</button>
    <p>{{ isActive }}</p>

    <button @click="checkActive(isActive)">check isActive</button>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        number: 0,
        isActive: false,
      },
      methods: {
        toggleActive: function () {
          this.isActive = !this.isActive
        },

        checkActive: function (check) {
          console.log(check)
        }
      }
    })
  </script>
</body>
</html>
```

- v-bind
    - html 기본 속성에 vue data를 연결
    - class의 경우 다양한 형태로 연결 가능하다.
        - 조건부 바인딩
            - {’class Name’ : ‘조건 표현식’ }
            - 삼항 연산자도 가능하다.
        - 다중 바인딩
- [’JS 표현식’, ‘JS 표현식’. ….]

- vue nstacne가지 opions 중 하나
- computed 객체에 정의한 함수를 페이지가 최초로 렌더링 될 때 호출하여 계산
    - 계산 결과가 변하기 전까지 함수를 재호출하는 것이 아닌 계산된 값을 반환한다.
- filter
    
    ```jsx
    | 를 사용하여 필터화한다.
    ex) <p>{{ students|Undertwentyfive|tallerthansevenfoot }}</p>
    ```
