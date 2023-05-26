# Vue DRF

- skeleton code with back-server, front-server

## CORS : Cross-Origin Resource Sharing

- 브라우저가 요청을 보내고 서버의 응답이 브라우저에 도착
    - server의 log는 200정상을 반환하지만 브라우저 막는경우
- 보안상의 이유로 브라우저는 동일 출처 정책(SOP)에 의해 다른 출처의 리소스와 상호작용 하는 것을 제한한다.

### SOP : Same-Origin Policy

- 동일 출처 정책
- 불러운 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안 방식
- 잠재적으로 해로울 수 있는 문서를 분리함으로 공격받을 수 있는 경로를 줄인다.

- Origin : 출처
    - URL의 Protocol, Host, Port를 모두 포함하여 출처라고 부른다.
    - scheme/protocol,  host,  port 모두 동일하여야 same origin으로 인정한다. (ex : http://localhost:8000/ 여기까지 )

- CORS 교차 출처 리소스 공유
    - 추가 HTTP Header를 사용하여 특정 출처에서 실행 중인 웹 어플리케이션이 다른 출처의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
    - 리소스가 자신의 출처와 다를 때 교차 출처 HTTP 요청을 실행
        - CORS policy 교차 출처 리소스 공유 정책
            - 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS header를 포함한 응답을 반환해야한다.

## Set CORS

- CORS 표준에 추가된 HTTP Response Header를 통해 이를 통제 가능하다.
- HTTP Response Header
    - **Access-Control_Allow_Origin**
        - 단일 출처를 지정하여 브라우저가 해당 출처가 리소스에 접근하도록 허용한다.
    - Access-Control_Allow_Credentials
    - Access-Control_Allow_Headers
    - Access-Control_Allow_Methods

```jsx
$ python install django-cors-headers

$ pip freeze > requirements.txt

installed_apps에 'corsheaders',
middleware에 'corsheaders.middleware.CorsMiddleware',
	commonmiddleware보다는 위에 있어야한다.

```

```jsx
8080 서버를 허용하는 방법
CORS_ALLOWED_ORIGINS = [
    'http://localhost:8080',
]

이렇게 전부 다 허용해도된다.
CORS_ALLOWED_ALL_ORIGINS = True
```