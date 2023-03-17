# Django Design Pattern



- 응용 소프트웨어를 개발할 때 자주 사용되는 구조가 있기에 일반화하여 하나의 공법, 패턴으로 만들어 둔 것

### 소프트웨어 디자인 패턴의 목적

- 특정 문맥에서 공통적으로 발생하는 문제에 대한 재 사용 가능한 해결책을 제시
- 프로그래머가 어플리케이션이나 시스템을 디자인할 때 발생하는 공통된 문제들을 해결하는데 형식화된 패턴

→ 커뮤니케이션의 효율성을 높이는 기법

## Django Design Pattern

- Django에서 적용된 디자인 패턴은 **MTV** 패턴이다.
    - MTV 패턴은 MVC 디자인 패턴을 기반으로 만들었다.
        - MVC : Model - View - Controller
            - 업무의 분리와 향상된 관리를 제공
            - 개발 효율성 및 유지보수 GOOD!
            - 다수 멤버로 개발하기 용이
- MTV : Model - Template - View
    - Model
        - 데이터와 관련된 로직을 관리
        - 응용프로그램의데이터 구조를 정의하고 데이터베이스의 기록을 관리
    - Template
        - 레이아웃과 화면을 처리
        - 화면상의 사용자 인터페이스 구조와 레이아웃을 정의
    - View
        - Model 과 Template이 관련한 로직을 처리해서 응답을 반환한다.
        - 클라이언트의 요청에 대해 처리를 분기하는 역할
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cec9d471-09b3-47df-a9d8-e674df215c36/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230316%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230316T235858Z&X-Amz-Expires=86400&X-Amz-Signature=d412de72341e035e401f28bcb8f44411dbbc7e2dda0c0ca831e064a3c1fba03c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    

## Django Template

- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직
- Django Template을 이용한 HTML 정적 부분과 동적 컨텐츠 삽입

### Django Template Language (DTL)

- Django template에서 사용하는 built-in template system
- 조건, 반복, 변수 치환, 필터 등의 기능을 제공
    - but, python 처럼 바로 실행되는 것은 아니니 주의!!!
