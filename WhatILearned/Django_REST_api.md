# Django REST api

## REST API

### API

- Application Programming INterface
- 애플리케이션과 프로그래밍으로 소통하는 방법
    - 개발자가 복잡한 기능을 쉽게 만들 수 있도록 프로그래밍 언어로 제공되는 구성
- Web API
    - 웹 서버 또는 웹 브라우저를 위한 API
    - Third Party Open API 서비스 목록
        - Youtube API
        - Naver Papago API
        - Kakao Map API
    - HTML, XML, JSON 등 다양한 타입의 데이터를 응답한다.
    

### REST

- Reprosentational State Transfer
- API server를 개발하기 위한 일종의 소프트웨어 설계 방법론
    - 로이 필딩의 박사학위 논문에서 처음으로 소개된 후 네트워킹 문화에 널리퍼졌다.
- 소프트웨어 아키텍쳐 디자인 제약 모음
- REST 원리를 따르는 시스템을 RESTful 하다고 부른다.
- REST의 기본 아이디어는 리소스
    - 리소스를 정의하고 리소스에 대한 주소를 지정하는 전반적인 방법을 서술

- JSON
    - JSON : JavaScript의 표기법을 따른 단순 문자열
    - 파이썬 dictionary, 자바스크립트의 object처럼 C 계열의 언어가 갖고 있는 자료 구조로 쉽게 변환할 수 있는 key-value형태의 구조를 가지고 있다.
    - 사람이 읽고 쓰기 쉽고 기계가 해석하고 분석하여 만들어 내기 쉽다.
    - API에서 가장 많이 사용하는 데이터 타입
- 정리
    - REST : 자원을 정의하고 자원에 대한 주소를 지정하는 방법의 모음
        - 자원을 식별 : URI
        - 자원에 대한 행위 : HTTP Methods
        - 자원을 표현 : JSON

urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('html/', views.article_html),
    path('json-1/', views.article_json_1),
    path('json-2/', views.article_json_2),
    path('json-3/', views.article_json_3),
]
```

views.py

```python
from django.shortcuts import render
from django.http.response import JsonResponse, HttpResponse
from .models import Article

# Create your views here.
def article_html(request):
    articles = Article.objects.all()
    context = {'articles': articles}
    return render(request, 'articles/article.html', context)

def article_json_1(request):
    articles = Article.objects.all()
    articles_json = []
    for article in articles:
        articles_json.append(
            {
            'id': article.pk,
            'title': article.title,
            'content': article.content, 
            'created_at': article.created_at,
            'updated_at': article.updated_at,
            }
        )
    return JsonResponse(articles_json, safe=False)
```

보기 어지럽게 적혀있는걸 보기 편하게 바꾸어준다.

크롬 익스텐션, json viewer

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04a3fec0-b08e-4f6c-be44-468d11c467e2/Untitled.png)

views.py

```python
def article_json_2(request):
    articles = Article.objects.all()
    data = serializers.serialize('json', articles)
    return HttpResponse(data, content_type='application/json')
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8b88db89-41d7-46e5-b3cf-a96c1c13eb65/Untitled.png)

### Django_REST Framework

settings.py

installed_apps에 'rest_framework' 추가

serializers.py

```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    
    class Meta:
        model = Article
        fields = '__all__'
```

views.py

```python
from .serializers import ArticleSerializer

def article_json_3(request):
    articles = Article.objects.all()
    serializer = ArticleSerializer(articles, many=True)
    return Response(serializer.data)
```

POSTMAN을 이용해보기

urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    # path('html/', views.article_html),
    # path('json-1/', views.article_json_1),
    # path('json-2/', views.article_json_2),
    # path('json-3/', views.article_json_3),
    path('articles/', views.article_list),
		path('articles/<int:article_pk>', views.article_detail),
]
```

serializers.py

```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    
    class Meta:
        model = Article
        # fields = '__all__'
        fields = ('id', 'title','content',)
```

views.py

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from django.shortcuts import render
from django.http.response import JsonResponse, HttpResponse
from django.core import serializers
from .serializers import ArticleSerializer
from .models import Article

def article_list(request):
    articles = Article.objects.all()
    serializer = ArticleSerializer(articles, many=True)
    return Response(serializer.data)
def article_detail(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    serializer = ArticleSerializer(article)
    return Response(serializer.data)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/81561830-d4cf-4b15-bad9-0e9b73533a3f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e5edb98-8b89-486f-ba2b-08008ffcb20e/Untitled.png)