# web css

## CSS

- Cascading Style Sheets
- 스타일을 지정하기 위한 언어

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bd780204-7aa9-460a-8b7b-0f2cdfa7dfba/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230308T235233Z&X-Amz-Expires=86400&X-Amz-Signature=95312812fe25f98eb60305665542613c285134f391a8ff5828e6a4b34f05cad0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 속성(Property) : 어떤 스타일 기능을 변경할지 결정
- 값(Value) : 어떻게 스타일 기능을 변경할지 결정

### CSS  정의 방법

```
- inline(인라인)
    - <h1 style=”color: blue; font-size: 100px;”>Helo</h1>
- <style> :  내부 참조
```

```jsx
<style>
	hi{
		color:blue;
		font-size: 100px;
	}
</style>
```

```
color: 

- 외부참조(link file) : 분리된 CSS 파일
    - <link rel=”stylesheet” href=”style.css”>
```

### CSS with 개발자 도구

- styles : 해당 요소에 선언된 모든 CSS
- computed : 해당 요소에 최종 계산된 CSS

## CSS Selectors
<br/>

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f170a272-7708-4b3c-9aa8-0f13490a7389/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230308T235323Z&X-Amz-Expires=86400&X-Amz-Signature=56317eac3398df2a3983d62d50c8ee468f11fd77ed9b2167df222a8a03976a16&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
<br/>

### 선택자 유형

- 기본 선택자
    - 전체 선택자(*)
    - 요소(tag) 선택자 : HTML 태그를 직접 선택
    - 클랙스(class) 선택자 : 마침표(.)문자로 시작하며, 해당 클래스가 적용된 항목을 선택
    - 아이디(id) 선택자 : # 문자로 시작하며, 해당 아이디가 적용된 항목을 선택, 일반적으로 1번만 사용(사용 권장)
    - 속성(attr) 선택자
- 결합자(Combinators)
    - 자손 결합자, 자식 결합자

### 적용 우선순위

- CSS 우선순위를 아래와 같이 그룹 지을 수 있다.
    1. 중요도(Importance) - 사용시 주의해야한다.
        1. !important
    2. 우선 순위(Specificity) 중요!!!!
        1. **인라인 > id > class, 속성 > 요소**
        2. 우선 순위가 같다면 나중에 한 것으로 적용된다. 
<br/>
<br/>
## CSS 상속

- 상속을 통해 부모 요소의 소성을 자식에게 상속한다.
    - 속성(프로퍼터) 중에서 상속이 되는 것과 되지 않는 것들이 있다.
        - 상속되는 것
            - text 관련 요소(font, color, text-align)
            - opacity
            - visibility
        - 상속되지 않는 것
            - Box model 관련 요소(width, height, margin, padding, borader, box-sizing, display)
            - position 관련 요소(position, top/right/bottom/left, z-index)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    h2 {
      color: orange;
      font_size: xx-large;
      font-weight: 800

    }
  </style>
  <link rel="stylesheet" href="styles.css"> 
</head>
<body>
  <h1>Hello emmet</h1>
  <h2>emmet is easy</h2>
  <h3>Oh my God!</h3>
  <p>this is a paragraph</p>
  <div></div>
  <a href="http://google.com/">Google</a>
  <p>Lorem ispsum dolor sit, amet <span>consectetur</span> adipisicing elit. Ratione, soulta manam mol</p>

  <form action="">
    <input type="text"><br>
    <input type="password" name="password" id="password"><br>
    <input type="submit" value="제출">
  </form>

</body>
</html>
```
<br/>

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/056424e0-5d4b-4167-88e3-3696d9556f5d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230308T235512Z&X-Amz-Expires=86400&X-Amz-Signature=0dac960bd4242262b90821a285b022dc61282de4f4cdaafe48cbfc04b3d4602f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

게임으로 연습하기<br/>
32단계 게임하며 CSS정복하기

[https://flukeout.github.io/](https://flukeout.github.io/)
<br/>
### CSS Box model

- 모든 요소는 네모(박스모델)이고, 위에서부터 아래로, 왼쪽에서 오른쪽으로 쌓인다.
- 하나의 박스는 4가지 영역으로 이루어져있다.
    - content
    - padding
    - border
    - margin
    - 숫자들이 여러 개일 경우 상하좌우 순서대로

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1e0ce219-d7f5-4ac4-bc2e-6593aad93daa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230308T235529Z&X-Amz-Expires=86400&X-Amz-Signature=bca38fea192c048907e9c46172b20ba634c7cecaf2aacd0c8eba4b20a493325e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
<br/>
```html

<!-- 숫자들이 여러개일 경우 상하좌우 순서대로 -->
.margin{
	margin-top:10px;
	margin-right:20px;
	margin-bottom:30px;
	margin-left:40px;
}

.margin-padding{
	margin:10px;
	padding:30px;
}

.border{
	border-width:2px;
	border-style:dashed;
	border-color:black;
}

<!-- 요소들은 shorthand로 쓸 수도 있다. -->

.border{
	border:2px dashed black;
}

```
<br/>

- box-sizing
    - 일반적으로 box-sizing은 content-box
        - padding을 제외한 순수 contents 영역 만을 box로 지정
    - 하지만 border까지의 너비를 보길 원한다.
        - 이러한 경우에는 box-sizing을 border-box로 설정한다.
<br/>

## 개발자 도구

- 크롬 개발자 도구
    - 웹 브라우저 크롬에서 제공하는 개발과 관련된 다양한 기능을 제공
    - 주요기능
        - Elements - DOM 탐색 및 CSS 확인 및 변경(해당 요소의 HTML 태그)
            - Styles - 요소에 적용된 CSS 확인
            - Computed - 스타일이 계산된 최종 결과
            - Event Listeners - 해당 요소에 적용된 이벤트(JS)
        - Sources, Network, Performance, Application, Security, Audits
<br/>
- 학습 가이드라인<br/>

    - MDN web docs<br/>
        - https://developer.mozilla.org/ko/

    - 개발자 도구 활용법<br/>
        - https://developer.chrome.com/docs/devtools/css/