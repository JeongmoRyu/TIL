# HTTP URI

### HTTP

- HTTP 특징
    - stateless(무상태)
    - 동일한 연결에서 연속적으로 수행되는 두 요청 사이에 링크가 없음
    - 이를 해결하기 위해 쿠키와 세션을 사용해 서버 상태를 요청과 연결하도록 한다.
- HTTP Request Methods
    - GET, POST, PUT, DELETE
- HTTP reponse status codes
    - Informational responses (100-199)
    - Successful responses (200 - 299)
    - Redirection messages (300 - 399)
    - Client error responses (400 - 499)
    - Server error responses (500 - 599)

[HTTP Cats](https://http.cat/)

[HTTP DOGS - A dog for every HTTP Status Code](https://http.dog/)

### URI(자원의 식별자)

- Uniform Resource Identifier(통합 자원 식별자)
- 인터넷에서 리소스를 식별하는 문자열(일반적인 URI는 URL) **위치로 자원을 식별**
- 특정 이름 공간에서 이름으로 리소스를 식별하는 URI는 URN **이름으로 자원 식별**

### URL

- Uniform Resource Locator (통합 자원 위치)
- 웹에서 주어진 리소스의 주소
- URL 구조
    - Scheme (or protocol) : https
        - 브라우저가 리소스를 요청하는데 사용해야 하는 프로토콜
        - URL의 첫 부분은 브라우저가 어떤 규약을 사용하는지를 나타낸다. 다른 프로토콜도 존재한다.
            - mailto : 메일을 열기 위해
            - ftp: 파일 전송하기 위해
    - Authority
        - ://으로 구분된 패턴 (://www.naver.com/)
        - Domain Name
            - 요청 중인 웹 서버를 나타낸다.
            - 직접 IP 주소를 사용하는 것도 가능하다.
        - Port
            - 웹 서버의 리소스에 접근하는데 사용되는 기술적인 Gate
            - HTTP 표준포트는 생략이 가능하다.
                - HTTP - 80
                - HTTPS - 443
            - Django는 8000으로 잡혀있다.
        - Path
            - 웹 서버의 리소스 경로
            - 과거에는 물리적 위치 현재는 추상화된 형태의 구조를 표현
        - Parameters
            - 웹 서버에 제공하는 추가적인 데이터
            - & 기호로 구분되는 key-value 목록
            - 서버는 리소스를 응답하기 전에 이러한 파라미터를 사용하여 추가 작업을 수행할 수 있다.
        - Anchor
            - 리소소의 다른 부분에 대한 앵커
            - 부분 식별자 (fragment identifier) # 이후 부분은 서버에 전송되지는 않는다. 이를 통해 해당 지점으로 이동할 수 있다.
    

URN

- Uniform Resource Name (통합 자원 이름)
- URL과 달리 자원의 위치에 영향을 받지 않는 독립적인 이름 역할을 한다.
- URL의 단점을 극복하기 위해 자원이 어디에 위치한지 여부와 관계없이 이름만으로 자원을 식별하게 한다.
- 보편화되어 있지 않다.
    - ISBN (국제 표준 도서번호)
    - ISAN (국제 표준 시청각 자료 번호)