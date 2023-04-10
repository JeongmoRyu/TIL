# DB

## A Many-To-One-Relationship

- RDB에서 1:1 관계 혹은 M:N 관계가 아닌 한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 경우
- 기준 테이블에 따라 (1:N)이라고도 한다.
    - ex) 고객 1명이 여러 주문을 할 수 있다.

### Foreign KEY

- 외래 키(외부 키)
- 관계형 데이터베이스에서 다른 테이블의 행을 식별할 수 있는 키
- 참조되는 테이블의 기본 키(Primary Key)
- 참조하는 테이블의 행 1개의 값은 참조되는 측 테이블의 행 값에 대응된다.
    - 이로 인해 참조하는 테이블의 행에는 참조되는 테입르에 나타나지 않는 값을 포함 할 수 없다.
- 키를 사용하여 부모 테이블의 유일한 값을 참조(참조 무결성)
- 외래 키의 값이 반드시 부모 테이블의 기본 키일 필요는 없지만 유일한 값이어야 한다.

## N:1 (Commnet - Article)

- 모델 관계 설정
    - 댓글창 만들어보기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/248c37f8-bea7-4034-a51f-049a0559bacc/Untitled.png)

models.py

```python
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.content
```

- ForeignKey arguments - on_delete
    - 외래 키가 참조하는 객체가 사라졌을 때 외래 키를 가진 객체를 어떻게 처리할 지를 정의
    - 데이터 무결성을 위해서 매우 중요한 설정
    - on-delete 옵션 값
        - CASCADE : 부모 객체(참조된 객체)가 삭제되었을 때 이를 참조하는 객체도 삭제
        - PROTECT, SET_NULL, SET_DEFAULT

shell_plus

```html
In [1]: comment = Comment()

In [2]: comment.content = 'first comment'

In [3]: article = Article.objects.create(title='title', content='content')

In [4]: Article.objects.all()
Out[4]: <QuerySet [<Article: 1번째글 - 첫번째>, <Article: 2번째글 - title>]>

In [5]: comment.article = article

In [6]: article.save()

이렇게 확인할 수도 있다. 
In [7]: comment.article
Out[7]: <Article: 2번째글 - title>

In [8]: comment.article.content
Out[8]: 'content'

In [9]: comment.article.title
Out[9]: 'title'
```

다시만들어보자

```html
In [10]: comment = Comment(content='second comment', article=article)

In [11]: comment.article_id
Out[11]: 2

In [12]: comment.save()
```

### 관계 모델 참조

- Related manager
    - N:1, M:N 관계에서 사용 가능한 문맥
    - 역참조할 때 사용 가능한 manager생성
        - 모델 생성 시 objects라는 매니저를 통해 queryset api를 사용한 것처럼 related manager를 통해 queryset api를 사용할 수 있다.
    - 역참조
        - 나를 참조하는 테이블을 참조하는 것
        - 본인을 외래 키로 참조 중인 다른 테이블에 접근하는 것
        - article.comment_set.method()
        - 역참조 시 사용하는 매니저 이름을 변결할 수 도 있다.
            - 작성 후 migration 필요
        
        ```html
        article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
        ```
        
        - related_name 작성

```html
In [15]: article = Article.objects.get(id=2)

In [16]: article.comment_set.all()
Out[16]: <QuerySet [<Comment: second comment>]>

In [17]: article.comment_set.get(id=1)
Out[17]: <Comment: second comment>
```

### Comment 구현

- views.py

```python
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm()
    context = {
        'article': article,
        'comment_form' : comment_form,
        }
    return render(request, 'articles/detail.html', context)
```

- detail.html

```html
{% extends 'base.html' %} 

{% block content %}
  <h1>DETAIL</h1>
  <hr />

  {% if article.image %}
    <img src="{{article.image.url}}" />
  {% endif %}

  <div id="article-content">
    <p>글 제목 : {{article.title}}</p>
    <p>글 내용 : {{article.content}}</p>
    <p>생성시각 : {{article.created_at}}</p>
    <p>수정시각 : {{article.updated_at}}</p>

    <hr>
    <a href="{% url 'articles:update' article.pk %}">수정하기</a>
    <form action="{% url 'articles:delete' article.pk %}" id="delete-form">
      {% csrf_token %}
      <input type="submit" value="삭제하기" id="delete-btn" />
    </form><br>
    <hr>
    <a href="{% url 'articles:index' %}">목록보기</a>

    <br>

    <h5>Comments</h5>
    <hr>
    <form action="" method="POST">
      {% csrf_token %}
      {{comment_form}}
      <input type="submit" value="작성">

    </form>

  </div>
{% endblock content %}
```

