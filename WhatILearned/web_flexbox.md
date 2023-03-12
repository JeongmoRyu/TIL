# web_flexbox

## FLEXBOX

- layout에 특화된 기능을 보유하고있다.
- CSS Flexible Box Layout
    - 수직 정렬
    - 아이템의 너비와 높이 혹은 간격을 동일하게 배치
- CSS Flexible Box Layout
    - 행과 열 형태로 아이템들을 배치하는 1차원 레이아웃 모델
        - 축
            - main axis (메인 축)
            - cross axis (교차 축)
        - 구성 요소
            - Flex Container (부모 요소)
            - Flex Item (자식 요소)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d6f3789a-f0e4-47fb-b8b7-222744a13539/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004827Z&X-Amz-Expires=86400&X-Amz-Signature=d455dcf936dbf3061907ef0ce15653b2ad8e29da881ad087d5ff57d2a1fe7e63&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="flexbox.css">
</head>
<body>
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>

  </div>
</body>
</html>
```

```css
.container {

  display: flex;

}

.item {
  width: 100px;
  height: 100px;
  background-color: black;

  margin-top: 20px;
  margin-right: 20px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/69ad189c-193d-4a6c-afab-739a62514f36/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004836Z&X-Amz-Expires=86400&X-Amz-Signature=1a6808b9707f8187f1842d6a87fdd862bb9e5f7c1884036a7b672e6920affa76&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

→ flex창이 생긴다.

- Flexbox 축
    - flex-direction : row
        - 아이템이 쌓이는 방향이 메인이다.

- Flexbox 구성요소
    - Flex Container(부모요소)
        - flexbox 레이 아웃을 형성하는 가장 기본적인 모델
        - Flex item들이 놓여있는 영역
        - display 속성을 flex 혹은 inline-flex로 지정
    - Flex Item (자식 요소)
        - 컨테이너에 속해있는 컨텐츠(박스)

### Flex 속성

- 배치 설정
    - flex-direction
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b83baaa3-cee8-49cf-b3cb-8e79a2a20db6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004854Z&X-Amz-Expires=86400&X-Amz-Signature=2a35517dd8e13bc335a79ed43cc495e013019de81353ff0a93e1ca39cf3bec96&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - flex-wrap
        - 아이템이 컨테이너를 벗어나는 경우 해당 영역 내에 배치되도록 설정
        - 줄 넘김이라고 생각하면 된다.
            - wrap : 넘기면 다음줄로 배치
            - no-wrap : 한줄에 배치

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5d9d62c5-8b60-4d9e-91b7-0d07f2434e13/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004904Z&X-Amz-Expires=86400&X-Amz-Signature=62382c2a3ab1c9a5b39954ed934cea5ece6f5d7e4a50e205cdc369f0ee452107&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 공간 나누기
    - justify-content (main axis)
        - Main axis 기준으로 공간 배분
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a102cdec-e173-4be3-ab8a-98771a7fbb54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004913Z&X-Amz-Expires=86400&X-Amz-Signature=5cd8002c999fdb2180e5204e68ce03627976be6995c62aaee2d6bd207990aabc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - align-content (cross axis)
        - Cross axis를 기준으로 공간 배분

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c66b00a-39d8-47cb-ad87-06cf0457a259/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004922Z&X-Amz-Expires=86400&X-Amz-Signature=4bba1d0d0f24447e2b7e4389c2bad8a28a27264a2f1a7cb1c5efebf99c44462d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 정렬
    - align-items (모든 아이템을 cross axis 기준으로)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3a397959-8b35-441c-8f4e-d83fc349d1c9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004931Z&X-Amz-Expires=86400&X-Amz-Signature=9c24b1c8ce53946bf06d8fb03792c97d68b23c8fe0f32deeb4454fb470fb3d1b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - align-self (개별 아이템)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/378f3105-c4d2-4dcc-8a0d-7a2f339c1dd4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004941Z&X-Amz-Expires=86400&X-Amz-Signature=c0053f569bb9b87d77ce77b9366455f84a39302c608908890343410fd51fa4a4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- practice

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="flexbox.css">
</head>
<body>
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>

  </div>
</body>
</html>
```

```css
.container {

  display: flex;
  flex-direction: row-reverse;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bf3a23b3-f071-4459-8ec0-d93e43d0b418/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T004951Z&X-Amz-Expires=86400&X-Amz-Signature=24c579f8e5315b97e09159f77485f185f915b012ea2c94d1044b7ae482f5b269&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {

  display: flex
	flex-direction: column;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c6c8cc25-9c3a-4612-823a-6dd67debe4dd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005002Z&X-Amz-Expires=86400&X-Amz-Signature=a311b314f08d4bb48dce99dcd92209f65d9ad7a812d6a4938d1be190bfc22ea4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/288e891f-9f6a-40ba-ab77-754a6f4ecb9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005012Z&X-Amz-Expires=86400&X-Amz-Signature=b2dc7dd269a791d6ad8367e167bd06b761f664d1536c6107e6981c6d61b053e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

→ reverse랑 착각하지말자

```css
.container {

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/25d70a26-5d54-4147-8fb2-96538d4b78b2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005022Z&X-Amz-Expires=86400&X-Amz-Signature=6dcc91d49cb91e26432aaeae3d2f009a4ab33790105389d2f844236789e74a3c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

→ 간격 일정하게

```css
.container {

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

→ 주위를 둘러쌓 부분이 일정하게

```css
.container {

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-evnely;

}

.item {
  width: 100px;
  height: 100px;
  background-color: rgb(158, 142, 142);

  margin-top: 20px;
  margin-right: 20px;

  font-size: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/545c2125-fe00-488f-bbc0-afc9b90ff762/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005031Z&X-Amz-Expires=86400&X-Amz-Signature=ed89816f956b0269f55946a4deef3dafd52f1b98b21d81d66e0512cdeb92534a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- align practice

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="align.css">
</head>
<body>
  <div class="container">
    <div class="item">one</div>
    <div class="item">two</div>
    <div class="item">three</div>
    <div class="item">four</div>

  </div>
  
</body>
</html>
```

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;

  align-items: stretch;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c0ebfea-2300-4815-b816-4b192f3f93e5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005050Z&X-Amz-Expires=86400&X-Amz-Signature=3e4006d3389316feee795807d3fd4c9c5ffdd843332c6e95a1747376f75b72e5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;

  align-items: flex-start;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0044c520-240a-4b5a-abda-e1ddef663845/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005059Z&X-Amz-Expires=86400&X-Amz-Signature=c3d3e7c4568c485b7d7fc45815a8f41acaff337ffccab4b833c5f85edac2bb2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;

  align-items: flex-end;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/02c34d34-9022-4f56-8f24-7cd344631fff/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005110Z&X-Amz-Expires=86400&X-Amz-Signature=7848da2d2d5f548cc55af61c29aba407df16f4b552282ecd88f3ece4e81ae195&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;

  align-items: center;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e1704f3c-9924-419b-a294-dda8a79ee2b2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005126Z&X-Amz-Expires=86400&X-Amz-Signature=2229293d436a69f201e18da131dc4df59dbb99c61afa98c882199b116a90c942&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;

  align-items: baseline;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6542ea56-3a44-4c30-a75f-369dc6021c15/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005200Z&X-Amz-Expires=86400&X-Amz-Signature=31b486243e535724d3d9950eb074fcf093a550520ade6e19a910a0c4de036478&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/de664f41-b5b5-4032-abff-ef2e6f81dba1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005210Z&X-Amz-Expires=86400&X-Amz-Signature=93790e732cc42395abe3e1bbfa4d99d01d75199279f278ff9a10a7d08182beb9&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- order를 통한 순서 바꾸기

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="align.css">
</head>
<body>
  <div class="container">
    <div class="item order3">one</div>
    <div class="item order1">two</div>
    <div class="item order4">three</div>
    <div class="item order2">four</div>

  </div>
  
</body>
</html>
```

```css
.container {
  background-color: rgb(252, 219, 219);
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.item {
  background-color: bisque;
  border: 1px solid black;
  font-size: 20px;
  margin-right: 5px;

}

.order1 {
  order: 1;
}
.order2 {
  order: 2;
}
.order3 {
  order: 3;
}
.order4 {
  order: 4;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2db9f31c-f4fe-47f8-ace5-3fb41ce7e361/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005222Z&X-Amz-Expires=86400&X-Amz-Signature=cb0fed5585dc89f3c5a269eedb51c802f0123f0c6b0a109a3c8e55744cf8b02d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 늘어나는 비율 조절하기
    - flex-grow  ↔ shrimp 도 존재한다.

- 개구리 보내기 게임
- flexbox froggy

[https://flexboxfroggy.com/#ko](https://flexboxfroggy.com/#ko)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9df36242-edd0-4adb-ae3b-3bfe65004310/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005232Z&X-Amz-Expires=86400&X-Amz-Signature=a5e288987cce166499ffb3c337bd5ee92d1c55af76e96c8fcbd115f0766f3d7f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/83f73587-5867-4828-b4eb-a775e51efc5b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005248Z&X-Amz-Expires=86400&X-Amz-Signature=094b71a012ea250ad0658dee978566e8c51fac4666e32291b50a4733a3ef76b1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fd80b75a-32ba-4d64-83ec-759251c1f1cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005308Z&X-Amz-Expires=86400&X-Amz-Signature=f3a6879f756cf1cf251f167c99a94c3c0a6f0a8d192cf9f2e5570a7083023bcf&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5c53ed3e-8158-4b99-9fb8-d2566d2781d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230312T005320Z&X-Amz-Expires=86400&X-Amz-Signature=5863eff2ef089fe2d79a66539013bcda352d1eaacb124f494258ef3283423ef1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)