# python foundamental point
- 확장자명 .py

“life is short, you need python”

컴퓨터 프로그래밍 언어

 - 컴퓨터에게 무언가를 시킬 때 쓰는 말

**파이썬**

1. 쉽다
2. 강력하다
3. 많은 사람들이 사용한다

## 자주 겪는 실수들

- 대/소문자
- 띄어쓰기
- 스펠링

+@ 순서대로 입력되기에 입력 순서도 확인해봐야 한다.

### python 문법

- 저장
    - 변수(Variable)
        - 숫자
        - 글자    ex) 숫자 30 vs 글자 ‘30’
        - 참/거짓 - 조건/반복에 사용된다. ex)True, False 단 두가지!!!
    - 리스트(List) - [] 대괄호를 넣어주면 된다.
        - 리스트는 순서 0부터 시작한다.
    - 딕셔너리(Dictionary) - ={}
        - 이름표를 가진 정보
- 조건
    - if, else
        - 만약 —면
        - —해줘
        - 아니라면
        - —해줘    ex) if, else
- 반복
    - elif
        - 만약 —이라면
        - —해줘
        - 그게 아니라 —이면
        - —해줘
        - 모두 아니라면
        - —해줘    ex) if, elif, else
    - while(종료 조건이 필요)
        - 만약 —이라면
        - 계속 —해줘
    - for (종료 조건이 필요없음)
        - —에 있는 —를 이용해서
        - —해줘   ex) for — in

- 함수
    - excel 함수
        - sum()
        - average()
        - count()
    - python 함수
        - built-in function(내장함수)
            - print(’hi’)
            - abs(-3) = 3
            - len(’hi’) = 2
        - non-built-in functions
- 모듈 - 함수나 변수 등을 모아 놓은 파이썬 파일

---

## 요청과 응답

- 클라이언트와 서버 간의 요청(URL)과 응답(JSON)

### JSON

- 데이터만을 주고 받기 위한 표기법
- 파이썬의 DIctionary와 List 구조로 쉽게 변환하여 활용 가능
- API의 응답으로 많이 이용

### API(Application Programming Interface)

- 두 소프트웨어가 서로 통신할 수 있도록 연결 시켜주는 인터페이스

### Request Library

- 파이썬에서 요청을 쉽게 보낼 수 있게 도와주는 모듈
- $ pip install requests(모듈 설치, 모듈 불러오기)
- ex) import requests
    
    request.get(’url’)
    
    request.get(’url’).json()