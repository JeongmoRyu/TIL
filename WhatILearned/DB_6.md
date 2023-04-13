# DB_6

## profile창 만들기

accounts/url.py

```python
path('profile/<str:username>/', views.profile, name='profile'),
```

accounts/views.py

```python
from django.contrib.auth import get_user_model

def profile(request, username):
    User = get_user_model()
    person = User.objects.get(username=username)
    context = {
        'person': person,
    }
    return render(request, 'accounts/profile.html', context)
```

accounts/templates/profile.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>{{person.username}}님의 프로필</h1>

  <hr>
  <h3>{{person.username}}'s 게시글 </h3>
  {% for article in person.article_set.all %}
    {% comment %} <a href="{% url 'articles:detail' article.pk %} ">{{article.title}} </a> {% endcomment %}
    <div class="card">
      <div class="card_body">
        <h5 class="card-title">{{article.title}} </h5>
        <p class="card_text">{{article.content}} </p>
        <a href="{% url 'articles:detail' article.pk %}" class="btn btn-primary"> 자세히 보기 </a>
      </div>
    </div>
  {% endfor %}

  <hr>
  <h3>{{person.username}}'s 댓글 </h3>
    {% for comment in person.comment_set.all %}
      <div>{{comment.content}} </div>
    {% endfor %}
  
  <hr>
  <h3>{{person.username}}'s 좋아요! 게시물 </h3>
  {% for article in person.like_articles.all %}
    <a href="{% url 'articles:detail' article.pk %} ">{{article.title}} </a>
  {% endfor %}

  <hr>
  <a href="{% url 'articles:index' %}" class="btn btn-success">BACK</a>

{% endblock content %}
```

base.html

```python
<h3 id="user-hello"><i>안녕하세요, <a href="{% url 'accounts:profile' user.username %}">{{user}} </a> 님 !</i></h3>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01377c41-6099-47a9-a41a-be6ccd03cbfe/Untitled.png)

## Follow 만들기

accounts/model.py

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

# Create your models here.
class User(AbstractUser):
    followings = models.ManyToManyField('self', symmetrical=False, related_name='followers')
```

accounts/url.py

```python
path('<int:user_pk>/follow/', views.follow, name='follow'),
```

accounts/views.py

```python
def follow(request, user_pk):
    if request.user.is_authenticated:
        User = get_user_model()
        person = User.objects.get(pk=user_pk)
        if person != request.user:
            if person.followers.filter(pk=request.user.pk).exist():
                person.followers.remove(request.user)
            else:
                person.followers.add(request.user)
        return redirect('accoutns:profile', person.username)
    return redirect('accounts:login')
```

accounts/templates/profile.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>{{person.username}}님의 프로필</h1>
  <div>
    <div>
      팔로잉 : {{person.followings.all|length}} / 팔로워 : {{person.followers.all|length}}
    </div>
    {% if request.user != person %}
      <div>
        <form action="{% url 'accounts:follow' person.pk %}" method="POST">
          {% csrf_token %}
          {% if request.user in person.followers.all %}
            <input type="submit" value="Unfollow">
          {% else %}
            <input type="submit" value="Follow">
          {% endif %}
        </form>
      </div>
    {% endif %}
  </div>

  <hr>
  <h3>{{person.username}}'s 게시글 </h3>
  {% for article in person.article_set.all %}
    {% comment %} <a href="{% url 'articles:detail' article.pk %} ">{{article.title}} </a> {% endcomment %}
    <div class="card">
      <div class="card_body">
        <h5 class="card-title">{{article.title}} </h5>
        <p class="card_text">{{article.content}} </p>
        <a href="{% url 'articles:detail' article.pk %}" class="btn btn-primary"> 자세히 보기 </a>
      </div>
    </div>
  {% endfor %}

  <hr>
  <h3>{{person.username}}'s 댓글 </h3>
    {% for comment in person.comment_set.all %}
      <div>{{comment.content}} </div>
    {% endfor %}
  
  <hr>
  <h3>{{person.username}}'s 좋아요! 게시물 </h3>
  {% for article in person.like_articles.all %}
    <a href="{% url 'articles:detail' article.pk %} ">{{article.title}} </a>
  {% endfor %}

  <hr>
  <a href="{% url 'articles:index' %}" class="btn btn-success">BACK</a>

{% endblock content %}
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/242d8078-f9ec-4488-86bd-1575b4c19ab3/Untitled.png)