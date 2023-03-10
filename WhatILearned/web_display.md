# WEB CSS Display


- display에 따라 크기와 배치가 달라진다.

## display

- display: block
    - 줄 바꿈이 일어나는 요소 (다른 elem을 밀어낸다.)
    - 화면 크기 전체의 가로 폭을 차지한다.
    - 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
- display: inline
    - 줄 바꿈이 일어나지 않는 행의 일부 요소
    - content를 마크업하고 있는 만큼만 가로 폭을 차지한다.
    - width, height, margin-top, margin-bottom을 지정할 수 없다.
    - 상하 여백은 line-height로 지정한다.
- display: inline-block
    - block과 inline 레벨 요소의 특징을 모두 가짐
    - inline처럼 한 줄에 표시 가능하고, block 처럼 width, height, margin 속성을 모두 지정할 수 있다.
- display: none
    - 해당 요소를 화면에 표시하지 않고, 공간조차 부여되지 않음
    - 이와 비슷한 visibility : hidden 해당요소가 공간은 차지하나 화면에 표시되지 않는다.
<br/>

## 블록 레벨 요소와 인라인 레벨 요소

- 블록 레벨 요소와 인라인 레벨 요소 구분
- 대표적 블록 레벨 요소
    - div / ul, ol, li / p / hr / form
- 대표적 인라인 레벨 요소
    - span / a / img / input, label / b, em, i, strong<br/>

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
  <div class="box"></div>  
  <div class="box"></div>  
</body>
</html>
```
<br/>

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  margin-top: 20px;

}
```
<br/>


![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c542e01b-e52b-42db-9950-9b3b645cb698/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T003908Z&X-Amz-Expires=86400&X-Amz-Signature=e1445c5e5e76f353d39e28f878b6c84a4aad1afe8348ffc4d1bbf9fdd09fcf45&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br/>

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  /* margin-top: 20px;
  margin-right: auto;
  margin-left: auto; */
  margin: 20px auto;

}
```
<br/>

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9eb0450a-2225-4c12-b9cd-6695c6d4fef6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T003917Z&X-Amz-Expires=86400&X-Amz-Signature=d8bfc19716f824db9aa723b71fd371195b70e6d2555e62c7f7fc2db7d44c04b0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
<br/>
<br/>

- 글자 입력하기

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
  <div class="box">
    <span>div</span>
  </div>  
  <div class="box">
    <span>div</span>
  </div>  
</body>
</html>
```

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  /* margin-top: 20px;
  margin-right: auto;
  margin-left: auto; */
  margin: 20px auto;

  text-align: center;

}
```
<br/>

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bb776e73-0898-498a-8b36-9036feae9f92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T003934Z&X-Amz-Expires=86400&X-Amz-Signature=57cb1a2eefee103a60ee955ffab987d63786381ea951ba42cfbb6df108cec1e8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  /* margin-top: 20px;
  margin-right: auto;
  margin-left: auto; */
  margin: 20px auto;

  text-align: center;

}

span {
  line-height: 100px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1701815d-90ea-4586-bce7-62dca8ebb7af/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T003948Z&X-Amz-Expires=86400&X-Amz-Signature=776f0586853b7e050e19eb3107c49fc7873d5c7fc06b194f1066155aacd572fc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
<br/>
<br/>


- none

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
  <div class="box test">
    <span>1</span>
  </div>  
  <div class="box">
    <span>2</span>
  </div>  
</body>
</html>
```

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  /* margin-top: 20px;
  margin-right: auto;
  margin-left: auto; */
  margin: 20px auto;

  text-align: center;

}

span {
  line-height: 100px;
}

.test {
  display:none;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a7ed14e6-90d3-4e9d-ab71-d0d86637a425/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T003959Z&X-Amz-Expires=86400&X-Amz-Signature=f09d53c49497f6cc0b5c8d09cddd9c95f22eb84f028e67b19f545989384afcc6&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br/>
<br/>

- visibility : hidden

```css
.box{
  background-color: aquamarine;
  height: 100px;
  width: 100px;

  /* margin-top: 20px;
  margin-right: auto;
  margin-left: auto; */
  margin: 20px auto;

  text-align: center;

}

span {
  line-height: 100px;
}

.test {
  visibility: hidden;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/199e2113-ee8f-48a7-9da5-b8dd4ad20794/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T004010Z&X-Amz-Expires=86400&X-Amz-Signature=0b13470964f9a96641edf7aeea2c1e2e1621671e9183b0e18111e12c26770e3d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

