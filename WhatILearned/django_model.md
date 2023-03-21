# Django Model

## Database

- 체계화된 데이터의 모임
- 검색 및 구조화 같은 작업을 보다 쉽게 하기 위해 조직화된 데이터를 수집하는 저장 시스템
- Database 기본 구조
    - 스키마(Schema)
        - 뼈대(structure)
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/375c8e3e-e614-405c-b180-6a8028676ff6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T000806Z&X-Amz-Expires=86400&X-Amz-Signature=a059c0236c224ddf9d78bbe3a3d28297e428b3f7a4a0a3a9e822747121744e09&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
            
    - 테이블(Table)
        - 필드와 레코드를 사용해 조직된 데이터 요소들의 집합
        - 관계(Relation)라고 부름
            1. 필드(field)
                1. 속성, 컬럼
                2. 각 필드는 고유한 데이터 형식이 지정됨(INT, TEXT 등)
            2. 레코드(record)
                1. 튜플, 행
                2. 테이블의 데이터는 레코드에 저장됨
                3. PK(Primary Key)
                    1. 각 레코드의 고유한 값
                    2. 다른 항목과 절대로 중복 될 수 없는 단일 값
                4. Query(쿼리)
                    1. 데이터를 조회하기 위한 명령어

## Model

- 모델 클래스 1개는 데이터베이스 테이블 1개

- 모델 만들기

```
from django.db import models

# Create your models here.
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
```

- 각 모델은 django.models.Model 클래스의 서브 클래스
    - django.db.models 모듈의 Model 클래스를 상속받아 구성
    - 클래스 상속 기반 형태의 Django 프레임워크 개발
    - title, content : DB 필드의 이름, 클래스 변수명
    - 뒤는 클래스 변수 값, DATA 타입
    - 데이터 유형에 따라 다양한 모델 필드를 제공
        - DataField()
        - CharField()
            - 길이의 제한이 있는 문자열을 넣을 때 사용
            - max_length
                - 필드의 최대 길이
                - CharField의 필수 인자
                - Django의 유효성 검사 때 활용
        - IntegerField()
        - TextField(**options)
            - 글자 수가 많을 때 사용
            - 저장할 때 길이에 대한 유효성을 검증하지 안는다.
    - 데이터베이스 스키마

## Migrations

- Django가 모델에 생긴 변화(필드 추가, 수정 등)을 실제 DB에 반영하는 방법
- makemigrations

```html
$ python manage.py makemigrations
```

- migrate : 모델의 변경사항과 데이터 베이스를 동기화

```html
$ python manage.py migrage
```

- showmigrations : migrate 되었는지 여부 확인

```html
$ python manage.py showmigrations
```

- sqlmigrate : SQL 문으로 어떻게 해석 될 지 확인 가능

```html
$ python manage.py sqlmigrate articles 0001
```

## ORM

- ORM이 설계도를 이해하고 동기화를 번역, 이해 가능하게 한다.
- Object-Relational-Mapping
- SQL을 사용하지 않고 데이터베이스를 조작할 수 있게 만들어준다.
- 장단점
    - 장점
        - SQL을 잘 알지 못해도 객체 지향 언어로 DB 조작이 가능
        - 객체 지향적 접근으로 인한 높은 **생산성**
    - 단점
        - ORM 만으로 세밀한 데이터베이스 조작을 구현하기 어려운 경우가 있다.

## QuerySet API

sqlite 설치, 파이썬 쉘 환경까지 사용

```html
$ pip install ipython
$ pip install django-extensions -> installed_APPS에 언더바로 넣어줘야한다.
$ pip freeze > requirements.txt
$ python manage.py shell_plus
```

- Database API
    - Django가 제공하는 ORM 을 사용하여 데이터 베이스를 조작하는 방법
    - Model을 정의하면 데이터를 만들고 읽고 수정하고 지울 수 있는 API를 제공
    - 
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/58964a65-0510-4171-b538-5d37593ae3c8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T000822Z&X-Amz-Expires=86400&X-Amz-Signature=0f781e9bd0524d82d4b4f559966360e7ac7599f22985ffad2c5be02c2038684f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - objects manager
        - DB를 python class로 조작할 수 있도록 여러 메서드를 제공하는  manager
    - Query
        - 데이터베이스에 특정한 데이터를 보여 달라는 요청
        - 파이썬으로 작성한 코드가 ORM에 의해 SQL로 변환되어 데이터 베이스에 전달되며 데이터 베이스의 응답 데이터를 ORM이 QuerySet이라는 자료 형태로 변환하여 전달
        - QuerySet
            - 데이터베이스에게서 전달 받은 객체 목록(데이터 모음)
            - Django ORm을 통해 만들어진 자료형
            - 데이터베이스가 단일한 객체를 반환 할 때는 QuerySet이 아닌 모델의 인스턴스로 반환된다.
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/426cfbc4-8f32-4424-b860-adc73b592174/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T000838Z&X-Amz-Expires=86400&X-Amz-Signature=714bd5f883135063a94e49581018bcfdaa4498da9b3d33fe0f70dfbb11d55a32&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
            
        

## QuerySet API Prac

- CURD
    - create(생성) / read(조회) / update(수정) / delete(삭제)
- Create
    1. article = Article()
        1. 클래스를 통한 인스턴스 생성
    2. article.title
        1. 클래스 변수명과 같은 이름의 인스턴스 변수를 생성 후 값 할당
    3. article.save()
        1. 인스턴스로 save 메서드 호출

```python
In [1]: article = Article()

In [2]: article.title = "Hello"

In [3]: article.content = "django! content!"

In [4]: article.save()
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3af55f1d-f593-490f-9dc2-f59672f9d061/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230321%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230321T000849Z&X-Amz-Expires=86400&X-Amz-Signature=3974472e9888446a8d580a70e3ddfaa1971e1d24064c9b3b6f8aa76f8075d925&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```python
In [5]: article = Article.objects.all()
In [7]: article
Out[7]: <QuerySet [<Article: Article object (1)>]>

In [8]: article[0]
Out[8]: <Article: Article object (1)>

In [9]: article[0].title
Out[9]: 'Hello'

In [10]: article[0].content
Out[10]: 'django! content!'
```

- Read
    1. Methods that “return new querysets”
    2. Methods that “do not return querysets”
    - all() : 전체 데이터 조회
    - get() : 단일 데이터 조회
        - 고유성을 보장하는 조회에서 사용해야 한다.
    - filter() : 지정된 조회 매개 변수와 일치하는 객체를 포함하는 새 QuerySet 반환
        - 조회된 객체가 없거나 1개여도 QuerySet을 반환
    - Field lookups
        - 특정 레코드에 대한 조건을 설정하는 방법
        - filter(), exclude(), get()에 대한 키워드 인자로 지정됨

- Update
    - save() 인스턴스 메서드 호출
- Delete
    - delete() 인스턴스 메서드 호출
    -