- DTL Syntax
    - Variable
        - {{varialbe}}
        - dot(.)을 사용하여 변수 속성에 접근할 수 있음
        - render()의 세번째 인자로 {’key’:value}와 같이 딕셔너리 형태로 넘겨주며 key에 해당하는 문자열이 template에서 사용 가능한 변수명이 된다.
        
        ```html
        from django.shortcuts import render
        
        # Create your views here.
        def index(request):
            
            info = {
                'name': 'JM',
                'age': 30,
            }
        
            return render(request, 'my_app/index.html', {'info' : info})
        ```
        
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
          <h1>HOLA~~~~!!! {{ info.name }}</h1>
          <h2>나이는 : {{ info.age }}</h2>
          
        </body>
        </html>
        ```
        
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fb5170ab-731d-4ef3-92b6-fe8485ecad5e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230316%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230316T235914Z&X-Amz-Expires=86400&X-Amz-Signature=4ee92b43e4300071d30b58495ee967898b441e29422c2873e726db9d26fc3fae&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - Filters
        - {{variable| filter}}
            - 60개의 built-in template filters를 제공
            - 인자로 받기도, chained도 가능하다 {{name|age:30}}
    - Tags
        - {% tag %}
        - 일부 tag는 시작과 종료 태그가 필요하다
            - {% if %}{% endif %}
            - 24개의 built-in template filters를 제공
        
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
          <h1>HOLA~~~~!!! {{ info.name }}</h1>
          {% if info.age == 30 %}
            <p>HI brother</p>
          {% endif %}
        
          <h2>AGE : {{ info.age }}</h2>
          
        </body>
        </html>
        ```
        
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/06755690-d161-4f61-8673-a5afed86fd92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230316%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230316T235927Z&X-Amz-Expires=86400&X-Amz-Signature=7a7c3253c27e93a354af320c3f0fe402d2ee55c5867f3b5454a057a7d05fba3e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    </br>
    
    - Comments
        - {# #}
        - 주석을 표현하기 위해 사용
        - 유효하지 않은 코드를 포함할 수 있다.
        - 줄 바꿈 허용 X
            - 여러 줄 주석은 {% comment %} {% endcomment %} 사이에 입력한다.
            

practice

```python
from django.shortcuts import render

# Create your views here.
def index(request):
    
    info = {
        'name': 'JM',
        'age': 30,
    }

    return render(request, 'my_app/index.html', {'info' : info})

def test(request):
    name = "JM"
    menu = "chicken"
    payment = "credit_card"
    charge = 25000

    order = ["chicken", "pizza", "lamb", "beef", "pork"]

    context = {
        "name": name,
        "menu": menu,
        "payment": payment,
        "charge": charge,
        "orders": order,
    }

    return render(request, "my_app/test.html", context)
```

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
  <h1>bill</h1>
  <p>name: {{name}}</p>
  <p>menu: {{menu|default:"beer"}}</p>
  <p>how to pay: {{payment}}</p>
  <p>charge: {{charge}}</p>

  <h2>I'd like to order</h2>
  {% for order in orders %}
      <h3>{{order}}</h3>
  {% empty %}
      <h4>Nothing</h4>
  {% endfor %}
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e9576ea5-d157-4b51-a82e-ec9e323ecb13/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000025Z&X-Amz-Expires=86400&X-Amz-Signature=950390109d497ecd89a283885574cbddf4c50c63ecdd12815e5b6280218805f1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### Template Inheritance

- 템플릿 상속은 기본적으로 코드의 재사용성에 초점을 맞춤
- 템플릿 상속을 사용하면 사이트의 모든 공통 요소를 포함하고 하위 템플릿이 재정의 할 수 있는 블록을 정의하는 기본 템플릿을 만들 수 있다.
- 템플릿 상속에 관련된 태그
    - {% extend ‘’ %}
        - 2개 이상 사용할 수 없고 최상단에 작성되어야한다.
        - {% block content %} {% endblock content %}

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b9310a94-8bd2-4015-a7d4-a7b1491b130a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000050Z&X-Amz-Expires=86400&X-Amz-Signature=0c49897d48c0ee8a2e71dcaf84f7323c3499d929ee0a532b183b80184f869b2a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d4cadac9-b043-40de-8147-ffcba1fa6c7f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000059Z&X-Amz-Expires=86400&X-Amz-Signature=4553727d3be8f50cf4daac9f108e1d03a4c1925e0d2c59fdeea86cdee7e5ec47&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

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
  <h1>
    <a href="http://google.com">Google</a>
    <a href="http://naver.com">NAVER</a>

  </h1>
  {% block body %}
  {% endblock body%}

</body>
</html>
```

```html
{% extends './baseline.html' %}

{% block title %}
  TEST
{% endblock title %}

{% block body %}

<h1>bill</h1>
  <p>name: {{name}}</p>
  <p>menu: {{menu|default:"beer"}}</p>
  <p>how to pay: {{payment}}</p>
  <p>charge: {{charge}}</p>

  <h2>I'd like to order</h2>
  {% for order in orders %}
      <h3>{{order}}</h3>
  {% empty %}
      <h4>Nothing</h4>
  {% endfor %}

{% endblock body %}
```

```python
from django.shortcuts import render

def test_baseline(request):
    name = "JM"
    menu = "chicken"
    payment = "credit_card"
    charge = 25000

    order = ["chicken", "pizza", "lamb", "beef", "pork"]

    context = {
        "name": name,
        "menu": menu,
        "payment": payment,
        "charge": charge,
        "orders": order,
    }

    return render(request, "my_app/test_baseline.html", context)
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5026b3b3-e5fc-4eb4-8c98-333021fc5601/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000114Z&X-Amz-Expires=86400&X-Amz-Signature=61278bcb61d0df43531185c86263676a8bd5014dd06260939771b76264588c4b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### Trailing URL Slashes

- Django는 URL 끝에 /가 없다면 자동으로 붙여주는 것이 기본설정이지만 모든 프레임워크가 이렇게 동작하는 것은 아니다.
- foot/bar 과  foot/bar/가 같은 것이 아니다.  그래서 URL을 정규화하여야 한다.

### Variable routing의 필요성

- URL 주소를 변수로 사용하는 것을 의미한다.
- 변수 값에 따라 하나의 path()에 여러 페이지를 연결 시킬 수 있다.
    
    
    1. str
        1. ‘/’을 제외하고 비어있지 않은 모든 문자열 기본값
    2. int
        1. 0 또는 양의 정수
    3. slug
    4. uuid
    5. path

### APP URL mapping

- 앱이 많아졌을 때 urls.py를 각 app에 mapping하는 방법을 이해한다.
- 서비스를 개발하다보면 url와 view가 매우 많아지게 되어  urls.py에서 관리하게 되면
    - 가독성 down
    - 유지 보수 비용 up
    
    → 해결방안
    
    - 각각의 app 폴더 안에 urls.py를 작성하면 된다.
    - include 되는 앱의 url.py에 urlpatterns가 작성되어 있지 않다면 에러가 발생할 수 있기에 빈 리스트라도 작성되어야 한다.
- include()
    - 다른 URLconf(app/urls.py)들을 참조할 수 있도록 돕는 함수
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6c507d05-b2b5-49c4-ada5-0e6b438b791f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000126Z&X-Amz-Expires=86400&X-Amz-Signature=f3b180c18dc53a7ede8d16198e6444c07cdd89f374b6ab5f04e8534423e919f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    

### Naming URL patterns

- 이름을 바꿔야 할 경우 하나하나 다 바꿀 수 없기 때문에 name 인자를 정의해서 사용하면 된다.
- 이러한 방법으로 특정 경로들의 의존하는 것을 막을 수 있다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f665f33-f3c1-4d86-aa54-6fcb364b942d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000201Z&X-Amz-Expires=86400&X-Amz-Signature=2b254ff9304c7251c60419b09ed08dfdab93d2b1d13cf628198a7039a1effea3&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

그 후에 url을 사용하여 name된 이름을 넣어준다.

```html
{% url '' %}
```

- practice

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
  <h1>
    <a href="http://google.com">Google</a>
    <a href="http://naver.com">NAVER</a>
    <a href="/my_app/test/">Test</a>
    

  </br>

    <a href="/my_app/index/">index</a>
    <a href="/polls/index/">index</a>
    <a href="{% url 'my_app:index' %}">A_index</a>
    <a href="{% url 'polls:index' %} ">P_index</a>

  </h1>
  {% block body %}
  {% endblock body%}

</body>
</html>
```

```python
from django.urls import path
from . import views

app_name = "polls"
urlpatterns = [
    path('index/', views.index, name="index")
]
```

```python
from django.urls import path
from . import views

app_name = "my_app"
urlpatterns = [
    path('home/', views.index),
    path('test/', views.test),
    path('test_baseline/', views.test_baseline),
    path('index/', views.index, name="index")
]
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/39f57dc0-4168-411d-bc33-540d1cd8fc2b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230317%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230317T000211Z&X-Amz-Expires=86400&X-Amz-Signature=19b8cbe807955de152e515dd2227fe8044311947be7793b7c8d76f15fb317a39&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)