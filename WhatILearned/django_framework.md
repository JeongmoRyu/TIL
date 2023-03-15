# Django 웹 프레임워크 이해하기

## Framework

- 이미 많은 사람들이 만들어 놓은 코드들을 재사용해서 사용할 수 있다.
    - 개발 속도가 빠르다.
    - 체계적으로 만들 수 있다.(검증된 코드)
    - 생산성과 품질을 높임
- 이러한 코드들을 모아 놓은 것이 프레임 워크(FRAMEWORK)
    - 특정 프로그램을 개발하기 위한 여러 도구들과 규약을 제공하는 것
- 소프트웨어 프레임 워크는 복잡한 문제를 해결하거나 서술하는 데 사용되는 기본 개념 구조

## 클라이언트 - 서버 구조

- 오늘날 대부분 웹 서비스는 클라이언트-서버 구조를 기반으로 동작한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d0656006-4cd1-4691-9b64-687f996a890e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235252Z&X-Amz-Expires=86400&X-Amz-Signature=1688adf4fe05668a5e5b2763bc878c1dddacd23e6dbd7e35ff40b22462a5497b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 클라이언트
    - 웹 사용자의 인터넷에 연결된 장치
    - Chrome 또는 Firefox와 같은 웹 브라우저
    - 서비스를 요청하는 주체
- 주체
    - 웹 페이지, 사이트 또는 앱을 저장하는 컴퓨터
    - 클라이언트가 웹 페이지에 접근하려고 할 때 서버에서 클라이언트 컴퓨터로 웹 페이지 데이터를 응답해 사용자의 웹 브라우저에 표시됨
    - 요청에 대한 서비스를 응답하는 주체

<br/>

- 클라이언트 - 서버 구조
    - 클라이언트 : 홈페이지를 달라고 요청한 컴퓨터, 웹 브라우저
        - 자원(resource)를 달라고 요청
        - 자원을 해석하는 역할(랜더링) 수행
    - 서버 : 홈페이지 파일을 제공한 컴퓨터, 프로그램
        - 자원(resource)를 제공함

## 장고(Django) 시작!

```jsx
- $ pip install diango==3.2.18
버전을 정해서 인스톨하기
- $ django-admin startproject first_pjt
프로젝트 생성
- $ python manga.py runserver
서버실행
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2fbd0104-fffe-40c7-90f4-fee97f3d2de1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235311Z&X-Amz-Expires=86400&X-Amz-Signature=77c5ddb9144ba364495d3ad46e0a7ee5b6101c0ff71bb9f4959399166c55dd8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c2cd0b00-ec82-46e5-b704-d731315ea551/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235320Z&X-Amz-Expires=86400&X-Amz-Signature=e30a1992a1575480c331a9d310d43ad0f580c49b7468f2c6f6fb4d66362b19cd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e714636e-29df-4ec2-8cb2-d6eb7e497dd7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235328Z&X-Amz-Expires=86400&X-Amz-Signature=382a1741d98de330458dd05d6ed95fae6a39a60aec2cc640c92ed346f51d6684&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/878d6a85-b4d2-4b46-81bc-c272291416c6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235336Z&X-Amz-Expires=86400&X-Amz-Signature=d66bc41bc5e4e2bcffa3ef77d6a345c3ab11b46043136b98c8e4d71c1940a275&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

</br>

## 가상환경

- 패키지와 가상환경

```jsx
가상환경

- 가상환경 생성
	python -m venv venv

- 가상환경 활성화(ON)
	source venv/Scripts/activate

- 가상환경 비활성화(OFF)
	deactivate

- 가상환경 패키지 목록 저장
	pip freeze > requirements.txt

