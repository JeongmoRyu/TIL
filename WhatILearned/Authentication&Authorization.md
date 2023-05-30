# Authentication&Authorization

## Authentication

- 인증, 입증
- 모든 보안 프로세스의 첫 번째 단계
    - 가장 기본적인 요소
- 401 Unauthorized
    - HTTP 표준에서는 미승인을 명확히 하고 있지만 의미상 이 응답은 비인증을 의미한다.

## Authorization

- 권한 부여, 허가
- 사용자에게 특정 리소스 또는 기능에 대한 액세스 권한을 부여하는 과정 : 절차
- 보안 환경에서 권한 부여는 한상 인증이 먼저 필요하다
    - 사용자는 조직에 대한 액세스 권한을 부여 받기 전에 먼저 자신의 ID가 진짜인지 확인해야한다.
- 서류의 등급, 제한 구역 등 웹 페이지에서 글을 조회, 삭제, 수정 할 수 있는 방법
- 403 Foridden
    - 401과 차이점은 서버가 클라이언트가 누구인지 알 수 있다는 점

## Authentication & Authorization

- 회원가입 후 로그인 시 서비스를 이용할 수 있는 권한 생성
    - 인증 이후에 권한이 따라오는 경우가 많다.
- 인증을 다 거치더라도 권한이 동일하게 부여되는 것은 아니다.
    - ex) 로그인을 하더라도 다른 사람들의 글과 컨탠츠를 수정, 삭제가 가능한 것은 아니다.
- 세션, 토큰, 제 3자를 활용하는 등의 다양한 인증 방식이 존재한다.

## Authentication determined

- 인증 여부 확인 방법
- REST_FRAMEWORK에서 DEFAULT_AUTHENTICATION_CLASSES
- settings.py에서 작성하는 설정
    - DRF가 기본으로 제공해주는 인증 방식 중 하나인 **TokenAuthentication**
- view 함수, 각 요청 마다 다른 인증 방식으로 설정하려면 decorator를 활용한다.
    
    ```python
    - @authentication_classes([SessionAuthentication, BasicAuthentication])
    - @permission_classes([IsAuthenticated])
    ```
    

- BasicAuthentication
    - 가장 기본적인 수준의 인증 방식
    - 테스트하기에 적합하다.
- SessionAuthentication
    - Django에서 사용했던 session기반의 인증 시스템
    - DRF와 Django의 session 인증 방식은 보안적 측면을 구성하는 방법에 차이가 있다.
- RemoteUserAuthentication
    - Django의 Remote user 방식을 사용할 때 활용하는 인증 방식
- TokenAuthentication
    - 간단히 구현 가능하다
    - 기본적인 보안 기능을 제공한다.
    - 다양한 외부 패키지를 사용할 수 있다.

## dj-rest-Auth

- dj-rest-auth

```python
$ pip install dj-rest-auth

installed_apps에 
'rest_framework.authtoken',
'dj_rest_auth', 추가

urls.py에
path('accounts/', include('dj_rest_auth.urls')) 추가
```

- registration

```python
$ pip install 'dj-rest-auth[with_social]'
설치하기

urls.py에
path('accounts/signup/', include('dj_rest_auth.registration.urls'))
```