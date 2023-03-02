# APS (Algorithm Problem Solving) 1

## Complexity metric

- 개념

```
[IT용어] 시스템이나 시스템 구성요소(component) 또는 소프트웨어 프로그램의 복잡도 (complexity)를 측정(measurement)하는 측정 체계(metric)
시스템을 어느 정도의 수준까지 시험해야 하는지 또는 시스템을 개발하는데 어느 정도의 노력을 소요해야하는지를 결정하는 근거를 제공한다.
복잡도 메트릭을 통해 시스템(구성요소)의 복잡도를 측정한 결과 복잡도가 높은 경우, 일반적으로 많은 장애가 유발될 가능성이 크므로 보다 정밀한 시험을 통해 내재된 오류를 사전에 제거하여야 한다.
일반적으로 복잡도 메트릭은 시스템 구성요소의 크기를 제어하는 논리의 복잡도 조합으로 볼 수 있다. 복잡도를 측정하는 표준적인 방법에는 LOC(line of code), 맥케이브 복잡도 메트릭(McCabe"s complexity metrics), 핼스테드 메트릭(Halstead"s metrics) 등이 있다.
"NAVER"
```


- 알고리즘의 효율
    - 공간적 효율성과 시간적 효율성
        - 공간적 효율성 : 연산량 대비 얼마나 적은 메모리 공간을 차지하는가
        - 시간적 효율성 : 연산량 대비 얼마나 적은 시간을 요하는 가
        - 효율성 == 복잡도
    - 복잡도의 표기
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1a1f7d39-5a08-4c04-8c68-6bf28fa36da4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230301T234001Z&X-Amz-Expires=86400&X-Amz-Signature=cda22e1d0b2118e0dbb845171ff1511e00334c433aa705b8cddb660752020f4d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
- Big-Oh
    - 점근적 상한
    - 단순화된 표현 n**2
    - 최고차항만 계수 없이
- Big-Omega
    - 점근적 하한
    - 최소한의 시간을 표현할 때 사용
    - 최고차항만 계수 없이
- Big-Theta
    - Big_Oh와 Big-Omega 표기가 같을 때 사용
- 다양한 표현들

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/adca1cdf-d35b-4c20-b422-5fe623e287b2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230301%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230301T233946Z&X-Amz-Expires=86400&X-Amz-Signature=4f094e4c5bcc2460aaa587448f94033b79a0b2a8207e96a36396f65daea87a71&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
