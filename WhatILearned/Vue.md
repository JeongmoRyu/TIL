# Vue fe

- Evan You 개발자
    - 구글의 Angular 개발자 출신
        - 입문자가 시작하기 좋은 Framework
        - Angular보다 가볍고 간편하게 사용할 수 있다.
- Vue 기본구조 (3가지 다 이용할 수 있다.)

```html
//html
<template>
	<div>
		<p>hello worlds!!!</p>
	</div>
</template>

//javascript
<script>

</script>

//CSS
<style>
</style>
```

- CDN
    - vue2 한글
    
    ```html
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    ```
    
    - practice
    
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
      <div id="app">
        <p id="name">name : {{message}} </p>
        <input id="inputName" type="text" v-model="message">
      </div>
      
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
        // CODE HERE
        const app = new Vue({
          el: '#app',
          data: {
            message: '',
          }
        })
      </script>
    </body>
    </html>
    ```
    
    ## MVVM Pattern
    
    - 소프트웨어 아키텍처 패턴의 일종
    - 마크업 언어로 구현하는 그래픽 사용자 인터페이스(view)의 개발을 BE(model)로 분리시켜 view가 어느 특정한 모델 플랫폼에 종속되지 않도록 한다.
    - View : 실제로 보는 부분 DOM
    - Model : 실제 데이터 JSON
    - View Model  : view를 위한 model, view와 바인딩되어 액션을 주고 받음
    
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
      <div id="app">
        <p>{{message}} </p>
        <p>{{movie}} </p>
        <p>{{message}} </p>
        <p>{{movie}} </p>
        <p>{{message}} </p>
        <p>{{movie}} </p>
    
      </div>
      <!-- Vue CDN -->
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
        const app = new Vue({
          el:'#app',
          data: {
            message:'',
            movie:'terminator',
          },
          methods: {
            print: function() {
              console.log('printing...')
            },
            bye() {
              this.message = this.message + 'hi'
            },
            arrowBye: () => {
              this.message = 'Arrow Frunction'
              console.log(this)
            }
          }
        })
      </script>
    </body>
    </html>
    ```