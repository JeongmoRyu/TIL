# WEB


- 웹 사이트는 웹 페이지의 모음
- 웹 페이지 구성요소
    - HTML, CSS, JavaScript
    - 구조, 표현(스타일링), 동작(인터렉션)
    - Web 주간 = HTML + CSS (구조(레이아웃)와 표현(스타일링))
- 추가 extention
    - live server
    - auto rename tag
    - highlight matching tag
    - emmet - 빠르게 작성하도록 도와주는 툴이다
        - visual studio code는 내장되어 있다.

## 개발 환경 설정

- Visual Studio Code
    - MS에서 제공하는 무료 텍스트 에디터

## HTML

- Hyper Text Markup Language
- Hyper Text(하이퍼 텍스트)
    - 참조(하이퍼 링크)를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
- Markup Language
    - 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어
        - HTML, Markdown
- 웹 페이지를 작성(구조화)하기 위한 언어
- .html : HTML 파일

## HTML 기본 구조

- html : 문서의 최상위(root) 요소
- head : 문서 메타데이터 요소
    - 문서제목, 인코딩, 스타일, 외부 파일 로딩 등
    - 일반적으로 브라우저에 나타나지 않는 내용
    - head의 예시

```
- <title> : 브라우저 상단 타이틀
- <link> : 외부 리소스 연결 요소 (CSS 파일 등)
- <style> : CSS 직접 작성
```

- body : 문서 본문 요소
    - 실제 화면 구성과 관련된 내용

### 요소(element)

```
- <h1>
    - <h1>contents<h1>
    - 여는 태그, 내용, 닫는 태그
- 내용이 없는 태그들
    - br : 줄바꿈 <br>, <br/>
    - hr, img, input, link, meta
    - 요소는 중첩될 수 있음
        - 요소의 중첩을 통해 하나의 문서를 구조화한다.
        - 태그의 쌍을 잘 확인해야 한다.
```

### 속성

```
- <a href=”https://google.com”></a>
- href : 속성명,  뒤에 나오는건 속성값
- 각 태그별로 사용할 수 있는 속성이 다르다.

- 속성을 통해 태그의 부가적인 정보를 설정할 수 있다.
- 속성을 가질 수 있으며 경로나 크기와 같은 추가적인 정보를 제공
- 요소의 시작 태그에 작성하며 보통 이름과 값이 하나의 쌍으로 존재
```

### HTML Global Attribute

- 모든 HTML 요소가 공통으로 사용할 수 있는 대표적인 속성
    - id : 문서 전체에서 유일한 고유 식별자 지정
    - class : 공백으로 구분된 해당 요소의 클래스의 목록
    - style : inline 스타일

- 주석필기
- <!— 주석 내용 —>

practice

```html
<!DOCTYPE html>
<html lang="en">
    <head>
    <meta charset="UTF-8" />
        <title>Document</title>
    </head>

    <body>
        <h1>Portfolio<h1>
        
        <h3>My name is Aiden<h3>

        <div>abcd1234</div>
        
        <a href="http://www.google.com/">Google</a>
        <a href="http://www.naver.com/">Naver</a>

    </body>

</html>
```


### 텍스트 요소
```
- <a></a> href 속성을 활용하여 다른 URL로 연결하는 하이퍼링크 생성
- <b></b> : 굵은 글씨 요소 강조
- <strong></strong> : 굵은 글씨 요소 강조
- <i></i> : 기울임 글씨 요소
- <em></em> : 기울임 글씨 요소
- <br> : 텍스트 내에 줄 바꿈 생성
- <img> : src 속성을 활용하여 이미지 표현
- <span></span> : 의미 없는 인라인 컨테이너
```


### 그룹 컨텐츠

<p></p> : 하나의 문단

<hr> : 주제를 분리하기 위한 수평선

<div></div> : 의미 없는 블록 레벨 컨테이너

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>Jeongmo Ryu</h1>
  
  <br>Hello!! My Friend!</br>

  <a href="http://google.com/">Goggle</a>
  <a href="http://naver.com/">Naver</a>
  <br/>
  새로운 Tab에 열 수 있는 링크<br/>
  <a href="http://naver.com/" target="_blank">NAVER</a>
  <br/>

</body>

</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/af14bdb1-bc9f-489b-bd1b-ab21c0ced7c1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230307T233911Z&X-Amz-Expires=86400&X-Amz-Signature=48d271093e3eef35a2d96dd364c7b8bda783619b9cb919146510101e7ea3d5bf&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### input

- input label
    - input : id속성을
    - label에는 for 속성을
- 일반적 유형
    - text : 일반 텍스트 입력
    - password : 입력 시 값이 보이지 않고 문자를 특수기호(*)로 표현
    - email : 이메일 형식이 아닌 경우 form 제출 불가
    - number : min, max, step 속성을 활용하여 숫자 범위 설정 가능
    - file : accept 속성을 활용하여 파일 타입 지정 가능
    - checkbox  : 다중 선택
    - radio : 단일 선택

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <header>
    <a href="http://google.com/">Google</a>
    <h1>건강설문</h1>
  </header>
  <section>
    <form>
      <label for="name">이름을 기재해주세요.</label>
      <input type="text" name="name" id="name">
      <hr>
      <label for="region">지역을 선택해주세요.</label> <br/>
      <select name="region" id="region" required>
        <option>서울</option>
        <option>대전</option>
        <option>광주</option>
        <option>구미</option>
        <option>부울경</option>
      </select>
      <hr>
      체온을 선택해주세요. <br/>
      <input type="radio" name="body-heat" id="normal">
        <label for="normal">37도 미만</label>  <br/>
      <input type="radio" name="body-heat" id="warn">
        <label for="warn">37도 이상</label> <br/>
      <hr>
      <input type="submit" value="제출">

    </form>
  </section>
  <footer>
    Google 설문지를 통해 비밀번호를 제출하지 마시오
  </footer>

</body>

</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bf31efe3-8eca-461c-9b09-bca832d314b0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230307T233838Z&X-Amz-Expires=86400&X-Amz-Signature=4b0a2fd61116325a9c80fe2cf10a6af6367452a218889959fd950c4b6f493bc8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)