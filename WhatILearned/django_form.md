# Django Form

- 사용자가 입력한 데이터가 우리가 원하는 데이터 형식이 맞는지에 대한 유효성 검증이 필요하다.
- Django Form은 과정에서 과중한 작업과 반복 코드를 줄여줌으로써 훨씬 수비게 유효성 검증을 진행할 수 있도록 만들어 준다.
- Django는 Form과 관련한 유효성 검사를 단순화하고 자동화 할 수 있는 기능을 제공하여 , 개발자가 직접 작성하는 코드보다 더 안전하고 빠르게 수행하는 코드를 작성 할 수 있다.

## Django Form Class

- [forms.py](http://forms.py) 생성후 ArticleForm class선언

```python
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=30)
    content = forms.CharField()
```

- view 업데이트

```python
from django.shortcuts import render, redirect
from .models import Article
from .forms import ArticleForm

# Create your views here.
def index(request):
    articles = Article.objects.all()
    context = {'articles': articles}
    return render(request, 'articles/index.html', context)

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {'article': article}
    return render(request, 'articles/detail.html', context)

def create(request):
    if request.method == 'POST':
        title = request.POST.get('title')
        content = request.POST.get('content')
        article = Article(title=title, content=content)
        article.save()
        return redirect('articles:detail', pk=article.pk)
    else:
        form = ArticleForm()
        context = {'form' : form}
        return render(request, 'articles/create.html', context)

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')

def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        article.title = request.POST.get('title')
        article.content = request.POST.get('content')
        article.save()
        return redirect('articles:detail', pk=article.pk)
    else:
        context = {'article': article}
        return render(request, 'articles/update.html', context)
```

- create.html 변경

```
{% extends 'base.html' %}

{% block content %}
  <h1>글작성</h1>
  <hr>

  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    {{form.as_p}}
    <input type="submit">
  </form>
{% endblock content %}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d9a28459-28d2-48e0-a04e-816d270f6599/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235747Z&X-Amz-Expires=86400&X-Amz-Signature=cdc928b2c8b51188df450a22c2451702863e5da6c271e5697556a12551561e8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- From rendering option
    - label & input 쌍에 대한 3가지 출력 옵션
    1. as_p()
        1. p태그로 감싸져서 렌더링
    2. as_ul()
        1. li 태그로 감싸져서 렌더링
        2. ul 태그는 직접 작성해야한다.
    3. as_table()
        1. tr 태그로 감싸져서 렌더링

- HTML input 요소
    - Form fields
        - 입력에 대한 유효성 검사 로직을 처리한다.
        - 템플릿에서 직접 사용된다.
    - Widgets
        - 웹 페이지의 HTML input 요소 렌더링을 담당
            - input 보여지는 부분을 변경한다.
        - Widgets은 form fields에 할당된다.
        

## WIDGETs

- 웹 페이지의 HTML input element 렌더링을 담당
    - 유효성 검증과는 관계 X
    - input 보여지는 부분을 변경한다.
    
    ```python
    from django import forms
    
    class ArticleForm(forms.Form):
        title = forms.CharField(max_length=30)
        content = forms.CharField(widget=forms.Textarea)
    ```
    

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68730021-c71b-4bfa-a978-da8a41fdb7ab/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235804Z&X-Amz-Expires=86400&X-Amz-Signature=88146310744533a6fd1b52e6a1c36c413efee9d3d889c6a88add1a4d36874289&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## Django ModelForm

- Model을 통해 Form Class를 만들 수 있는 helper class
- ModelForm은 Form과 똑같은 방식으로 View 함수에서 사용
- ModelForm 선언
    - forms 라이브러리에서 파생된 ModelForm 클래스를 상속받음
    - 클래스 안에 Meta 클래스 선언
    - exclude 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 있다.

```python
from django import forms
from .models import Article

# class ArticleForm(forms.Form):
#     title = forms.CharField(max_length=30)
#     content = forms.CharField(widget=forms.Textarea)

class ArticleForm(forms.ModelForm):
    
    class Meta:
        model = Article
        fields = '__all__'
#        exclude = ('title',)
# fields랑 같이 써도 되지만 주로 따로 사용한다.
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68730021-c71b-4bfa-a978-da8a41fdb7ab/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235813Z&X-Amz-Expires=86400&X-Amz-Signature=2a99feae581d474fe9e9d13ccd12943abae9f8a9d4cbd3c4e462e9ea3ac860a5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- is_valid() 유효성 검사
    - views
    
    ```python
    def create(request):
        if request.method == 'POST':
            form = ArticleForm(request.POST)
            if form.is_valid():
                article = form.save()
                return redirect('articles:detail', article.pk)
            # title = request.POST.get('title')
            # content = request.POST.get('content')
            # article = Article(title=title, content=content)
            # article.save()
            return redirect('articles:create', pk=article.pk)
        else:
            form = ArticleForm()
            context = {'form' : form}
            return render(request, 'articles/create.html', context)
    ```
    
- save() method
    - form 인스턴스 바인딩 된 데이터를 통해 데이터베이스 객체를 만들고 저장
    - ModelForm의 하위 클래스는 키워드 인자 instance 여부를 통해 생성할지 수정할 지를 정한다.
    - 정리해보면
- create 수정하기

```
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm()
    context = {'form' : form}
    return render(request, 'articles/create.html', context)
```

- update 수정하기
- 

```
def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm(instance=article)
        
    context = {'form': form, 'article': article}
    return render(request, 'articles/update.html', context)
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>UPDATE</h1>
  <hr>

  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>

  <hr>
  <a href="{% url 'articles:detail' article.pk %}">[BACK]</a>
{% endblock content %}
```

- 위젯을 작성하는 2가지 방법

```python
class ArticleForm(form.ModelForm):
		class Meta:
				model = Article
				fields = '__all__'
				widgets = {
							'title': forms.TextInput(attrs={
									'class':'title',
									'placeholder':'Enter the title',
									'maxlength':10,
									}
						)
				}
```

```python
class ArticleForm(form.ModelForm):
		title = forms.CharField(
				label='제목',
				widget=forms.TextInput(
						attrs={
								'class': 'my-title',
								'placeholder':'Enter the title',
						}
				),
		)

		class Meta:
				model = Article
				fields = '__all__'
```

## Stactic files

- 파일 자체가 고정되어 있고, 서비스 중에도 추가되거나 변경되지 않고 고정되어 있는 상황
- Media File
    - 미디어 파일
    - 사용자가 웹에서 업로드하는 정적 파일
    
    client → http request → server
    
    client ← http response ← server
    

- base.html

```
{% load static %}

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href=" {% static 'base.css' %} ">
  <title>CRUD PJT</title>
</head>
<body>

  {% block content %}
  {% endblock content %}
  
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

- settings

```python
STATIC_URL = '/static/'
STATICFILES_DIRS=[
    BASE_DIR / 'static',
]
```

- base.css를 static 폴더를 만들어서 생성해준다.
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b1786342-70f5-4a9c-89f5-a6767b0855ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235828Z&X-Amz-Expires=86400&X-Amz-Signature=ebad778f308e5a7997d6b6770f30eba878747a60df6f9512cc2b608387d70ef9&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/795ff57c-42b2-4964-8265-a0a1eef9c9c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235850Z&X-Amz-Expires=86400&X-Amz-Signature=b3facae5c4282bfda7b874e3e6b889a09d4159c0405513d497decdb1f4099f3e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/813b3776-ddad-4cf1-938f-ab6c51b5afc6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235903Z&X-Amz-Expires=86400&X-Amz-Signature=57c73dae356fa26b50996671d68d3c53ae081a48a1c3b704ee7b99991d42f240&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    templates처럼 전체에 할 수도 있다.
    
    settings.py에도 추가를 해주면 된다.
    
    ```python
    STATIC_URL = '/static/'
    STATICFILES_DIRS=[
        BASE_DIR / 'static',
    ]
    ```
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4e92e213-5974-40b8-928a-f6c69f713b3f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235911Z&X-Amz-Expires=86400&X-Amz-Signature=9f27de09163791d2d9f21076b6d3683d72a347a31c9198e5efce9e162fda89bc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/813b3776-ddad-4cf1-938f-ab6c51b5afc6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235924Z&X-Amz-Expires=86400&X-Amz-Signature=2ec8c5bc1b21bd2b40360117acecd41b3d56e640ce67be7cdadfea93a4750609&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/84be233a-9860-4d3a-9b4b-b43e0dd20f9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230323%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230323T235935Z&X-Amz-Expires=86400&X-Amz-Signature=c312d4ea732e303ce2968fbb5d2bf9045cc784f1c6fbad212d035c3d77eec552&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)