# Django_Form&Data



- HTML form element를 통해 사용자와 애플리케이션 간의 상호작용을 이해한다.
- 웹은 클라이언트-서버 아키텍처를 사용한다.

## Sending form data(client)

- HTML <form> element
    - 웹에서 사용자 정보를 입력하는 여러 방식(text, button, submit 등)을 제공하고, 사용자로부터 할당된 데이터를 서버로 전송하는 역할을 담당한다.
- HTML form’s attributes
    - action
        - 입력 데이터가 전송될 URL을 지정
        - 어디로 보낼 것인지 지정하는 것이며 이 값은 유효한 URL이어야 한다.
        - 속성을 지정하지 않으면 데이터는 현재 form이 있는 페이지를 보낸다.
        
    - method
        - 데이터를 어떻게 보낼 것인지
        - HTTP request methods를 지정
        - GET POST 방식을 통해 전송할 수 있다.

- HTML <input> element
    - 사용자로부터 데이터를 입력 받기 위해 사용
    - type 속성에 따라 동작 방식이 달라진다.
        - input 요소의 동작 방식은 type 특성에 따라 현격히 달라진다. MDN 문서에서 참고 사용
        - 지정하지 않는다면 기본값은 text
    - 핵심 속성
        - name
            - form을 통해 데이터를 제출했을 때 name 속성에 설정된 값을 전송하고 서버는 name 속성에 설정된 값을 통해 사용자가 입력한 데이터 값에 접근할 수 있다.
            - 서버에 전달하는 파라미터로 mapping하는 것

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="#" method="#">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>

{% endblock content %}
```

- HTTP request methods
    - HTTP
        - HTML 문서와 같은 리소스(데이터, 자원)들을 가져올 수 있도록 해주는 프로토콜(규칙, 규약)
        - 웹에서 이루어지는 모든 데이터 교환의 기초
        - HTTP는 주어진 리소스가 수행 할 작업을 나타내는 request methods를 정의
    - HTTP Method
        - GET
            - 서버로부터 정보를 조회하는 데 사용한다.
                - 리소스를 요청하기 위해 사용
            - 데이터를 가져올 때 사용
            - Query string parameters를 통해 전송한다.
        
        ```html
        {% extends 'base.html' %}
        
        {% block content %}
          <h1>Throw</h1>
          <form action="#" method="GET">
            <label for="message">Throw</label>
            <input type="text" id="message" name="message">
            <input type="submit">
          </form>
        
        {% endblock content %}
        ```
        
        - 
            - Query string parameters
                - 사용자가 입력 데이터를 전달하는 방법 중 하나이고 url 주소에 데이터를 파라미터를 통해 넘기는 방법이다.
                - &로 연결된 key, value 로 구성되며 ?로 구분된다.
                
                ```html
                ex) http://abcdabcd/abcd ?key=value&key=value
                
                ex) http://127.0.0.1:8000/Catch/?message=message
                밑에 연습에서 message를 쳤을 경우 나오는 URL
                ```
                
        
        - POST
        - PUT
        - DELETE
        

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
]
```

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
		path('catch/', views.catch, name="catch"),
]
```

```python
from django.shortcuts import render

# Create your views here.
# /catch/로 요청을 보내는 form을 포함한 html
def throw(request):
    return render(request, 'articles/throw.html')

def catch(request):
    request.GET.get("message")
    print(request.GET.get("message"))
    # 터미널에서 입력한 메세지를 확인할 수 있다.
    return render(request, "articles/catch.html")
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>
    {% block title %}
    {% endblock title %}
    
  </title>
</head>
<body>
  <a href="http://google.com">Google</a>
  <a href="http://naver.com">NAVER</a>
  <h1>
    {% block body %}
    {% endblock body %}
  </h1>
</body>
</html>
```

```html
{% extends 'base.html' %}

{% block title %}Throw{% endblock title %}

{% block body %}
  <h1>Throw</h1>
  <form action="{% url 'articles:catch' %}" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>

{% endblock body %}{% extends 'base.html' %}

{% block body %}
<h1>Catch</h1>
<p>Received Data {{ message}} </p>
<a href="{% url 'articles:throw' %}">Go back</a>
{% endblock body %}
```

```html
{% extends 'base.html' %}

{% block title %}Throw{% endblock title %}

{% block body %}
  <h1>Throw</h1>
  <form action="{% url 'articles:catch' %}" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>

{% endblock body %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/36ff8ba0-ae21-4b49-befe-5d455c9b9969/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230320%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230320T011056Z&X-Amz-Expires=86400&X-Amz-Signature=a16d83aa259807c26dd7714ad9f812ee600b7262faa94e21832cd3e3558052ca&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5fb78e45-5dea-47c1-a36d-1af10748bbb9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230320%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230320T011104Z&X-Amz-Expires=86400&X-Amz-Signature=1f168b4279dd06d566cd94d075f1381bf2400d559995c0f4edd82959ff2a1f08&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## Retrieving the data(server)

- 데이터 가져오기(검색하기)
- 서버는 클라이언트로 받은 key-value 쌍의 목록과 같은 데이터를 받는다.
- throw가 보낸 데이터를 catch에서 가져오기
- catch 작성하기
    
    ```html
    {% extends 'base.html' %}
    
    {% block content %}
      <h1>Throw</h1>
      <form action="/catch/" method="GET">
        <label for="message">Throw</label>
        <input type="text" id="message" name="message">
        <input type="submit">
      </form>
    
    {% endblock content %}
    ```
    
- 데이터 가져오기
    - catch 페이지가 잘 응답되어 출력됨을 확인한다.
    - 요청과 응답 객체 흐름
        1. 페이지가 요청되면 Django는 요청에 대한 메타데이터를 포함하는 HttpRequest object를 생성
        2. 해당하는 적절한 view함수를 로드하고 HttpRequest를 첫 번째 인자로 전달한다.
        3. view함수는 HttpResponse object를 반환한다.