# Vue Router

## Routing

- 네트워크에서 경로를 선택하는 프로세스
- 웹 서비스에서의 라우팅
    - 유저가 방문한 URL에 대해 적절한 결과를 응답하는 것
- Routing in SSR
    - Server가 모든 라우팅을 통제
    - URL로 요청이 들어오면 응답으로 완성된 HTML을 제공한다.
- Routing in SPA/CSR
    - 서버는 하나의 HTML(index.html)만을 제공한다. /  하나의 URL만을 가질 수 있다.
    - 이후 동작은 javascript를 사용한다.

- 필요한 이유
    - URL을 통해 유저가 페이지의 변화를 감지할 수 있다.
    - 무엇을 렌더링 중인지 상태를 알 수 있다.
        - 새로고침
        - 링크 공유 시 첫 페이지 공유
    - 브라우저 뒤로 가지 기능을 가능하게 한다.

## Vue Router

- Vue 공식 라우터
- SPA 상에서 라우팅을 쉽게 개발할 수 있는 기능을 제공
- 라우트에 컴포넌트를 매핑한 후 어떤 URL에서 렌더링을 할지 알려준다.
    - SPA를 MPA처럼 URL을 이동하면서 사용 가능하다.
    - URL이 변경되지 않는 SPA의 단점을 해결할 수 있다.

```jsx
$ vue create vue-router-app
# cd vue-router-app
$ vue add router
```

- App.vue

```jsx
<nav>
	<router-link to='/'>Home</router-link>
	<router-link to='/about'>About</router-link>
<nav>
<router-view/>
```

- views 폴더 생성

- router-link
    - a 태그와 비슷한 기능으로 URL을 이동시킨다.
    - routes에 등록된 컴포넌트와 매핑된다.
    - 히스토리 모드에서 router-link는 클릭 이벤트를 차단하여 a 태그와 달리 브라우저가 페이지를 다시 로드하지 않도로고한다.
    - 목표 경로를 to 속성으로 지정한다.

- router-view
    - 주어진 URL에 대해 일치하는 컴포넌트를 렌더링 하는 컴포넌트
    - 실제 component가 DOM에 부착되어 보이는 자리를 의미한다.
    - router-link를 클릭하면 routes에 매핑된 컴포넌트를 렌더링한다.
    - Django에서의 block tag 와 유사하다.
        - app.vue는 base.html
        - router-view는 block태그로 감싸진 부분
    
    ```jsx
    djanao에서의 표현
    
    urlpatterns = [
    	path('', views.index, name='index'),
    ]
    
    router에서의 표현
    src/router/index.js
    
    const routes = [
    	{
    		path: '/',
    		name: 'index', 
    		component: IndexView
    	},
    ]
    ```
    
    - 프로그래밍 방식 네비게이션
        - vue 인스턴스 내부에서 라우터 인스턴스에 $router로 접근 할 수 있다.
        - 다른 URL 이동하려면
            
            ```jsx
            this.$router.push 를 사용한다.
            
            export default {
            	name: 'AboutView',
            	methods : {
            		toIndex() {
            			this.$router.push({ name: 'index' })
            		}
            	}
            }
            ```
            
        - history stack에 이동한 url을 넣는 push 방식
        - 
- Dynamic Route Matching

```jsx
$route.params로 변수에 접근 가능하다.

<h1>Hello, {{ $route.params.userName }}</h1>

data에 넣어서 사용하는 것을 더 권장하기는 한다.

<template>
	<div>
		<h1>Hello, {{ userName }}</h1>
	<div>
<template>

<script>
	name: 'HellowView',
	data() {
		return {
			userName: this.$route.params.userName
		}
	}
}
</script>

```