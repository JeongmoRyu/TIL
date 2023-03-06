# Computer Thinking


- 프로그래밍의 어려운 점 두 가지
    - 프로그래밍 언어 문법과 라이브러리 사용
    - 논리 (Hard Logic)
- 문법과 라이브러리

### Hard vs Soft Logic

- 문제를 풀 때는 직관을 사용한 것
- 직관의 장점 : 익숙한 상황에서 빠르다
    - 일상생활에서 Soft Logic을 사용한다.
- 직관의 단점 : 정확하지 않다, 강한 착각을 일으킨다.
    - 프로그래밍 언어의 표현들이 모두 논리학에서 나왔다.

## 명제

- 참이나 거짓을 알 수 있는 식이나 문장
- 진리값 T, F         1,0

### 연산(결합)

- 부정 NOT
    - p가 명제일 때 진리값이 반대
- 논리곱 AND
    - p, q가 명제일 때, p, q 모두 참일 때만 참이 되는 명제
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3210a5cd-b519-489b-bdb8-a0a067955f43/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231441Z&X-Amz-Expires=86400&X-Amz-Signature=98e682cb47b0d2c3986d522d20af688e92e3ba945ab9612c28661ad00c616218&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
- 논리합 OR
    - p, q가 명제일 때, p, q 모두 거짓일 때만 거짓이 되는 명제
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/09972f42-edf9-448d-9cad-91025d5dfe4f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231450Z&X-Amz-Expires=86400&X-Amz-Signature=71fea20d71279b9d950918224a84c66a0603b8058b601a7d1613e452044acae4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
- 배타적 논리합 XOR
    - p, q가 명제일 때, p, q 중 하나만 참일 떄 참이 되는 명제
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1601620b-76de-4246-8591-a7b0e85259a4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231505Z&X-Amz-Expires=86400&X-Amz-Signature=bf2456d89b9fdb411f4732e9d2be26343d26e5003fa9f108ccba345fa12988bb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    

### 합성

- 연산자 우선순위

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e352460-6cf7-4ac1-b5cd-44061d37b146/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231518Z&X-Amz-Expires=86400&X-Amz-Signature=308718ed2c4ca3d74453828ab3a96fc5263b161754e7811386a1f18a939f6e1d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

항진명제 : 진릿값이 항상 참

모순명제 : 진릿값이 항상 거짓

사건 명제 : 항진명제도 모순명제도 아닌 명제

- 조건명제
    
    p → q
    
- 쌍방조건명제
    
    p ↔ q
    
- 조건 명제의 역, 이, 대우

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4d97efe7-6217-4c3f-983c-ed02d1b45386/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231529Z&X-Amz-Expires=86400&X-Amz-Signature=a9d02e007a2d86ebcd898b396f67f3532b86003037ed16890d8f11f1fa6fb136&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### Practice

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/10d82549-d684-41cd-8308-cc7b2feac693/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231609Z&X-Amz-Expires=86400&X-Amz-Signature=a3eb8620bf7660d01dd9b7c9d92e155e843fbb99653230d5e919ab094bd4074a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/078f196a-cea3-4d04-904a-808532c31d3d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231618Z&X-Amz-Expires=86400&X-Amz-Signature=13d97a99edf6d314cc2ccfd0998a15015c60e88440e9613ae804a42a54d8c86b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/64e190e5-7797-457d-a4f8-947ac86c4cff/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230306%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230306T231627Z&X-Amz-Expires=86400&X-Amz-Signature=140dadad4402432b304c48e5fa2c3b7a915ab4530d6d17386f47582a69beca49&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)