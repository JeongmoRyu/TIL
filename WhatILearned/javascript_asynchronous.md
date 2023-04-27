# javascript 동기와 비동기

### 동기(Synchronous)

- 순서대로 하나씩 처리하는 것
- python 코드가 일반적으로 동기식이다.

### 비동기(Asynchronous)

- 작업을 시작한 후 결과를 기다리지 않고 다음 작업을 처리하는 것 ( 병렬적 수행)
- 시간이 필요한 작업들은 요청을 보낸 뒤에 응답이 빨리 오는 작업부터 처리한다.
- 사용하는 이유
    - 사용자 경험
        - 비동기로 처리한다면 먼저 처리되는 부분부터 보여줄 수 있기에 긍정적인 효과를 볼 수 있다.
        - 동기로 진행하게 되면 앱의 실행 로직에 따라 진행되기에 앱이 멈춘 것과 같은 경험을 받을 수 있기에 이를 방지하고자 한다.

## JavaScript 비동기 처리

- Single Thread 언어, JavaScript
    - Thread : 작업을 처리할 때 실제로 작업을 수행하는 주체로 multi-thread라면 업무를 수행할 수 있는 주체가 여러 개라는 의미
- JavaScript는 하나의 작업을 요청한 순서대로 처리할 수 밖에 없다.
    - 비동기 처리를 할 수 있도록 도와주는 환경이 필요하다.
    - Runtime : 특정 언어가 동작할 수 있는 환경
    - JS는 비동기 관련한 작업은 브라우저 또는 Node 환경에서 처리한다.
        1. JS Engine’s Call Stack
            1. 요청이 들어올 때마다 순차적으로 처리하는 Stack (LIFO)
            2. 기본적인 Javascript의 Single Thread 작업 처리
        2. Web API
            1. JavaScript 엔진이 아닌 브라우저에서 제공하는 runtime 환경
            2. 시간이 소요되는 작업을 처리 (setTimeout, DOM Event, AJAX )
        3. Task Queue
            1. 비동기 처리된 Callback 함수가 대기하는 Queue(FIFO)
        4. Event Loop
            1. Call Stack과 Task Queue를 지속적으로 모니터링
            2. Call Stack이 비어 있으면 Task Queue에서 가장 오래된 작업으로 push

```html
JS 비동기 처리 동작 방식
- 모든 작업은 Call Stack (LIFO)
- 오래걸리는 작업이 들어오면 Web API로 보내 별도로 처리하도록 한다.
- Web API에서 처리가 끝난 작업들은 곧바로 Call Stack으로 들어가지 못하고 Task Queue(FIFO)에 순서대로 들어간다.
- Event Loop가 Call Stack이 비어있는 것을 계속 체크하고 Call Stack이 빈다면 TQ에서 가장 오래된 작업을 Call Stack으로 보낸다.

```

## Axios

- js의 HTTP 웹 통신을 위한 **라이브러리**
- 확장 가능한 인터페이스와 쉽게 사용할 수 있는 **비동기 통신** 기능을 제공
- **node 환경**은 npm을 이용해서 설치 후 사용할 수 있고 browser 환경은 CDN을 이용해서 사용할 수 있다.
    - 공식문서
        - https://axios-http.com/kr/docs/intro
        - https://github.com/axios/axios

- Axios 사용하기

```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
		axios.get('요청할 URL')
		.then(성공하면 수행할 콜백함수)
		.catch(실패하면 수행할 콜백함수)
		// 위의 두 함수를 많이 사용한다.

		.finally(무조건 실행하는 함수)
	</script>
```

- 야옹이 사진 불러오기

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

  <button>야옹아 이리온</button>

  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
      console.log('고양이는 야옹')
      const catImageSearchURL = 'https://api.thecatapi.com/v1/images/search'
      const btn = document.querySelector('button')
      btn.addEventListener('click', function() {
        axios.get(catImageSearchURL)
          .then((response) => {
            // console.log(response.data)
            console.log(response.data[0].url)
            imgElem = document.createElement('img')
            imgElem.setAttribute('src', response.data[0].url)
            document.body.appendChild(imgElem)
            
          })
          .catch((error) => {
            console.log('실패했다옹')
          })
  
        console.log('야옹야옹')
      })

  </script>
  
</body>
</html>
```

- 야옹이 연습 더하기

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
  <div id="cat-container"></div>
  <button id="cat_get_button">hello!! cat</button>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const catSearchUrl = "https://api.thecatapi.com/v1/images/search"
    const catButton = document.querySelector("#cat_get_button")

    catButton.addEventListener('click', () => {
      axios({
        method: 'get',
        url: catSearchUrl,

      })
      .then(response => {
        console.log(response)
        return response.data
      })
      .then(responseBody => {
        console.log(responseBody)
        console.log(responseBody[0].url)
        const catImgElem = document.createElement('img')
        catImgElem.setAttribute('src', responseBody[0].url)

        const catContainer = document.querySelector('#cat-container')
        catContainer.childNodes.forEach(element => element.remove())
        catContainer.appendChild(catImgElem)
      })
      .catch(error => {
        console.log(error)
      })
    })
  </script>
  
</body>
</html>
```

## Callback 과 Promise

- 비동기 처리의 단점
    - 코드의 실행 순서가 불명확하다는 단점이 있다.
    - 실행 결과를 예상하면서 코드를 작성할 수 없게 한다.
        - callback 함수를 사용해서 해결할 수 있다.

### Callback Function

- Callback Hell
    - 콜백 함수는 연쇄적으로 발생하는 비동기 작업을 순차적으로 동작할 수 있게 한다.
    - 비동기 처리를 위한 콜백을 작성할 때 마주하는 문제를 Callback hell이라고 하며 이때의 코드 작성 형태가 마치 피라미드와 유사하여 Pyramid of doom이라고도 한다.

### Promise

- Callback Hell 문제를 해결하기 위한 비동기 처리를 위한 객체
- 비동기 작업의 완료 또는 실패를 나타내는 객체 - 하겠다는 약속

```html
const myPromise = axios.get()
지정해놓고 사용할 수도 있다.
```

- 성공 : then(callback)
    - 이전 작업의 성공 결과를 인자로 전달 받는다.
- 실패 : catch(callback)
    - 이전 작업의 실패 객체를 인자로 전달 받는다.
- 계속 해서 chaining 할 수 있다.

```html
work1()
	.then((result1) => {
		// work2
		return result2
})
	.then((result2) => {
		// work2
		return result3
})
	.catch((error) => {
		// error handling
}) 
```

- 멍뭉이 불러오기

```html
s<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <button>hello Doggy!!</button>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const dogImageSearchURL = "https://dog.ceo/api/breeds/image/random"
    const dogBtn = document.querySelector('button')
    dogBtn.addEventListener('click', function() {
      axios({
        method: 'get',
        url: dogImageSearchURL
      })
      .then((response) => {
        const imgSrc = response.data.message
        return imgSrc
        
      })
      .then((imgSrc) => {
        const imgTag = document.createElement('img')
        imgTag.setAttribute('src', imgSrc)
        document.body.appendChild(imgTag)
      })
      .catch((error) => {
        console.log(error)
      })
    })
  </script>
</body>
</html>
```

