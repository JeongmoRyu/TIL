# web CSS Position

- 문서 상에서 요소의 위치를 지정
- static : 모든 태그의 기본 값(기준 위치)
    - 일반적인 요소의 배치 순서에 따름(좌측 상단)
    - 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치됨

- relative : 상대 위치
    - 자기 자신의 static 위치를 기준으로 이동 (normal flow 유지)
    - 레이아웃에서 요소가 차지하는 공간은 static 일 때와 같은 (normal position 대비 offset)
    - 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동가능
- absolute : 절대 위치
    - 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남)
    - static이 아닌 가장 가까이 있는 부모/조상 요소를 기준으로 이동(없는 경우 body)
    - 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동가능
- fixed : 고정 위치
    - 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남)
    - 부모 요소와 관계없이 viewport를 기준으로 이동
        - 스크롤 시에도 항상 같은 곳에 위치함
    - 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동가능
- sticky :  스크롤에 따라 static → fixed 로 변경된다.
    - 속성을 적용한 박스는 평소에 문서 안에서 position : static 상태와 같이 일반적인 흐름에 따르지만 스크롤 위치가 임계점에 이르면 postion : fixed와 같이 박스를 화면에 고정할 수 있는 속성
    - 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동가능

- 박스 만들기

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="html0308.css">
</head>

<body>

  <div>
    <div class="big">
      <div class="small" id="red"></div>
      <div class="small" id="gold"></div>
      <div class="small" id="green"></div>
      <div class="small" id="blue"></div>
      <div class="small" id="pink"></div>
    </div>

  </div>
  
</body>
</html>
```

```css
.box {
  width: 100px;
  height: 100px;
}

.big {
  position: relative;
  margin: 100px auto 500px;
  border: 5px solid black;
  width: 500px;
  height: 500px;

}

.small {
  width: 100px;
  height: 100px;

}

#red {
  background-color: red;
  position: absolute;
  top: 400px;
  left: 400px;
}

#gold {
  background-color: gold;
}

#green {
  background-color: green;
}

#blue {
  background-color: blue;
}

#pink {
  background-color: pink;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a8239fb7-12f0-4ede-af24-492f9e1606ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T153430Z&X-Amz-Expires=86400&X-Amz-Signature=3a939fc8cd514e09cf800ea27c63a964293a467c567ddf4300824d2ea4622310&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.box {
  width: 100px;
  height: 100px;
}

.big {
  position: relative;
  margin: 100px auto 500px;
  border: 5px solid black;
  width: 500px;
  height: 500px;

}

.small {
  width: 100px;
  height: 100px;

}

#red {
  background-color: red;
  position: absolute;
  top: 400px;
  left: 400px;
}

#gold {
  background-color: gold;
  position: fixed;
  bottom: 50px;
  right: 50px;
}

#green {
  background-color: green;
  position:absolute;
  top: 200px;
  left: 200px;
}

#blue {
  background-color: blue;
  position: relative;
  top: 100px;
  left: 100px;
}

#pink {
  background-color: pink;
  position: absolute;
  top: 0px;
  left: 0px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e7c6ff74-74d0-4e29-a189-4f33c8fd21e5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T153443Z&X-Amz-Expires=86400&X-Amz-Signature=29531048221ee39edde64e9dd6bcab3c15b3f50aec9eb8ba6b32d108cfcff545&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## WEB

### layout - Float

- css 원칙1
    - 모든 요소는 네모박스이고 위에서부터 아래로 왼쪽에서 오른쪽으로 쌓인다.

- 박스를 왼쪽 오른쪽으로 이동시켜 텍스트를 포함 인라인 요소들 주변을 wrapping하도록 한다.
- 요소가 Normal flow를 벗어나도록 함

- 속성
    - none : 기본값
    - left : 요소를 왼쪽으로 띄움
    - right :  요소를 오른쪽으로 띄움

- Float는 레이아웃을 구성하기 위해 필수적으로 활용되었으나, FLEXBOX, GRID 와 함께 사용도가 낮아졌다.
- Float 활용 전략 - Normal Flow에서 벗어난 레이아수 구성
    - 원하는 요소들을 float로 지정하여 배치

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="html0309.css">
</head>
<body>
  <div class="container">
    <div class="box"></div>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Neque officiis excepturi quos aut enim corporis consequuntur hic perferendis repellendus vitae magnam, cumque et, vero delectus eum soluta molestias ullam ad!  Lorem ipsum dolor sit amet consectetur adipisicing elit. A nostrum doloremque dolorum consectetur odit at, perspiciatis eius! Pariatur, sit molestiae ex vel, minus quibusdam veniam quo similique nihil vero aut?</p>

  </div>

</body>
</html>
```

```css
.box {
  width: 100px;
  height: 100px;
  background-color: beige;

  float: left;
  margin-right: 20px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/64ead57c-6e71-4ee6-9e36-37d0f539720f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T153456Z&X-Amz-Expires=86400&X-Amz-Signature=e87e4b84ec563914c64b080beb2bd5c2ec89c25ed45f7dd192f607b0c503b607&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

→ html에서 lorem은 의미 없는 문자들을 넣어두는 방법입니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="html0309.css">
</head>
<body>
  <div class="container">
    <div class="box1 left"></div>
    <div class="box1 box2 left"></div>
    
  </div>

</body>
</html>
```

```css
.box1 {
  width: 100px;
  height: 100px;
  background-color: beige;
  border: 1px solid black;
}

.box2 {
  background-color: blue;
  
}

.left {
  float: left;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c714e252-e2ec-4bf0-930a-af2b767d7c42/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T153514Z&X-Amz-Expires=86400&X-Amz-Signature=e4dc1feb1eb23b41ebaf53c5c61a3a3036242ab3fce6c0e2be175d9be285c1f8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

→ 이러한 방식으로 layout을 많이 잡는다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="layout.css">
</head>
<body>
  <div class="container">
    <div class="header"></div>
    <div class="section-l left"></div>
    <div class="section-r left"></div>
    <div class="footer"></div>

  </div>
</body>
</html>
```

```css
.header {
  height: 100px;
  background-color: cadetblue;
}
.section-l {
  height: 500px;
  background-color: violet;
  width: 40%;
}

.section-r {
  height: 500px;
  background-color: aqua;
  width: 60%;
}

.footer {
  height: 100px;
  background-color: yellow;
  clear: both;

}

.left {
 float: left;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/73215366-d1b7-48f0-88e0-a90f154de22f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T153527Z&X-Amz-Expires=86400&X-Amz-Signature=923011234771b9734ede13a759ca09adf2c670b18836ea4b124a55e07759fc4e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)