- 파일로부터 패키지 다운로드 받기
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1b1abbbf-bd6a-487c-8d3b-26e196b187db/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235356Z&X-Amz-Expires=86400&X-Amz-Signature=6b204fe645b54c6bebf629e132c0e243f456a563c7e6be3f2d550f9b27ddbbc3&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- Do practice make new server

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cb759c50-f8a4-4c5b-a8de-743b44b7b099/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235405Z&X-Amz-Expires=86400&X-Amz-Signature=35cbd7278865f7fb9a52c36b67ac4f365a14d9524cd3bd3e745649141a09a999&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## 프로젝트 구조

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c9f592bc-17bc-4b61-b1c5-47bc7fdc4e34/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235414Z&X-Amz-Expires=86400&X-Amz-Signature=282ddb14a9841c7ccd925bad5d253fb7541f2cdd8155429a720dbd7526ac1fa8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- init.py
- asgi.py
    - Asynchronous Server Gateway Interface
    - Django 어플리케이션이 비동기식 웹 서버와 연결 및 소통하는 것을 도운다.
- settings.py
    - Django 프로젝트 설정을 관리
- urls.py
    - 주소
- wsgi.py
    - Web Server Gateway Interface
    - Django 어플리케이션이 웹 서버와 연결 및 소통하는 것을 도운다.
- manage.py
    - 프로젝트와 다양하게 상호작용하는 커맨드라인

<br/>

- Django Application
    - 어플리케이션 생성
    
    ```jsx
    $ python manage.py startapp articles
    ```
    
- 앱(APP) : 하나의 큰 기능 단위

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aa5621a1-dca4-41aa-8cda-c8bc1dd75f3f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235427Z&X-Amz-Expires=86400&X-Amz-Signature=3370f58c129e623b781b7915a59905461a94fd58be00d9cf7654ccbb25999254&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- admin.py
    - 관리자용 페이지를 설정하는 곳
- apps.py
    - 앱의 정보가 작성되는 곳
    - 별도로 추가 코드를 작성하지 않음
- models.py
    - 어플리케이션에서 사용하는 Model을 정의하는 곳
    - MTV 패턴의 M에 해당
- test.py
    - 프로젝트의 테스트 코드를 작성하는 곳
- views.py
    - view 함수들의 정의되는 곳
    - MTV 패턴의 V에 해당

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

**중요**

앱을 사용하기 위해서는 

installed_apps 리스트에 반드시 articles를 넣어주어야 한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/47ce0da3-0c8f-485f-9fd5-cf5108dae669/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235441Z&X-Amz-Expires=86400&X-Amz-Signature=80de616536f55e0d498344689812a42e2d4aa866432ef0a7a2856baa9960e8e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

## Project & Application

- project
    - collecion of apps
    - 여러 앱들의 집합
- application
    - 실제 요청을 처리하고 페이지를 보여주는 등의 역할을 담당한다.
    - 하나의 역할과 기능 단위로 작성되는 것을 권장한다.
    

## 요청과 응답

Django = Model, View, Template

순서 : URL - View - Template 으로 제작하여 확인한다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/db289500-4f35-4c69-89a8-703aa13b4198/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235456Z&X-Amz-Expires=86400&X-Amz-Signature=9df871f6ae343eb214ec51e75e96ce080ee9c765d85e9d35b89d17eb7ec99dce&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d9e30dd2-3128-45c0-93cd-864f0d131423/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235504Z&X-Amz-Expires=86400&X-Amz-Signature=37758b64ecd96524a871880992cc39251d4ee20eed4c3d9eaebc41af4d19f965&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/224086a1-2818-419e-aa05-0d138e2faa6f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235514Z&X-Amz-Expires=86400&X-Amz-Signature=421e4830c03d47975947a694c227e8b23090609ea1be7267fc3355ae4a6ec685&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

주소창에 articles/를 넣고 들어가 본다면???

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8fbb1d9e-4195-48d5-bbdb-0903686725aa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230315%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230315T235523Z&X-Amz-Expires=86400&X-Amz-Signature=36c465f2ee6ed0d2a5e80149d6bf955f72253824b21591fb4e0484428493c60d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
