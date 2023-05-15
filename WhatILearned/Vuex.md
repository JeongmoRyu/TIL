# vuex

## Local storage

- 상태 유지하기
    - MDN 메인 페이지에서 테마를 설정하고 새로 고침해도 유지할 수 있는 방법
    - 개발자 도구 > Application > Local Storage에서 확인
        - theme key에서 light value 저장

- Window.localStorage
    - 브라우저의 내장 객체 중 하나
    - key-value 형태로 데이터를 저장할 수 있는 저장소
    - localStorage에 저장된 데이터는 브라우저를 종료해도 계속해서 유지된다.
        - 다른 탭에서 동일한 데이터를 공유할 수 있는 반면 다른 도메인에서 접근할 수 없다.
    
    ```jsx
    setItem(key, value) : key, value 형태로 데이터 저장
    
    getItem(key) : key 값으로 저장된 데이터 불러오기
    ```
    
- JSON.stringify
    - JSON 객체의 메서드
    - 자바스크립트 객체를 JSON 형식의 문자열로 변환하여 반환
- JSON.parse
    - JSON 형식의 문자열을 자바스크립트 객체로 변환하여 반환
    

## Plugins

- Vuex store에 추가적인 기능을 제공하는 확장 기능
- 일반적으로 state의 변화에 감지해 어플리케이션의 성능을 최적화하는 목적을 가진다.

- vuex-persistedstate
    - local storage에 저장해 주는 plugin
    - 종료 후 다시 열었을 때 이전 상태를 유지할 수 있도록 해준다.

```jsx
vuex persistedstate 설치

$ npm i vuex-persistedstate
```

- index.js

```jsx
import createPersistedState from 'vuex-persistedstate'

Vue.use(Vuex)

expero default new Vuex.Store({
	plugins: [
		createPersistedState( ),
],
})
```

## Vuex Binding Helper

- vuex store의 state, mutations, actions 등을 간단하게 사용할 수 있도록 만들어진 헬퍼 함수
- mapState, mapActions와 같은 형식으로 사용한다.

```jsx
import {mapState, mapActions} from 'vuex'
```

- 객체 → 이름을 바꾸거나 추가 기능을 구현할 때
- 배열 → 일반적인 형태로 사용할 때

- mapState
    - vuex store 상태를 컴포넌트의 데이터에 매핑할 때 사용한다.
    - 객체 혹은 배열 형태로 상태를 매핑하여 사용할 수 있다.
    - 객체
        - mapState import
        - Spread operator를 사용하여 mapState 전개
        - mapState 내부에 불러오고자 하는 값을 정의하고 arrow함수를 사용하여 할당한다.
        - key값을 다른이름으로 변경하여 사용 할 수 있다.
    
    - 배열
        - mapState import
        - Spread operator를 사용하여 mapState 전개
        - vuex store 상태 중 불러오고자 하는 대상을 배열의 원소로 정의한다.
        

```jsx
원래 쓰는 방법
message() {
      return this.$store.state.message
    },

import {mapState } from 'vuex'
배열 상태로 쓸때
...mapState(['message']),

객체로 받을 때
...mapState({
  message: state => state.message
}),
```

- mapActions
    - 컴포넌트에서 this.$store.dispatch()를 호출하는 대신 액션 메서드를 직접 호출하여 사용할 수 있다.
    - mapState와 같이 객체 혹은 배열 형태로 매핑 가능하다.
    - 객체 형태로 매핑
        - this.———로 사용하여 payload를 넘겨주거나 추가적인 로직을 작성하는 것이 가능하다.
    - 배열 형태로 매핑
        - mapState와 동일한 방식으로 사용하지만 inputData를 호출시 인자로 직접 값을 넘겨주어야 한다.

```jsx
원래 쓰는 방법

<input type="text" @keyup.enter="changeMessage" v-model="inputData">

methods: {
    changeMessage() {
      const newMessage = this.inputData
      this.$store.dispatch('changeMessage', newMessage)
      this.inputData = null
    },
  },

mapActions를 사용할 때 

배열로 받을 때
import {mapState, mapActions } from 'vuex'

<input type="text" @keyup.enter="changeMessage(inputData)" v-model="inputData">
methods: {
    ...mapActions(['changeMessage'])
  },

객체로 받을 때
import {mapState, mapActions } from 'vuex'

<input type="text" @keyup.enter="Onsubmit" v-model="inputData">
methods: {
    ...mapActions({
      actionsChangeMessage: 'changeMessage'
    }),
    onSubmit() {
      const newMessage = this.inputData
      this.actionsChangeMessage(newMessage)
      this.inputData = null
    }
  },
}
```

- Modules
    - vuex store를 여러 파일로 나눠서 관리할 수 있게 해 주는 기능
    - vuex store와 동일한 구성을 가진 별도의 객체를 정의하여 modules 옵션에 작성한 객체를 추가하여 사용한다.
    - 별개의 .js파일에 정의하고 import하는 방식으로도 사용가능하다.
    - Store의 가독성을 향상시킬 수 있다.