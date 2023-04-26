# JavaScript Dom

- JavaScript는 웹 페이지에서 다양한 기능을 구현하는 스크립트 언어
- 정적인 정보만 보여주던 웹 페이지를 데이터가 주기적으로 갱신되거나 사용자와 상호 작용을 하거나 애니메이션 등이 동작하게 하는 것을 가능하게 한다.

## DOM

- Brower APIs
    - 웹 브라우저에 내장된 API로 웹 브라우저가 현재 컴퓨터 환경에 관한 데이터를 제공하거나 오디오를 재생하는 등 여러가지 유용하고 복잡한 일을 수행할 수 있게 한다.
    - 이외 종류 : Geolocation API, WebGL
- 문서 객체 모델(Document Object Model)
    - 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공한다.
        - HTML  /  CSS 조작으로 쉽게 변경할 수 있다.
    - HTML 문서를 구조화하여 각 요소를 객체로 취급한다.
    - 단순한 속성 접근, 메서드 활용 뿐 아니라 프로그래밍 언어적 특성을 활용한 조작이 가능하다.

### DOM Structure

- Node로 표현한다.
- 문서를 논리 트리로 표현한다.
- 각 Node는 부모, 자식 관계를 형성하고 이에 따라 상속 개념도 동일하게 적용된다.
- DOM의 객체
    - window
        - DOM을 표현하는 창
        - 가장 최상위 객체 (생략 가능)
        - method
        
        ```jsx
        window.open()
        window.alert()
        window.print()
        ```
        
    - document
        - 브라우저가 불러온 웹 페이지
        - 페이지 컨텐츠의 진입점 역할을 하며 body와 같은 수많은 다른 요소들을 포함하고 있다.
        - 속성
        
        ```jsx
        HTML <title> : 웹페이지 제목 수정
        
        ```
        
    - navigator, location, history, screen

### DOM 조작

- 선택(SELECT)
- 조작(MANIPULATION)
    - 생성, 추가, 삭제

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1 id="title">DOM 조작</h1>
  <p class="text">querySelector</p>
  <p class="text">querySelectorAll</p>

  <ul>
    <li>Javascript</li>
    <li>Python</li>
  </ul>

  <p>

  </p>
  
  <a href=""></a>

  <script>

  </script>
</body>
</html>
```

```jsx
document.querySelectorAll('#title')
> NodeList [h1#title]

document.querySelectorAll('.text')
> NodeList(2) [p.text, p.text]

document.querySelector('.text')
> <p class="text">querySelector</p>

document.querySelectorAll('body > ul > li')
> NodeList(2) [li, li]
```

- NodeList
    - DOM 메서드를 사용해 선택한 노드의 목록
    - 배열과 유사한 구조를 가진다.
    - Index로만 각 항목에 접근 가능하다.
    - 배열의 forEach 메서드 및 다양한 배열 메서드 사용이 가능하다. - push, pop은 불가
    
    ```jsx
    document.createElement(tagname)
    > 생성
    const title = document.createElement('h1')
    > undefined
    
    HTML.innerText
    > 입력
    title.innerText = 'practice DOM'
    > 'practice DOM'
    
    const div = document.querySelector('div')
    > div 만들어주기
    > undefined
    
    Node.appendChild()
    > 추가 : 한번에 하나의 Node만 추가 가능
    div.appendChild(title)
    > <h1>practice DOM</h1>
    
    Node.remeveChild()
    > 삭제 : 제거된 Node 반환
    div.removeChild(title)
    > <h1>practice DOM</h1>
    ```
    
- 옮길수도 있다.

```jsx
const fruitsList = document.querySelector('#fruits')
> undefined

const banana = document.querySelector('#banana')
> undefined

fruitsList.appendChild(banana)
> <li id="banana">…</li>

```

```jsx
과일 목록
- apple

야채 목록
- cucumber
- banana
```

```jsx
과일 목록
- apple
- banana

야채 목록
- cucumber

```

- 속성 조회 및 설정
    
    ```jsx
    Element.getAttribute(attributeName)
    
    Element.setAttribute(name, value)
    > 해당 속성이 존재하는 경우 갱신
    Element.classList, Element.style
    > 직접적으로 해당 요소의 각 속성들을 제어할 수 있다.
    
    const aTag = document.createElement('a')
    > undefined
    aTag.innerText = 'Google'
    > 'Google'
    aTag.setAttribute('href', 'https://google.com')
    > undefined
    const div = document.querySelector('div')
    > undefined
    div.appendChild(aTag)
    > <a href="https://google.com>Google</a>
    
    ```
    
    - Fruit practice
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS DOM</title>
    </head>
    <style>
      .red {
        color: red;
      }
    
      .big {
        font-size: 32px;
      }
    </style>
    <body>
      <h1>Fruit</h1>
    
      <!-- <button id="event-button">커져라!</button> -->
    
      <ul id="list">
        <li class="red">apple</li>
        <li>orange</li>
        <li id="banana">banana</li>
        <li>grape</li>
        <li class="red">strawberry</li>
      </ul>
      <script>
      // strawberry 아래에 새로운 과일 하나 추가
      // 추가할 테그 만들기
        const mango = document.createElement("li")
        mango.innerText = 'mango' 
        const parent = document.querySelector("ul")
        parent.appendChild(mango)
    
    	// apple 위에 새로운 과일 하나 더 추가하세요
        const pineapple = document.createElement("li")
        pineapple.innerText = "pineapple"
        parent.prepend(pineapple)
    
    	// orange와 banana 사이에 새로운 과일을 하나 더 추가하세요
        const kiwi = document.createElement("li")
        kiwi.innerText = "kiwi"
        const banana = document.querySelector("#banana")
        parent.insertBefore(kiwi, banana)
    
    	// class가 red인 노드 모두 삭제
        const reds = document.querySelectorAll('.red')
        reds.forEach(element => {
          element.remove()
        });
    
    	// 모든 li 태그의 글자 크기를 키워보자
        const liTags = document.querySelectorAll('li')
        liTags.forEach(element => {
          element.classList.add('big')
        });
    
    	// 버튼을 누르면 이벤트 실행하기 
      const button = document.querySelector('#event-button')
      addEventListener('click', () => {
        changeFont()
      })
      
      function changeFont() {
        const Litags = document.querySelectorAll('li')
        Litags.forEach(element => {
          element.classList.add('big')
        })
      }
    
      </script>
    </body>
    </html>
    ```