# Front-end_Development


- Front-end 개발은 Web App 또는 Web site의 UI/UX를 제작하고 관리하는 과정
- 프레임워크와 라이브러리(React, Angular, Vue.js)를 사용하여 개발 효율성을 높이고 Web app의 복잡성을 관리한다.
- Front-end 개발에 사용되는 주요 기술은 HTML, CSS, JavaScript

## SPA(Single Page Application)

- 사용자의 요청에 대해 적절한 페이지 별 template을 반환한다.
- 서버에서 최초 1장의 HTML 만 전달 받아 요청에 대응하는 방식
    - CRS(Client Side Rendering) 방식으로 요청을 처리하기 때문에 가능하다.
    - + SSR(Server Side Rendering)
        - 기존의 방식은 SSR
        - Server에 사용자의 요청에 적합한 HTML을 렌더링하여 제공하는 방식

### CRS(Client Side Rendering)

- 최초의 한 장 HTML을 받아온다.
    - 빈 문서의 html 문서
- 각 요청에 대한 대응을 JavaScript를 사용하여 필요한 부분만 다시 렌더링한다.
    1. 필요한 페이지를 서버에 AJAX로 요청한다.
    2. 서버는 화면을 보여주기 위해 데이터를 JSON 방식으로 전달한다.
    3. JSON 데이터를 JavaScript로 처리, DOM 트리에 반영한다.
- CRS 방식을 사용하면 HTML 페이지를 서버로부터 바아서 표시하지 않아도된다.
    - 트래픽 감소 → 응답 속도가 빨라진다.
- 필요한 부분만 고쳐 나가기에 각 요청이 끊김없이 진행된다.
    - UX 향상 : 자연스러운 진행
- BE와 FE의 작업 영역을 명확히 분리 할 수 있다.
    - 협업이 용이해진다.

### CRS의 단점

- 검색 엔진 최적화(SEO, Search Engine Optimization)이 어렵다.
    - 서버가 제공하는 것은 빈 html
    - 내용을 채우는 것은 AJAX 요청으로 얻은 JSON 데이터로 클라이언트가 진행된다.
- 대체적으로 HTML에 작성된 내용을 기반으로 하는 검색 엔진에 빈 HTML을 공유하는 SPA 서비스가 노출되기 어렵다.
- CSR SSR를 분리하기 보다는 점점 SPA 서비스에서도 SSR을 지원하는 Framework가 발전하고 있다.
    - Vue의 Nuxt.js
    - React의 Next.js
    - Angular의 Universal