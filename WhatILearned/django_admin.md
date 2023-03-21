# Django admin


## Admin_site

- automatic admin interface
- 관리자 페이지
    - 사용자가 아닌 서버의 관리자가 활용하기 위한 페이지
    - 모델 class를 admin.py에 등록하고 관리
    - 레코드 생성 여부 확인에 매우 유용하며 직접 레코드를 삽입할 수 있다.
    - 가상환경을 만들었다면 ipython, django-extensions를 설치해주어야 한다.
    
    ```html
    $ pip install ipython django-extensions
    ```
    

## CRUD with view functions

```html
$ python manage.py createsuperuser

모델의 record를 보기 위해서는 admin.py에 등록 필요
from django.contrib import admin
from .models import Article

admin.site.register(Article)
```

- settings.py

```html
INSTALLED_APPS = [
		'django_extensions',
    'articles',
]
Templates = [
	'DIRS': [BASE_DIR / 'templates'],
]

```

- urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

- views.py

```python
from django.shortcuts import render

# Create your views here.
def index(request):
    return render(request, 'articles/index.html')
```

- crud/urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
]
```

- base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CRUD</title>
  <!-- CSS only -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
</head>
<body>
  {% block content %}
  {% endblock content %}

  <!-- JavaScript Bundle with Popper -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-kenU1KFdBIe4zVF0s0G1M5b4hcpxyD9F7jL+jjXkk+Q2h455rYXK/7HAuoJl+0I4" crossorigin="anonymous"></script>
</body>
</html>
```

- index.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>INDEX</h1>
{% endblock content %}
```

- model

```python
from django.db import models

# Create your models here.
class Article(models.Model):
    title = models.CharField(max_length=30)
    content = models.TextField()

    creadted_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
		
		def __str__(self):
        return f'{self.id}번째 글 - {self.title}'
```

→ 참고로 created_at이 되어야하는데 ㅋㅋㅋㅋㅋ

→ creadted_at으로 잘못 적었다는점 ㅋㅋㅋㅋㅋㅋㅋ

- admin

```python
from django.contrib import admin
from .models import Article

# Register your models here.
admin.site.register(Article)
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/eb87c996-4835-4469-9996-4964346de8bd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234410Z&X-Amz-Expires=86400&X-Amz-Signature=73e24d5e256c1799044e60888e660f9f4bf07b96e258d056233fe8d718e7cb93&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/efdcd298-caf5-4d66-806b-a902cbe6b2aa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234419Z&X-Amz-Expires=86400&X-Amz-Signature=56210827d9fbb1b11147e696d5dcf96f394ec280b3471d2209e4bcb537b3cea8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/06734a50-abc0-40d4-8c16-f1bcf4238d43/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234427Z&X-Amz-Expires=86400&X-Amz-Signature=703338c7de96f098fd1b587d933af5332080d66b200f31754b11c8968232b308&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/745ef550-3c40-44bf-989c-b3fa1fdd3685/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234436Z&X-Amz-Expires=86400&X-Amz-Signature=bb8eee5968347d3f79a1f61cd267aa0c730fab21033c186db155441f269c02c2&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```python
from django.shortcuts import render
from .models import Article

# Create your views here.
def index(request):
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Articles</h1>
  <hr>
  {% for article in  articles %}
    <p>글 번호 : {{article.pk}} </p>
    <p>글 제목 : {{article.title}} </p>
    <p>글 내용: {{article.content}} </p>
    <hr>
  {% endfor %}
{% endblock content %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/40e910f4-e67d-42d1-9398-927e59fa0eb7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234455Z&X-Amz-Expires=86400&X-Amz-Signature=d42e76357fbfb938fc1b9c2497e7946478097f875f1221a27c643fbc18e79123&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:pk>/', views.detail, name='detail' ),
]
```

```python
from django.shortcuts import render
from .models import Article

# Create your views here.
def index(request):
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {'article' : article}

    return render(request, 'articles/detail.html', context)
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Detail</h1>
  <hr>
  <p>글 제목 : {{article.title}} </p>
  <p>글 내용 : {{article.content}} </p>
  <p>글 생성시각: {{article.created_at}} </p>
  <p>글 수정시각: {{article.created_at}} </p>
	<a href=" {% url 'articles:index' %} ">목록보기</a>
{% endblock content %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3190ac29-1686-4b8f-8d12-2328276ba7ab/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T234505Z&X-Amz-Expires=86400&X-Amz-Signature=13b09691afe11aa08a2c5073e49c6fffa701e596a39432f8c1a3eec86273c580&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)