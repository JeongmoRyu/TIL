# web bootstrap

- 꿀팁!!!
    - alt 하고 커서 클릭하면 다중 커서가 된다.

- 원이랑 사각형 만들기

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="start.css">
</head>
<body>
  <div class="circle darkgreen"></div>
  <div class="circle red lg"></div>
  <div class="circle blue"></div>
  <div class="rect red sm"></div>
  <div class="rect blue"></div>
  <div class="rect red lg"></div>
</body>
</html>
```

```css
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}

.rect {
  width: 100px;
  height: 100px;
}

.darkgreen {
  background-color: darkgreen;

}
.red {
  background-color: red;
}
.blue {
  background-color: blue;
}
.lg {
  width: 150px;
  height: 150px;
}
.sm {
  width: 50px;
  height: 50px;
}
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e876dca6-d518-4927-b493-7b7b5bf2c230/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142712Z&X-Amz-Expires=86400&X-Amz-Signature=47a2681fb1d7f239ba001f9dfe26356868cbda1cb8eb4582ed388b680310dcfb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## Bootstrap

- bootstrap 시작하기
    - 장점들이 너무 많다.

```jsx
- head 앞에
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">

- bodt 마지막 앞에
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
```

### CDN

- Content Delivery(Distribution) Network
    - 컨텐츠(CSS, JS, Image, Text 등)를 효율적으로 전달하기 위해 여러 노드를 가진 네트워크에서 데이터를 제공하는 시스템
    - 개발 end-user의 가까운 서버를 통해 빠르게 전달 가능하고 서버의 부하가 적어진다.
    
- spacing
    - .mt-1
    - 0.25rem
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f484af09-2ad8-4318-bdbb-cada660a2d28/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142727Z&X-Amz-Expires=86400&X-Amz-Signature=d7e283b62f84108bd9546b9d6270177d8676229c44df9419f2ffd366c1653c41&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - .mx-auto
        - 자동 수평 중앙 정렬

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/77a02f90-d2a6-4630-aa57-20dc2f62e514/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142736Z&X-Amz-Expires=86400&X-Amz-Signature=45ff9ac03c26d88950c7cc1a89f42b1724e907bfa6bb0a16b47587982ad5ddb4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a04337f7-7a92-4854-94d8-e9024cb9bea0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142747Z&X-Amz-Expires=86400&X-Amz-Signature=16f3fafef2ece4d4af2ee0d423147b880e47038cbfe60889729b3b917024cf06&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- practice

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap.css">
</head>
<body>
  
  <div class="box mx-0"></div>
  <div class="box mt-2"></div>
  <div class="box mt-3"></div>
  <div class="box mt-4"></div>
  <div class="box mt-5"></div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/03596aee-3066-484d-ab3b-32dab15d1f14/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142759Z&X-Amz-Expires=86400&X-Amz-Signature=9982697f9be80d6b583df764d89bddbf3184d6b2060ae7574bbaf162bc96c08d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 색 넣어주기

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/098ca1fb-e443-49ac-852a-70d5ce8b4374/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142813Z&X-Amz-Expires=86400&X-Amz-Signature=adf716737a7ecfacfa2da06036e6d678beca3132e05847ef93cbbecc264b71c9&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap.css">
</head>
<body>
  
  <div class="box mx-0"></div>
  <div class="box mt-2 bg-primary"></div>
  <div class="box mt-3 bg-success"></div>
  <div class="box mt-4 bg-danger"></div>
  <div class="box mt-5 bg-warning"></div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/179cd863-7c12-41aa-9c49-4c52c1d64eb6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142829Z&X-Amz-Expires=86400&X-Amz-Signature=a7d7666a04dfe532ebca6a620c543d324b7542c87185640d062871c75350759a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap.css">
</head>
<body>
  
  <div class="box mx-0"></div>
  <div class="box mt-2 mx-auto bg-primary"></div>
  <div class="box mt-3 bg-success"></div>
  <div class="box mt-4 ms-auto bg-danger"></div>
  <div class="box mt-5 bg-warning"></div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/951c65ce-738b-4b6c-aeb5-617884f97941/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142842Z&X-Amz-Expires=86400&X-Amz-Signature=6be0740d9eee1b690ad6de2fb92d16c57ebaa3c2010a29090afa841394a1897b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- margin-collapse 현상
    - 마진이 겹치는 현상을 말한다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap.css">
</head>
<body>
  
  <div class="box mx-0"></div>
  <div class="box mt-2 mx-auto bg-primary"></div>
  <div class="box mt-3 bg-success"></div>
  <div class="box mt-4 ms-auto bg-danger"></div>
  <div class="box mb-5 mt-5 bg-warning"></div>
  <div class="box mt-3"></div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6bfb5602-a46e-4853-96bb-89e32305d3f9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142856Z&X-Amz-Expires=86400&X-Amz-Signature=fad04fec7c884c885102e3bde26451133f78cc39d543d4dae8e93b8626673232&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 문자도 크기와 색을 넣어줄 수 있다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap2.css">
</head>
<body>
  <p class="text-start text-sucess fs-1">one</p>
  <p class="text-center text-danger fs-2">two</p>
  <p class="text-end fs-3">three</p>
  <p class="text-center text-warning fs-4">four</p>
  <p class="text-start text-secondary fs-5">five</p>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/88e69b02-a4e9-47f8-b36d-b9854f796c99/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142906Z&X-Amz-Expires=86400&X-Amz-Signature=e28bde11e9a97bfeaa054dce0b6af180a10e4fef8a690d190493637ae204a572&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 공식문서를 참조해보면
