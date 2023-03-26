# Django_authentication_and_authorization(인증과권한)

- Django authentication system
    - authentication and authorization 처리
    - 인증시스템
    - settings.py에 포함되어 있으며 installed_apps에서 확인 가능하다.
        - django.contrib.auth

## Authentication(인증)

- 신원 확인

## Authorization(권한, 허가)

- 권한 부여

## Substituting a custom User model

- Custom User Model로 대체하기
- AUTH_USER_MODE 설정 값으로 Default User Model을 재정의 할 수 있도록 한다.
    - AUTH_USER_MODE
        - 프로젝트에서 User를 나타낼 때 사용하는 모델

- settings.py

```jsx
AUTH_USER_MODEL = 'accounts.User'
```

- accounts/models.py

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

# Create your models here.
class User(AbstractUser):
    pass
```

- accounts/admin.py

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User
# Register your models here.

admin.site.register(User, UserAdmin)
```

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

- AUTH_USER_MODEL 변경하는 것은 모델 관계에 영향을 미치기 때문에 훨씬 더 어려운 작업이 필요하다.
- 프로젝트 처음에 진행해야한다!!
- 중간 변경은 자제하자!!

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

참고 : User 모델 상속 받는 형식

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cf257094-8c8b-45ba-be97-1b222fcd7644/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230326T034322Z&X-Amz-Expires=86400&X-Amz-Signature=35504c05afcbcbbbc2926d5ee86ddaf21523b25018989191486e746f07b04dcd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## 데이터 베이스 초기화

1. migrations 파일 삭제
    1. migrations 폴더 및 **Init**.py는 삭제하지 않는다.
    2. 번호있는 파일만 삭제하기
2. db.sqlite3삭제
3. migrations 진행
    1. makemigrations
    2. migrate

새로운 프로젝트를 시작하는 경우 커스텀 User 모델을 설정하는 것이 권장된다.
