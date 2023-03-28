# Django_authentication_and_authorization(인증과권한)2

## 회원가입

- accounts/urls.py

```python
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('signup/', views.signup, name='signup'),
    
]
```

- accounts/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
##
from django.contrib.auth.forms import UserCreationForm

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')

def signup(request):
    if request.method == 'POST':
        pass
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```

- accounts/signup.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>회원가입</h1>

  <form action=" {% url 'accounts:signup' %} " method='POST'>
    {% csrf_token %}
    {{form.as_p}}
    <input type="submit" value='회원가입'>

  </form>
  <a href=" {% url 'articles:index' %} ">목록보기</a>
{% endblock content %}
```

![Untitled](https://file.notion.so/f/s/27ab94ee-366c-4c18-85cc-5c387f73d381/Untitled.png?id=00d419ac-7157-4500-a19a-aa7eca26312e&table=block&spaceId=f826548c-dfb0-4cf8-95d5-a414595fcdae&expirationTimestamp=1680072678685&signature=-jaJpeY1UOkhn5PvNM1VYjVIG_LuoaL5f2jIBK_z9Nk&downloadName=Untitled.png)

![Untitled](https://file.notion.so/f/s/f1e23a45-441d-4c1f-ac5f-6a7f692f5433/Untitled.png?id=3c547d52-ee47-4730-bc5e-785e5dec8ab6&table=block&spaceId=f826548c-dfb0-4cf8-95d5-a414595fcdae&expirationTimestamp=1680072690470&signature=fqJP4bFjzgL9e_sqQAhAlWFFiQTM9nXl5hVsdmoAPNk&downloadName=Untitled.png)

![Untitled](https://file.notion.so/f/s/9011972e-af58-4035-8064-f93de3c6e085/Untitled.png?id=f24f423e-36fe-4388-86c7-bf61a9f22951&table=block&spaceId=f826548c-dfb0-4cf8-95d5-a414595fcdae&expirationTimestamp=1680072703996&signature=6Sc9zeCrz2Nc73kU10Ftu0sKNEkYdPkbGcw8P1ZXlpc&downloadName=Untitled.png)

→ form 만들어주기

- accounts/forms.py

```python
from django.contrib.auth.forms import UserCreationForm, UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = get_user_model()

class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
```

- accounts/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
##
from django.contrib.auth.forms import UserCreationForm
from .forms import CustomUserCreationForm, CustomUserChangeForm

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')

def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            form.save()
						auth_login(request, user)
            return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)

	

```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d8cc8f97-ff35-4b18-affb-b1a7a2b34504/Untitled.png)

## 회원탈퇴

- accounts/urls.py

```python
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('signup/', views.signup, name='signup'),
    path('delete/', views.delete, name='delete'),
    
]
```

- accounts/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
##
from django.contrib.auth.forms import UserCreationForm
from .forms import CustomUserCreationForm, CustomUserChangeForm

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')

def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)

def delete(request):
    user = request.user.delete()
    auth_logout(request)
    return redirect('articles:index')
```

- templates/base.html

```html
{% load static %}

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">

    <link rel="stylesheet" href="{% static 'base.css' %}">
    <title>CRUD PJT</title>
  </head>
  
  <body>
    <div id="nav">
      <a href=" {% url 'accounts:signup' %} ">회원가입</a>
      <a href="{% url 'accounts:login' %}">로그인</a>
      <a href="{% url 'accounts:logout' %}">로그아웃</a>
      <form action=" {% url 'accounts:delete' %} " method='POST'>
        {% csrf_token %}
        <input type="submit" value='회원탈퇴'>

      </form>
    </div>
    <h3 id="user-hello"><i>안녕하세요, {{user}} 님 !</i></h3>
    <hr>
    <div id="content">
      {% block content %}{% endblock content %}
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </body>
</html>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8222cb3a-88d2-44c3-ada2-bb329ad1335f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93a39a26-0153-499e-a54c-13a7b6d96236/Untitled.png)

## 회원정보 수정

UserChangeForm

- accounts/forms.py

```python
from django.contrib.auth.forms import UserCreationForm, UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = get_user_model()

class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
```

- accounts/urls.py

```python
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('signup/', views.signup, name='signup'),
    path('delete/', views.delete, name='delete'),
    path('update/', views.update, name='update'),
    
]
```

- accounts/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
##
from django.contrib.auth.forms import UserCreationForm
from .forms import CustomUserCreationForm, CustomUserChangeForm

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')

def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)

def delete(request):
    user = request.user.delete()
    auth_logout(request)
    return redirect('articles:index')

def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
        
    else:
        form = CustomUserChangeForm(instance=request.user)
    context={
        'form': form,
    }
    return render(request, 'accounts/update.html', context)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42b093e5-db45-48ac-8c13-333080063ce0/Untitled.png)

- 너무 많은 정보를 제공하기 때문에 fields를 지정해준다.

```python
from django.contrib.auth.forms import UserCreationForm, UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = get_user_model()

