# JavaScript Event

## Event

- Event : HTML 요소에서 발생하는 모든 상황
    - 키보드 키 입력, 브라우저 닫기, 데이터 제출, 텍스트 복사
- Event object
    - 네트워크 활동이나 사용자와의 상호작용 같은 사건의 발생을 알리기 위한 객체
    - 이벤트를 발생했을 때 생성되는 객체
    - DOM 요소는 Event를 받고 수신
    - Event 처리 :  addEventListener(  ) 메서드를 통해 Event 처리기 (Event handler)를 다양한 html 요소에 부착해서 처리한다.
    
    ```python
    EventTarget.addEventListener(type, handler function)
    EventTarget.addEventListener(type, handler function[, options])
    ```
    
    - type : input, click, submit
    - handler function : 지정된 타입의 Event를 수신할 객체
    
    - 버튼 practice
    
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
      <button id="btn">버튼</button>
      <p id="counter">0</p>
      <script>
      // 초기값
      let counterNumber = 0
      // ID가 btn인 요소를 선택
      const btn = document.querySelector('#btn')
      // btn이 클릭 되었을 때마다 함수가 실행됨
      btn.addEventListener('click', function(event) {
        console.log('버튼을 클릭했어요!!!')
        counterNumber += 1
    
        const counter = document.querySelector('#counter')
        counter.innerText = counterNumber
      })
    
      </script>
    </body>
    
    </html>
    ```
    
    - input practice
    
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
      <input type="text" id="text-input">
      <p></p>
      <script>
        // 1. input 선택
        const textInput = document.querySelector('input')
        // 2. input 이벤트 등록
        textInput.addEventListener('input', function(event){
          // input은 이벤트의 대상
          // input의 value를 받아오기
          // 3. input에 작성한 값을 p 태그에 출력하기
          console.log(event)
          console.log(event.target)
          console.log(event.target.value)
    
          const pTag = document.querySelector('p')
          pTag.innerText = event.target.value
        })
    
      </script>
    </body> 
    
    </html>
    ```
    

## Event 전파

- DOM 요소에서 발생한 이벤트가 상위 노드에서 하위 노드, 하위 노드에서 상위 노드로 전파되는 현상
- addEventListner 메서드를 사용하여 전파 방식을 제어할 수 있음
- Event Bubbling : 기본값은 하위 노드에서 상위 노드로 전파되는 방식을 사용한다.

```html
상위로 전파되지 않도록 중단
- event.stopPropagation()
같은 레벨로도 이벤트가 전파되지 않도록 중단
- event.stopImmediatePropagation();
```

- Event 전파와 취소
    - 현재 Event의 기본 동작을 중단
    - HTML 요소의 기본 동작을 작동하지 않게 막음
    - HTML 요소의 기본 동작 예시
        - a 태그 : 클릭 시 특정 주소로 이동
        - form 태크 : form 데이터 전송

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
  <div>
    <h1>Classified</h1>
  </div>
  
<script>
  const h1=document.querySelector('h1')
  h1.addEventListener('copy', function(evnet) {
    console.log(event)
    event.preventDefault()
    alert("can't copy")
  })
</script>

</body>
</html>
```

- lotto practice

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>프로젝트</title>
  <style>
    /* 스타일은 수정하지 않습니다. */
    .ball {
      width: 10rem;
      height: 10rem;
      margin: .5rem;
      border-radius: 50%;
      text-align: center;
      line-height: 10rem;
      font-size: xx-large;
      font-weight: bold;
      color: white;
    }
    .ball-container {
      display: flex;
    }
  </style>
</head>
<body>
  <h1>로또 추천 번호</h1>
  <button id="lotto-btn">행운 번호 받기</button>
  <div id="result"></div>

  <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
  <script>
    const button = document.querySelector('#lotto-btn')
    button.addEventListener('click', function() {
      const ballContainer = document.createElement('div')
      ballContainer.classList.add('ball-container')

      const numbers = _.sampleSize(_.range(1, 46), 6)

      numbers.forEach((number) => {
        const ball = document.createElement('div')
        ball.classList.add('ball')
        ball.innerText = number
        ball.style.backgroundColor = 'crimson'
        ballContainer.appendChild(ball)
      });
      const result = document.querySelector('#result')
      result.appendChild(ballContainer)
    })
  </script>
</body>
</html>
```

- todo

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
  <form action="#">
    <input type="text" class="inputData">
    <input type="submit" value="Add">
  </form>
  <ul></ul>

  <script>
    const formTag = document.querySelector('form')
    const addTodo = function (event) {
      event.preventDefault() //form 제출 기능 막기
      const inputTag = document.querySelector('.inputData')
      const data = inputTag.value
      if (data.trim()) {
        const liTag = document.createElement('li')
        liTag.innerText = data
        const ulTag = document.querySelector('ul')
        ulTag.appendChild(liTag)
        event.target.reset()
      } else {
        alert('input does not exist')
      }
      
    }
    formTag.addEventListener('submit', addTodo)

  </script>
</body>
</html>
```