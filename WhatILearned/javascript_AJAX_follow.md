# JS AJAX



- Asynchronous JavaScript And XML ( 비동기식 JavaScript 와 XML )
- 비동기 통신을 이용하면 화면 전체를 새로고침하지 않아도 서버로 요청을 보내고 데이터를 받아 화면의 일부분만 업데이트 가능하다
- 비동기 웹 통신을 위한 라이브러리 중 하나가 Axios

## AJAX

- reload(새로고침) 하지 않아도 수행되는 비동기성
- 일부분만 업데이트 할 수 있다.

## 비동기(Async) 적용하기

- 각각의 템플릿에서 script 코드를 작성하기 위한 block tag 영역을 작성한다.

```html
{% block script%}
{% endblock script%}
```

## Follow

- axios CDN
    
    ```html
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    ```
    

base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-gH2yIJqKdNHPEq0n4Mqa/HGKIhSkIHeL5AyhkYV8i59U5AR6csBvApHHNl/vI1Bx" crossorigin="anonymous">  <title>Document</title>
</head>
<body>
  <div class="container">
    {% if request.user.is_authenticated %}
      <h3>{{ user }}</h3>
      <a href="{% url 'accounts:profile' user.username %}">내 프로필</a>
      <form action="{% url 'accounts:logout' %}" method="POST">
        {% csrf_token %}
        <input type="submit" value="Logout">
      </form>
      <form action="{% url 'accounts:delete' %}" method="POST">
        {% csrf_token %}
        <input type="submit" value="회원탈퇴">
      </form>
      <a href="{% url 'accounts:update' %}">회원정보수정</a>
    {% else %}
      <a href="{% url 'accounts:login' %}">Login</a>
      <a href="{% url 'accounts:signup' %}">Signup</a>
    {% endif %}
    <hr>
    {% block content %}
    {% endblock content %}

    {% block script %}
    {% endblock script %}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-A3rJD856KowSb7dwlZdYEkO39Gagi7vIsF0jrRAoQmDKKtQBHUuLZ9AsSv4jD4Xa" crossorigin="anonymous"></script>
</body>
</html>
```

profile.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>{{ person.username }}님의 프로필</h1>
  <div>
    <span id="followers-count">팔로워 : {{ person.followers.all|length }} /</span>
    <span id="followings-count">팔로잉 : {{ person.followings.all|length }}</span>
     
  </div>

  {% if request.user != person %}
  <div>
    <form id="follow-form" data-user-id="{{person.pk}}">
      {% csrf_token %}
      {% if request.user in person.followers.all %}
      <button type="submit" class="btn btn-secondary">언팔로우</button>
        <!-- <input type="submit" value="언팔로우"> -->
      {% else %}
      <button type="submit" class="btn btn-primary">팔로우</button>

        <!-- <input type="submit" value="팔로우"> -->
      {% endif %}
    </form>
  <div>
  {% endif %}

  <h2>{{ person.username }}이 작성한 모든 게시글</h2>
  {% for article in person.article_set.all %}
    <div>{{ article.title }}</div>
  {% endfor %}

  <hr>

  <h2>{{ person.username }}이 작성한 모든 댓글</h2>
  {% for comment in person.comment_set.all %}
    <div>{{ comment.content }}</div>
  {% endfor %}

  <hr>

  <h2>{{ person.username }}이 좋아요 한 모든 게시글</h2>
  {% for article in person.like_articles.all %}
    <div>{{ article.title }}</div>
  {% endfor %}

  <a href="{% url 'articles:index' %}">back</a>
{% endblock content %}

{% block script %}
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>>
  <script>
    const form = document.querySelector('#follow-form')
    form.addEventListener('submit', function (event) {
      event.preventDefault()

      const userId = event.target.dataset.userId
      const csrftoken = document.querySelector('[name=csrfmiddlewaretoken]').value;
      
      axios({
        method :'post',
        url: `/accounts/${userId}/follow/`,
        headers: {'X-CSRFToken': csrftoken},

      })
      .then((response) => {
        const isFollowed = response.data.is_followed
        const followBtn = document.querySelector('#follow-form > button')
        const followerscountTag = document.querySelector('#followers-count')
        const followingscountTag = document.querySelector('#followings-count  ')

        followBtn.classList.toggle('btn-primary')
        followBtn.classList.toggle('btn-secondary')
        // 버튼을 눌릴 때마다 색이 바뀔 수 있게 꾸밀 수 있다.
        const followersCount = response.data.followers_count
        const followingsCount = response.data.followings_count
        followerscountTag.innerText = followersCount
        followingscountTag.innerText = followingsCount

        if (isFollowed === true) {
          followBtn.innerText = '언팔로우'
        } else {
          followBtn.innerText = '팔로우'
        }
      })
    })
  </script>

{% endblock script %}
```

views.py

```python
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
from django.contrib.auth import update_session_auth_hash
from django.contrib.auth.decorators import login_required
from django.contrib.auth.forms import AuthenticationForm, PasswordChangeForm
from django.shortcuts import redirect, render
from django.views.decorators.http import require_http_methods, require_POST
from django.contrib.auth import get_user_model
from .forms import CustomUserChangeForm, CustomUserCreationForm
from django.http import JsonResponse

# Create your views here.
@require_http_methods(['GET', 'POST'])
def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')

    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        # form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            # 로그인
            auth_login(request, form.get_user())
            return redirect(request.GET.get('next') or 'articles:index')
    else:
        form = AuthenticationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)

@require_POST
def logout(request):
    if request.user.is_authenticated:
        auth_logout(request)
    return redirect('articles:index')

@require_http_methods(['GET', 'POST'])
def signup(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
        
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            # 회원가입 후 로그인
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)

@require_POST
def delete(request):
    if request.user.is_authenticated:
        request.user.delete()
        auth_logout(request)
    return redirect('articles:index')

@login_required
@require_http_methods(['GET', 'POST'])
def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
        # form = CustomUserChangeForm(data=request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/update.html', context)

@login_required
@require_http_methods(['GET', 'POST'])
def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        # form = PasswordChangeForm(user=request.user, data=request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            return redirect('articles:index')
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/change_password.html', context)

def profile(request, username):
    User = get_user_model()
    person = User.objects.get(username=username)
    context = {
        'person': person,
    }
    return render(request, 'accounts/profile.html', context)

@require_POST
def follow(request, user_pk):
    if request.user.is_authenticated:
        User = get_user_model()
        me = request.user
        you = User.objects.get(pk=user_pk)
        if me != you:
            if you.followers.filter(pk=me.pk).exists():
                you.followers.remove(me)
                is_followed = False
            else:
                you.followers.add(me)
                is_followed = True
            context = {
                'is_followed': is_followed,
                'followers_count':you.followers.count(),
                'followings_count' : you.followings.count()
            }
            return JsonResponse(context)
        # return redirect('accounts:profile', you.username)
    return redirect('accounts:login')
```