# vue navigation guard

## Navigation Guard

- Vue router를 통해 특정 URL에 접근할 때 다른 url redirect하거나 해당 URL로의 접근을 막는 방법
- 종류
    - 전역 가드 : 애플리케이션 전역에서 동작
    - 라우터 가드 : 특정 URL에서만 동작
    - 컴포넌트 가드 : 라우터 컴포넌트 안에서 정의

## Global Before Guard : 전역 가드

- 다른 url 주소로 이동할 때 항상 실행
- router/index.js에 router.beforeEach( )를 사용하여 설정한다.
- 콜백 함수의 값으로 다음과 같이 3개의 인자를 받는다.
    - to : 이동할 URL 정보가 담긴 Route 객체
    - from : 현재 URL 정보가 담긴 Route 객체
    - next : 지정한 URL로 이동하기 위해 호출하는 함수
        - 콜백함수에서 한번만 호출되어야한다.
        - 기본적으로 to에 해당하는 URL로 이동한다.
- URL이 변경되어 화면이 전환되기 전 router.beforeEach( )가 호출된다.
    - 화면이 전환되지 않고 대기 상태가 된다.
- 변경된 URL로 라우팅하기 위해서는 next( )를 호출해줘야 한다.
    - next가 호출되기 전까지 화면이 전환되지 않는다.

```jsx
router.beforeEach((to, from, next) => {
  console.log('to', to)
  console.log('from', from)
  console.log('next', next)
  next()
})
```

## Router Guard : 라우터 가드

- 전체 route가 아닌 특정 route에 대해서만 가드를 설정하고 싶을 때 사용한다.
    - beforeEnter ( )
        - 
        
        ### Router Guard : 라우터 가드
        
        - 전체 route가 아닌 특정 route에 대해서만 가드를 설정하고 싶을 때 사용한다.
            - beforeEnter ( )
                - route가 진행될 때 실행한다.
                - 등록한 위치에서 실행
                    - 다른 경우에서 탐색할 때에만 실핸된다.
                    - 콜백함수는 to, from , net로 받았다.

```jsx
{
    path: '/login',
    name: 'login',
    component: LoginView,
    beforeEnter(to, from, next) {
      if (isLoggedIn === true) {
        console.log('logged In')
        next({ name: 'home' })
      } else {
        next()
				// 로그인이 안 되어 있다면, 로그인 페이지로 이동
      }
    }
  },
```

id + 1

## Component Guard : 컴포넌트 가드

- 특정 컴포넌트 내에서 가드를 지정하고 싶을 때 사용한다.
- beforeRouteUpdate( )
    - 해당 컴포넌트를 렌더링하는 경로가 변경될 때 실행한다.
- params 변화를 감지하는 것을 beforRuoteUpdate( )를 사용해서 재할당 및 처리를 해준다.