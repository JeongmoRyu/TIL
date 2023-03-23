# Django CRUD

## Create

- Create 로직을 구현하기 위해서는 몇 개의 view 함수가 필요할까?
    - 사용자의 입력을 받을 페이지를 렌더링 하는 함수 1개
        - new view function
    - 사용자가 입력한 데이터를 전송 받아 DB에 저장하는 함수 1개
        - create view function
        
        ```python
        from django.urls import path
        from . import views
        
        app_name = 'articles'
        urlpatterns = [
            path('', views.index, name='index'),
            path('<int:pk>/', views.detail, name='detail'),
            path('new/', views.new, name='new'),
        		path('create/', views.create, name='create'),
        ]
        ```
        
        ```python
        from django.shortcuts import render
        from .models import Article
        
        # Create your views here.
        def index(request):
            articles = Article.objects.all()
            context = {'articles': articles}
            return render(request, 'articles/index.html', context)
        
        def detail(request, pk):
            article = Article.objects.get(pk=pk)
            context = {'article': article}
            return render(request, 'articles/detail.html', context)
        
        def new(request):
            return render(request, 'articles/new.html')
        
        def create(request):
            title = request.GET.get('title')
            content = request.GET.get('content')
        
            article = Article(title=title, content=content)
            article.save()
        
            return redirect('articles:detail', article.pk)
        ```
        
        ```html
        {% extends 'base.html' %}
        
        {% block content %}
          <h1>NEW</h1>
          <hr>
          <form action=" {% url 'articles:create' %} " method="GET">
            <label for="title">Title: </label>
            <input type="text" name="title">
            </br>
        
            <label for="content">Content: </label>
            <textarea name="content"></textarea>
            </br>
            <input type="submit">
          </form>
          <hr>
          <a href="{% url 'articles:index' %}">[Back]</a>
        {% endblock content %}
        ```
        

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d763da91-561b-417c-b66d-a884ce8994f1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T002603Z&X-Amz-Expires=86400&X-Amz-Signature=6ac3a522ddfbf76bdeef94169dceadf96c388b3c69a6c31288ac768af835f043&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## HTTP Method

- HTTP
    - HTTP
        - 네트워크 상에서 데이터를 주고 받기 위한 약속
    - HTTP Method
        - 데이터(리소스)에 어떤 요청(행동)을 원하는지를 나타낸 것

- GET & POST
    - 현재 코드 재검토
        - GET은 쿼리 스트링 파라미터로 데이터를 보내기 때문에 url을 통해 데이터를 보낸다.
    
- HTTP request method
    - GET
        - 특정 리소스를 가져오도록 요청할 때 사용
        - 반드시 데이터를 가져올 때만 사용해야 함
        - DB에 변화를 주지 않음
        - CRUD에서 R 역할을 담당
    - POST
        - 서버로 데이터를 전송할 때 사용
        - 서버에 변경사항을 만든다.
        - 리소스를 생성/변경하기 위해 데이터를 HTTP body에 담아 전송한다.
        - GET의 쿼리 스트링 파라미터와 다르게 URL로 데이터를 보내지 않는다.
        - CRUD에서 C/U/D 역할을 담당한다.

- 403 Forbidden
    - 서버에 요청이 전달되었지만 권한으로 인해서 거절되었다.
    - 서버에 요청은 도달했으나 서버가 접근을 거부할 때 반환된다.
- CSRF
    - Cross-Site-Request-Forgery
    - 사이트 간 요청 위조
- CSRF 공격 방어
    - Security Token 사용 방식
    - 사용자의 데이터에 임의의 난수 값을 부여해 요청마다 난수 값을 포함시켜 전송 시키도록 한다.
    - 서버에서 요청을 받을 때마다 token값이 유효한지 검증한다.
    - Django는 DTL에서 crsf_token 템플릿 태그를 제공하기도 한다.

## DELETE

## UPDATE

- 수정은 CREATE 로직과 마찬가지로 2개의 view함수가 필요하다
- 사용자 입력을 받을 페이지를 렌더링 하는 함수 1개
    - edit view function
- 사용자가 입력한 데이터를 전송 받아 DB에 저장하는 함수 1개
    - update view function

## Handling HTTP requests

```python
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:pk>/', views.detail, name='detail'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/delete/', views.delete, name="delete")
]
```

```python
from django.shortcuts import render, redirect
from .models import Article

# Create your views here.
def index(request):
    articles = Article.objects.all()
    context = {'articles': articles}
    return render(request, 'articles/index.html', context)

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {'article': article}
    return render(request, 'articles/detail.html', context)

def new(request):
    return render(request, 'articles/new.html')

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')

    article = Article()
    article.title = title
    article.content = content
    article.save()
    return redirect('articles:detail', article.pk)

def delete(request, pk):
    if request.method == "POST":
        article = Article.objects.get(pk=pk)
        article.delete()
    return redirect("articles:index")
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>DETAIL</h1>
  <hr>

  <p>글 제목 : {{article.title}}</p>
  <p>글 내용 : {{article.content}}</p>
  <p>글 생성시각: {{article.creadted_at}}</p>
  <p>글 수정시각: {{article.updated_at}}</p>
  <form action=" {% url 'articles:delete' article.pk %} " method="post">
    {% csrf_token %}
    <input type="submit" value="delete">
  </form>
  <a href="{% url 'articles:index' %}">목록보기</a>
{% endblock content %}
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>NEW</h1>
  <hr>
  <form action=" {% url 'articles:create' %} " method="POST">
    {% csrf_token %}
    <label for="title">Title: </label>
    <input id="title" type="text" name="title">
    </br>

    <label for="content">Content: </label>
    <textarea name="content" id="content"></textarea>
    </br>
    <input type="submit" value="제출">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[Back]</a>
{% endblock content %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e2ad9e2d-38e8-4dc6-be07-b0a0bb8d903d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T002622Z&X-Amz-Expires=86400&X-Amz-Signature=4e097a2905c3dde24c6d65d7f6e747fe400d31195b7d5e527963bb783689bb66&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/43f76a8f-f839-4402-8060-16b123415824/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T002631Z&X-Amz-Expires=86400&X-Amz-Signature=a9f951e29d8ba99169bf2401d23a4ad0ca46956875ad5d3a722a6c25b64d7122&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)