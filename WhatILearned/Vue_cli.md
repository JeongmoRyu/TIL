# vue cli

- Node.js 필요
- vue cli
    - vue 개발을 위한 표준 도구
    - 프로젝트의 구성을 도와주는 역할
    - 확장 플러그인, GUI, Bable 등 다양한 tool 제공

```jsx
설치
$ npm install -g @vue/cli

프로젝트 생성
$ vue create vue-cli
- 프로젝트 명 vue-cli
	- vue 2, 3 선택
```

```jsx
Vue CLI v5.0.8
✨  Creating project in C:\Users\SSAFY\Desktop\230502lecture\vue-cli.
🗃  Initializing git repository...
⚙️  Installing CLI plugins. This might take a while...

added 855 packages, and audited 856 packages in 13s

92 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
🚀  Invoking generators...
📦  Installing additional dependencies...

added 92 packages, and audited 948 packages in 3s

105 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
⚓  Running completion hooks...

📄  Generating README.md...

🎉  Successfully created project vue-cli.
👉  Get started with the following commands:

 $ cd vue-cli
 $ npm run serve

뜨면서 설치 완료 
```

- 서버 구동

```jsx
$ npm run serve

App running at:
  - Local:   http://localhost:8080/
  - Network: unavailable

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

- node_modules-Babel
    - JavaScript compiler
        - 자바 스크립트의 ES6+ 코드를 구버전으로 번역 / 변환 해주는 도구
        - 자바 스크립트의 파편화, 표준화의 영향으로 작성된 코드의 스펙트럼이 매우 다양하다.

```jsx
// Babel Input : ES2015 arrow function
[1, 2, 3].map((n) => n+1)

// Babel Output : ES5 equivalent
[1, 2, 3].map(function(n){
		return n+1
})

```

- node_modules-Webpack
    - static module bundler
    - 모듈 간의 의존성 문제를 해결하기 위한 도구
    - 프로젝트에 필요한 모든 모듈을 mapping하고 내부적으로 종속성 그래프를 빌드한다.

- Module
    - 개발하는 애플리케이션의 크기가 커지고 복잡해지면 파일 하나에 모든 기능을 담기가 어려워져 각 파일을 분리하여 관리하였고 이러한 파일이 js 파일 ⇒ module
    - module은 기능 단위로 분리하며 클래스 하나 혹은 특정한 목적을 가진 복수의 함수로 구성된 라이브러리 하나로 구성된다.
    - 
    
- Module의 의존성 문제
    - module 수가 많아지고 의존성이 깊어지면 특정 부분에서 문제가 발생하여 문제 파악이 어려울 수 있다.
    
    → Webpack이 의존성 문제를 해결하기 위해 나왔다.
    
- Bundler
    - 모듈 의존성 문제를 해결해주는 작업이 Bundling
    - module들을 하나로 묶어준다.
    - Vue CLI는 Babel, Webpack 초기 설정을 자동으로 해준다.
    
- public/index.html = bootstrap의 CDN = html base.html
    - 뼈대가 되는 html 파일

- src
    - src/assets : 정적 파일을 저장하는 디렉토리
    - src/components : 하위 컴포넌트들이 위치
    - src/App.vue : 최상위 컴포넌트 ,  index.html과 연결되어 있다.
    

### Component

- UI를 기능별로 분화한 코드 조각
- CS에서 다시 사용할 수 있는 범용성을 위해 개발된 소프틍뒈어 구성 요소
- tree로 구성하는 것이 보편적인 방법이다.
- 컴포넌트는 유지보스를 쉽게 만들어 줄 뿐 아니라 재사용성의 측면에서도 기능을 제공한다.
- Component based architecture 의 늑징
    - 관리가 용이하다.
    - 재사용성
    - 확장이 가능하다.
    - 캡슐화
    - 독립적이다.
    
    ⇒⇒⇒⇒ 비용이 감소된다.
    

### SFC (Single File Component)

- 기본 구조
    - html
    - script
    - style(CSS)
- Tree 구조이기에 div component는 하나만 있어야 한다.
- 사용하는 방법
    1. .vue  파일을 만든다.(src/components 폴더에서)
    2. 불러온다.(여기서부터 App.vue에서)
    
    ```jsx
    import MyComponent from './components/MyComponent.vue'
    ```
    
    1. 등록한다.
    
    ```jsx
    export default {
      name: 'App',
      components: {
        HelloWorld,
        MyComponent,
      }
    }
    ```
    
    1. template에 사용한다.
    
    ```jsx
    <template>
      <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
        <MyComponent />
      </div>
    </template>
    ```
    
    ```jsx
    <template>
      <div class="border">
        <h1> This is Component </h1>
      </div>
      
    </template>
    
    <script>
    export default {
      name: 'MyComponet',
    }
    </script>
    
    <style>
    .border {
      border:solid;
    }
    </style>
    ```
    
- child component를 만들기 위해

```jsx
<template>
  <div>
    <h3>This is child component</h3>
  </div>
</template>

<script>
export default {
  name:'MyChild'
}
</script>

<style>

</style
```

```
<template>
  <div class="border">
    <h1> This is Component </h1>
    <MyChild/>
    <MyChild/>
    <MyChild/>
  </div>
  
</template>

<script>
import MyChild from '@/components/MyChild'

export default {
  name: 'MyComponet',
  components : {
    MyChild,
  }
}
</script>

<style>
.border {
  border:solid;
}
</style>
```

```jsx
<template>
<div class='btn' :class="{'selected':selected}">
    <span>{{label}}</span>
    <span>{{desc}}</span>
  </div>
</template>

<script>

export default {
  name: 'MbtiButton',
  props : {
    label: String,
    desc: String,
  }
}
</script>

<style scoped>
.btn {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 150px;
  border: 1px solid goldenrod;
  border-radius: 10px;
  cursor: pointer;
}
.selected {
  background-color: blueviolet;
}

</style>
```

```jsx
<template>
  <div id="app">
    <HelloWorld msg="Hello This is MBTI World"/>
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="btn-row">
			<MbtiButton label="E" desc="외향형" selected="true"/>
      <MbtiButton label="I" desc="내향형"/>
    </div>
    <div class="btn-row">
      <MbtiButton label="S" desc="현실형"/>
      <MbtiButton label="N" desc="추상형" />
    </div>
    <div class="btn-row">
    <MbtiButton label="T" desc="직관형"/>
    <MbtiButton label="F" desc="공감형"/>
    </div>
    <div class="btn-row">
      <MbtiButton label="P" desc="즉흥형"/>
      <MbtiButton label="J" desc="계획형"/>
    </div>
    <HelloWorld msg="반가워요 친구들"/>
    <HelloWorld msg="Click the button to check MBTI"/>
    <!-- <MyComponent />
    <MyComponent /> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import MyComponent from './components/MyComponent.vue'
import MbtiButton from './components/MbtiButton.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    // MyComponent,
    MbtiButton,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btn-row {
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 10px;
}
</style>
```