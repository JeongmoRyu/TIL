# vue data management

## Data in components

- 동적 웹페이지를 만들고 있기에 다뤄야 할 데이터가 존재한다.
- 부모, 자식 관계가 아닌 일반적인 컴포넌트 연결의 단점
    - 데이터의 흐름을 파악하기 힘들다.
    - 개발 속도가 저하된다.
    - 유지 보수 난이도가 증가된다.
- 부모 자식 관계만 데이터를 주고 받게 한다면?
    - 데이터의 흐름을 파악하기 쉬워직로
    - 유지 보수가 용이해진다.

- 부모 → 자식 데이터의 흐름
    - pass props 방식
- 부모 ← 자식 데이터의 흐름
    - emit event 방식

## Pass Props

- 요소의 속성을 사용하여 데이터 전달
- props는 부모 컴포넌트의 정보를 전달하기 위한 사용자 지정 특성
- 자식 컴포넌트는 props옵션을 사용하여 수신하는 props를 명시적으로 선언해야한다.

```jsx
가장 큰 예시로는 HelloWorld 컴포넌트에서 msg
<HelloWorlkd msg="Welcome to Yout Vue.js App"/>

HelloWorld.vue에서
<h1> {{msg}} </h1>
```

- Pass Props
    - 부모 → 자식 데이터 전달 방식
    - 정적인 데이터를 전달하는 경우는 static props
    
    ```jsx
    prop-data-name="value"의 형태로 데이터 전달
    	속성 키 kebab-case를 사용한다.
    	자식에서 받는 props는 camal-case로 받는다.
    ```
    
    - props 명시한다.
    
    ```jsx
    일반적인 경우
    props: {
    	msg:String
    }
    
    정적일 경우
    props: {
    	staticProps:String,
    }
    
    ```
    

- Dynamic props
    - 변수를 props로 전달할 수 있다.
    - v-bind directive를 사용해 데이터를 동적으로 바인딩한다.
    - 부모 컴포넌트의 데이터가 업데이트 되면 자식 컴포넌트로 전달되는 데이터 또한 업데이트 된다.
    - 

- 컴포넌트의 data 함수
    - 각 vue 인스턴스는 같은 data 객체를 공유하므로 새로운 data 객체를 반환하여 사용해야한다.
    
    ```jsx
    data : function () {
    	return {
    		// component's data in here
    	}
    }
    ```
    
    ```jsx
    :dynamic-props="dynamicProps"
    앞의 키 값이름으로 데이터를 전달하겠다는 뜻
    ```
    

- 단방향 데이터 흐름
    - 모든 props는 부모에서 자식으로 단방향 바인딩을 형성한다.
    - 부모 속성이 업데이트되면 자식으로 흐르지만 반대방향은 안된다.
        - 부모의 업데이트 되면 자식 컴포넌트의 모든 prop들이 업데이트 된다.

## Emit Event

- 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때는 이벤트를 발생시킨다.
    - 데이터를 이벤트 리스너의 콜백 함수의 인자로 전달받는다.
    - 상위 컴포넌트는 해당 이벤트를 통해 데이터를 받는다.
    
    ```jsx
    $emit('event-name')
    
    - MyChild.vue
    
    <button @click="ChildtoParent">[button]</button>
    
    export default {
    	methods: {
    		ChildtoParent: function () {
    			this.$emit('child-to-parent')
    		}
    	}
    }
    
    - 데이터를 전달하고 하고 싶을 때는 this.$emit('child-to-parent', 'data')
    	- 데이터의 이름을 꼭 같게 맞출 필요는 없다. 
    	- 하지만 emit로 쓰는 것은 같게 해서 받아주어야한다.
    
    - MyComponent.vue
    
    <MyChild... 
    @child-to-parent="parentgetEvent"
    />
    
    export default {
    	methods: {
    		parentgetEvent: function () {
    			console.log("this is the way to emit evnet!")
    		}
    	}
    }
    ```
    
    - 데이터도 전달할 수 있다.
    
    ```jsx
    this.$emit('child-to-parent', 'data')
    
    - 데이터를 전달하고 하고 싶을 때는 this.$emit('child-to-parent', 'data')
    	- 데이터의 이름을 꼭 같게 맞출 필요는 없다. (ex inputData)
    	- 하지만 emit로 쓰는 것은 같게 해서 받아주어야한다. (ex. 'child-to-parent')
    
    export default {
    	methods: {
    		parentgetEvent: function (inputData) {
    			console.log("this is the way to emit evnet!")
    			console.log(`hello ${inputData}`)
    		}
    	}
    }
    
    ```
    
    - 
    
    사용하는 함수
    
    created
    
    mounted
    

## Lifecycle Hooks

- 각 vue 인스턴스는 생성과 소멸의 과정 중 단계별 초기화 과정을 거친다.
    - vue 인스턴스가 생성된 경우 인스턴스를 DOM에 마운트하는 경우 데이터가 변경되어 DOM을 업데이트하는 경우
- 각 단계가 트리거가 되어 특정 로직을 실행할 수 있다.
    
    ```jsx
    export default {
    ...
    	beforCreate() {
    		console.log('beforeCreate')
    	},
    	created() {
    		console.log('created')
    	},
    	beforeMount() {
    		console.log('beforeMount')
    	},
    	mounted() {
    		console.log('mounted')
    	}}
    ```
    
    - lifecycle hooks의 특징
        - 부모 컴포넌트의 mounted hook이 실행되었다고 해서 자식이 mount된 것은 아니고 또한 updated되었다고 update되는 것이 아니다.
            - instance마다 각각의 lifecycle을 가지고 있기 때문이다.