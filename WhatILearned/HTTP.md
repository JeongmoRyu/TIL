# HTTP

- Hyper Text Transfer Protocol
- HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
- WWW(web)에서 이루어지는 모든 데이터 교환의 기초가 된다.
- 클라이언트 ↔ 서버 프로토콜이라고도 불린다.

## HTTP

- 요청(requests)
    - 클라이언트(브라우저)에 의해 전송되는 메세지
- 응답(response)
    - 서버에서 응답으로 전송되는 메세지
- 특징
    - 비연결지향(connectionsless)
        - 서버에서 요청에 대한 응답을 보낸 후 연결을 끊는다.
    - 무상태(stateliss)
        - 연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나며 상태 정보가 유지되지 않는다.
        - 독립적인 상태
- 쿠키와 세션 : 서버와 클라이언트 간 지속적인 상태 유지를 위해 필요

## 쿠키(Cookie)

- study에서 공부하는 쿠키와 세션

[CS-Study/쿠키&세션.md at main · CS-SSAFY-4Class/CS-Study (github.com)](https://github.com/CS-SSAFY-4Class/CS-Study/blob/main/Web/%EC%BF%A0%ED%82%A4(Cookie)%26%EC%84%B8%EC%85%98(Session)/%EC%BF%A0%ED%82%A4%26%EC%84%B8%EC%85%98.md)

[https://github.com/CS-SSAFY-4Class/CS-Study/blob/main/Web/쿠키(Cookie)%26세션(Session)/쿠키%26세션.md](https://github.com/CS-SSAFY-4Class/CS-Study/blob/main/Web/%EC%BF%A0%ED%82%A4(Cookie)%26%EC%84%B8%EC%85%98(Session)/%EC%BF%A0%ED%82%A4%26%EC%84%B8%EC%85%98.md)

- 상태가 있는 세션을 만들도록 해준다.
- 사용 목적
    1. 세션 관리(Session management)
        1. 로그인, 아이디, 공지 안보기, 팝업
    2. 개인화(Personaliztion)
        1. 사용자 선호, 테마
    3. 트래킹(Tracking)
        1. 사용자 행동을 기록 및 분석
- 쿠키 수명
    - Session cookie
        - 현재 세션이 종료되면 삭제된다.
        - 브라우저 종료와 함께 세션이 삭제된다.
    - Persistent cookie
        - expires 속성에 지정된 날짜 혹은 Max-Age 속성에 지정된 기간이 지나면 삭제된다.

## 세션

- 사이트와 특정 브라우저 사이의 state(상태)를 유지시키는 것
- Session in Django
    - Django는 database-backed sessions 저장 방식을 기본 값으로 사용
        - session 정보는 Django DB의 django_session 테이블에 저장한다.
        - Django는 특정 session id를 포함하는 쿠키를 사용해서 각각의 브라우저와 사이트가 연결된 session을 알아낸다.

## Authentication in Web requests

- Login
    - Login : session을 create하는 과정

- accounts/urls.py

```
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('login/', views.login, name='login'),
]
```

- accounts/views.py

```python
from django.shortcuts import render
from django.contrib.auth.forms import AuthenticationForm

# Create your views here.
def login(request):
    if request.method == 'POST':
        pass
        # 로그인 처리를 해준다.
    else:
        # 비어있는 로그인 페이지를 제공
        form = AuthenticationForm()
    context = {'form': form}
    return render(request, 'accounts/login.html', context)
```

- accounts/templates/accounts/login.html

```
{% extends 'base.html' %}

{% block content %}
  <h1>LOGIN</h1>

  <form action=" {% url 'accounts:login' %} " method="POST">
    {% csrf_token %}
    {{form.as_p}}
    <input type="submit" value='로그인'>

  </form>

{% endblock content %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aa12b163-f7e4-4369-8c33-e5227c2c231d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021530Z&X-Amz-Expires=86400&X-Amz-Signature=bd48324bb54fbd7660344d2ab8ab1404c6bc32aa2304e7538006fc1b5eb5667f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b5132b4a-eb48-4829-94c7-3e3b1bf6c921/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021538Z&X-Amz-Expires=86400&X-Amz-Signature=12a4178d3ab977b202951471683e98ade6155d931ffe41870af3361f53fcd518&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/36b3cad3-2a69-4f07-a983-c9528cbf57a0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021546Z&X-Amz-Expires=86400&X-Amz-Signature=192c932c27fe37d0df1c590ff1cd559fefaa193a2eccfff5355598ee222f22c8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

로그인은 성공 but, 로그인 된 창이 아직 구현되지 않았다.

- 위의 단계를 쉽게 하는 방법도 이미 구현되어 있다.

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
        # 로그인 처리를 해준다.
    else:
        # 비어있는 로그인 페이지를 제공
        form = AuthenticationForm()
    context = {'form': form}
    return render(request, 'accounts/login.html', context)
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b5132b4a-eb48-4829-94c7-3e3b1bf6c921/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021556Z&X-Amz-Expires=86400&X-Amz-Signature=650845aaaaa2879a13531c70b7d946a7bc2629597670b61bff22c48d0741cd74&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9fc5ebab-b8d1-4d2d-b0a3-1bcf0cdae4ca/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021605Z&X-Amz-Expires=86400&X-Amz-Signature=b0b3da766abc8c30f47cabb50312348e919bbc37ce693ff3fd0971e121dc508d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

templates/base.html

```jsx
<body>
	<h3>안녕하세요, {{user}}님! </h3>
</body>
```

이제 로그인처리가 되어서 원하는 목록으로 돌아가게 된다.

확인해보면

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4e81e299-f6bc-4f04-a20f-8841d063b873/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021616Z&X-Amz-Expires=86400&X-Amz-Signature=18d716c3c34ed4c3a504f429282be32e3c21d294812a9922eaf83b5e9dae33a7&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b52da00-e58a-4823-8f6b-3047fddeb7c3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021624Z&X-Amz-Expires=86400&X-Amz-Signature=bd2d1c823bdca876095524dd7f968a4c740fa8c2ad33e9d92d8f3a63f289ea77&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## Logout

- logout(request)
    - session data를 DB에서 삭제
    - 클라이언트 쿠키에서도 sessionid 삭제

- articles/urls.py

```
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout')
]
```

- articles/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
        # 로그인 처리를 해준다.
    else:
        # 비어있는 로그인 페이지를 제공
        form = AuthenticationForm()
    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```

- templates/base.html

```jsx
<a href=" {% url 'accounts:logout' %} ">로그아웃</a> 추가하기
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b46518e2-f229-40d7-ae0f-f9bb3118bf42/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021633Z&X-Amz-Expires=86400&X-Amz-Signature=f9f11ac2800cfcccf72dcd11bc86f70c711efa5dc48b053f259adb0d9cd300c6&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1300be2d-8155-419e-a7ff-707d91e5974e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230327%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230327T021642Z&X-Amz-Expires=86400&X-Amz-Signature=e4b3a6eae291b660d3edf842a423af59991fb9c6698895bea4ec54a2fa09accb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)