class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
        fields = ('email', 'first_name', 'last_name')
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43c93c8b-0621-4103-88ad-6519cbc0db30/Untitled.png)

수정을 하고 다시 수정하기로 들어가면 입력이 되어있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aca38774-349c-46bd-b5b3-824ea0ffb1a5/Untitled.png)

## 비밀번호 수정

- templates/accounts/change_password.html

```
{% extends 'base.html' %}

{% block content %}
  <h1>비밀번호 변경</h1>

  <form action=" {% url 'accounts:change_password' %} " method='POST'>
    {% csrf_token %}
    {{form.as_p}}
    <input type="submit" value='비밀번호수정'>

  </form>
  <a href=" {% url 'articles:index' %} ">목록보기</a>
{% endblock content %}
```

- accounts/views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm, PasswordChangeForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
##
from django.contrib.auth.forms import UserCreationForm
from .forms import CustomUserCreationForm, CustomUserChangeForm
from django.contrib.auth import update_session_auth_hash

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {'form': form}
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')

def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)

def delete(request):
    user = request.user.delete()
    auth_logout(request)
    return redirect('articles:index')

def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
        
    else:
        form = CustomUserChangeForm(instance=request.user)
    context={
        'form': form,
    }
    return render(request, 'accounts/update.html', context)

def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            return redirect('articles:index')
        
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form':form,
    }
    return render(request, 'accounts/change_password.html', context)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/782afcde-87e3-4f29-9b8a-9ba1df0457cb/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3a2786e-c57f-451d-ad37-47de58624694/Untitled.png)

→ 원래 비밀번호로 사용하면 제대로 입력하라고 뜬다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3644de87-1af1-416b-a92c-e662e166b06f/Untitled.png)

→ 있는 Username을 사용하면 다른 이름을 사용하라고 뜬다.

## Decorator : HTTP methods

articles/views.py

```python
from django.shortcuts import render, redirect
from .models import Article
from .forms import ArticleForm
from django.views.decorators.http import require_http_methods, require_POST, require_safe

# Create your views here.
@require_safe
def index(request):
    articles = Article.objects.all()
    context = {'articles': articles}
    return render(request, 'articles/index.html', context)

@require_safe
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {'article': article}
    return render(request, 'articles/detail.html', context)

@require_http_methods(['GET', 'POST'])
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm()

    context = {'form': form}
    return render(request, 'articles/create.html', context)

@require_POST
def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')

@require_http_methods(['GET', 'POST'])
def update(request, pk):
    article = Article.objects.get(pk=pk)

    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail', pk=article.pk)
    else:
        form = ArticleForm(instance=article)

    context = {'form': form, 'article': article}
    return render(request, 'articles/update.html', context)
```

## Limiting access to logged_in users

- is_authenicated 적용하기
    - 로그인과 비로그인 상태에서 출력되는 링크를 다르게 설정하기
- templates/base.html

```html
{% load static %}

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">

    <link rel="stylesheet" href="{% static 'base.css' %}">
    <title>CRUD PJT</title>
  </head>
  
  <body>

    <div id="nav">
      {% if request.user.is_authenticated %}
        <h3 id="user-hello"><i>안녕하세요, {{user}} 님 !</i></h3>
        <a href="{% url 'accounts:logout' %}">로그아웃</a>

        <a href=" {% url 'accounts:update' %} ">정보수정</a>
        <form action=" {% url 'accounts:delete' %} " method='POST'>
          {% csrf_token %}
          <input type="submit" value='회원탈퇴'>
        </form>
      {% else %}
        <a href=" {% url 'accounts:signup' %} ">회원가입</a>

        <a href="{% url 'accounts:login' %}">로그인</a>
      {% endif %}
    </div>
    
    
    <hr>

    <div id="content">
      {% block content %}
      {% endblock content %}
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </body>
</html>
```

- articles/views.py

```python
from django.shortcuts import render, redirect
from .models import Article
from .forms import ArticleForm
from django.views.decorators.http import require_http_methods, require_POST, require_safe

# Create your views here.
@require_safe
def index(request):
    articles = Article.objects.all()
    context = {'articles': articles}
    return render(request, 'articles/index.html', context)

@require_safe
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {'article': article}
    return render(request, 'articles/detail.html', context)

@require_http_methods(['GET', 'POST'])
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm()

    context = {'form': form}
    return render(request, 'articles/create.html', context)

@require_POST
def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')

@require_http_methods(['GET', 'POST'])
def update(request, pk):
    article = Article.objects.get(pk=pk)

    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail', pk=article.pk)
    else:
        form = ArticleForm(instance=article)

    context = {'form': form, 'article': article}
    return render(request, 'articles/update.html', context)

def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1dd8b6a7-72d9-479b-9551-ac30361e29ec/Untitled.png)