- 이메일이나 카카오톡처럼도 만들어줄 수 있다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap2.css">
</head>
<body>
  <div class="box mt-3"></div>
  <button type="button" class="btn btn-primary position-relative">
    Mails <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-secondary">+99 <span class="visually-hidden">unread messages</span></span>
  </button>
  
  <div class="position-relative py-2 px-4 text-bg-dark border border-dark rounded-pill">
    Marker <svg width="1em" height="1em" viewBox="0 0 16 16" class="position-absolute top-100 start-50 translate-middle mt-1" fill="var(--bs-dark)" xmlns="http://www.w3.org/2000/svg"><path d="M7.247 11.14L2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z"/></svg>
  </div>
  
  <button type="button" class="btn btn-primary position-relative">
    Alerts <span class="position-absolute top-0 start-100 translate-middle badge border border-light rounded-circle bg-danger p-2"><span class="visually-hidden">unread messages</span></span>
  </button>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f6c045b9-af8d-4c0e-8581-3b2f0a75670a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142921Z&X-Amz-Expires=86400&X-Amz-Signature=ad02e26f642c5f7e04859ca4a087f6acf809b392fa328cdad1bdd4fdd19a2e47&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- components
    - 미리 완성되어 있는 기능들을 사용할 수 있다.
    
    대박!!!!!!
    
    - carousel
    - card
    - flex도 있다.
        - justify, align 모두 다 사용도 가능하다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <link rel="stylesheet" href="bootstrap2.css">
</head>
<body>
  <div class="d-flex flex-row mb-3 bg-light">
    <div class="p-2 bg-secondary text-white">Flex item 1</div>
    <div class="p-2 bg-secondary text-white">Flex item 2</div>
    <div class="p-2 bg-secondary text-white">Flex item 3</div>
  </div>
  <div class="d-flex flex-row-reverse bg-light">
    <div class="p-2 bg-warning text-white">Flex item 1</div>
    <div class="p-2 bg-warning text-white">Flex item 2</div>
    <div class="p-2 bg-warning text-white">Flex item 3</div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/53291bdd-3e61-41f7-af57-07bde94fb760/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142933Z&X-Amz-Expires=86400&X-Amz-Signature=e67bb8d45e3fa4041d0ca1930ea6813df40105cbecb6cf8475478579fbead522&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- Respeonsive Web DEsign(반응형 웹 구현하기)
    - 웹이 크기에 따라 변경되는 웹
    - Media Queries, Flexbox, Bootstrap Grid System, The viewport meta tag
    

### Bootstrap Grid System

- The Grid System
    - CSS가 아닌 편집 디자인에서 나온 개념으로 구성 요소를 잘 배치해서 시각적으로 좋은 결과물을 만들기 위함
    - 오와 열을 맞춘다.
    - 정보 구조와 배열을 체계적으로 작성하여 정보의 질서를 부여하는 시스템
- Web에서도 요소들의 디자인과 배치에 도움을 주는 시스템
    - Column : 실제 컨텐츠를 포함하는 부분
    - Gutter : 칼럼과 칼럼 사이의 공간 (사이간격)
    - Container : Column들을 담고 있는 공간

- Bootstrap Grid System
    - 12개의 column
    - 6개의 grid breakpoints

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">

</head>
<body>
  <div class="container">
    <div class="row">
      <div class="col-2 bg-secondary">first</div>
      <div class="col-4 bg-warning">second</div>
      <div class="col-4 bg-success">third</div>
      <div class="col-2 bg-danger">fourth</div>

    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2d2ff3c6-b9d4-4078-b56d-830c856b3155/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142947Z&X-Amz-Expires=86400&X-Amz-Signature=b5f06eafdcf733ad45fe97911eceb89a6bf13474f13697d897771954c0e823c2&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 특정 사이즈 밑으로 내려가면 변화되게
    - sm 사이즈 이상일 때는 옆의 숫자 사이즈가 되고
    - 그 미만일 경우에는 옆의 숫자가 없는 것과 마찬가지로 된다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e433ffcc-0411-4951-a1d6-a564a6bf58f4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T142956Z&X-Amz-Expires=86400&X-Amz-Signature=431259e687401ff1445ac4393647c46916f345ae7d0dd8ce7d44c2dbfbc9e831&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">

</head>
<body>
  <div class="container">
    <div class="row">
      <div class="col-sm-2 bg-secondary">first</div>
      <div class="col-sm-4 bg-warning">second</div>
      <div class="col-sm-4 bg-success">third</div>
      <div class="col-sm-2 bg-danger">fourth</div>

    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
</body>
</html>
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2d2ff3c6-b9d4-4078-b56d-830c856b3155/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T143012Z&X-Amz-Expires=86400&X-Amz-Signature=a214643ff9570972d304f264a4cae2dca7a329ad27fce3837d3815e2bacdbda0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6018f4df-bb6a-472f-bc7c-d8268f6f516c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230313T143019Z&X-Amz-Expires=86400&X-Amz-Signature=9b1d02ac563614bed4c8c2afcd421bd6c13bc41277bce584bd048d18733684a5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)