- forms.py

```python
class CommentForm(forms.ModelForm):
    class Meta:
        model = Comment
        exclude = ('article',)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77c87dfc-dfa6-4995-a207-4bd602d64db8/Untitled.png)

views.py

```python
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm()
    comments = article.comment_set.all()
    context = {
        'article': article,
        'comment_form' : comment_form,
        'comments' : comments,
        }
    return render(request, 'articles/detail.html', context)

def comments_create(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm(request.POST)
    if comment_form.is_valid():
        comment = comment_form.save(commit=False)
        comment.article = article
        comment_form.save()
    return redirect('articles:detail', article.pk)
```

urls.py

```python
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:pk>/', views.detail, name='detail'),
    path('create/', views.create, name='create'),
    path('<int:pk>/delete/', views.delete, name='delete'),
    path('<int:pk>/update/', views.update, name='update'),
    path('<int:pk>/comments/', views.comments_create, name='comments_create'),
]
```

detail.py

```html
{% extends 'base.html' %} 

{% block content %}
  <h1>DETAIL</h1>
  <hr />

  {% if article.image %}
    <img src="{{article.image.url}}" />
  {% endif %}

  <div id="article-content">
    <p>글 제목 : {{article.title}}</p>
    <p>글 내용 : {{article.content}}</p>
    <p>생성시각 : {{article.created_at}}</p>
    <p>수정시각 : {{article.updated_at}}</p>

    <hr>
    <a href="{% url 'articles:update' article.pk %}">수정하기</a>
    <form action="{% url 'articles:delete' article.pk %}" id="delete-form">
      {% csrf_token %}
      <input type="submit" value="삭제하기" id="delete-btn" />
    </form><br>
    <hr>
    <a href="{% url 'articles:index' %}">목록보기</a>

    <br>

    <h5>Comments</h5>
    <hr>
      <ul>
        {% for comment in comments %}
          <li>{{comment.content}}</li>
        {% endfor %}
      </ul>

    <form action="{% url 'articles:comments_create' article.pk %}" method="POST">
      {% csrf_token %}
      {{comment_form}}
      <input type="submit" value="작성">

    </form>

  </div>
{% endblock content %}
```

Comment 삭제하기

views.py

```python
def comments_delete(request, article_pk, comment_pk):
    comment = Comment.objects.get(pk=comment_pk)
    comment.delete()
    return redirect('articles:detail', article_pk)
```

urls.py

```html
path('<int:article_pk>/comments/<int:comment_pk>/delete', views.comments_delete, name='comments_delete'),
```

detail.html

사이에 넣어주기

```html
<ul>
        {% for comment in comments %}
          <li>{{comment.content}}</li>
          <form action=" {% url 'articles:comment_delete' article.pk comment.pk %} " method="POST">
            {% csrf_token %}
            <input type="submit" value="DELETE">
          </form> 
        {% endfor %}
      </ul>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8a4f18df-b92f-4c40-8aa2-d6047e7cae35/Untitled.png)

- 댓글이 없을 때 있을 때 몇개가 존재한다. 등을 필터를 통해 표현 가능하다.

```html
<h5>Comments</h5>
    {% if comments %}
      <p><b> {{comments|length}}개의 댓글이 있습니다. </b></p>
    {% endif %}
    <hr>
      <ul>
        {% for comment in comments %}
          <li>{{comment.content}}
          <form action=" {% url 'articles:comments_delete' article.pk comment.pk %} " method="POST">
            {% csrf_token %}
            <input type="submit" value="DELETE">
          </form> 
          </li>
        {% empty %}
          <p>댓글이 없어요..    :( </p>
        {% endfor %}
      </ul>
```

## N:1 (Article - User)

Article(N) - User(1)

0개 이상의 게시글은 1개의 회원에 의해 작성될 수 있다.

### Referencing the user model

개인 게시글 회원 탈퇴시 삭제 및 확인

```python
from django.conf import settings
class Article 과 class Comment에 추가할 내용
user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
    )
```