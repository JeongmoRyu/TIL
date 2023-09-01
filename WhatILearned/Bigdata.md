# Bigdata

- 병렬 분산 시스템과 맵리듀스 프레임워크 이해
- 하둡을 이용하여 여러 빅데이터 분석 문제들에 대해 아록리즘을 자바 언어로 구현하고 실행

![image](http://wiki.hash.kr/images/thumb/4/46/BigData_2267x1146_white.png/750px-BigData_2267x1146_white.png)

## 용어

- scale-out
    - 값싼 서버들을 이용함
    - 데이터 중심 어플리케이션 분야에서 값싼 서버들을 많이 이용하는 것을 선호함
- scale-up
    - 적은 수의 값비싼 서버들을 이욯함
    - 가격의 관점에서 선형으로 성능이 증가하지 않는다.
- 데이터 중심 프로세싱(Data-intensive processing)
    - 한대의 컴퓨터의 능력으로 처리가 어려움
    - 많은 수의 컴퓨터를 묶어서 처리해야함
    - 맵리듀스 프레임 워크가 하는 것
- 맵리듀스는 빅데이터를 이용한 효율적인 계산이 가능한 첫 번째 프로그래밍 모델
    - 기존에 존재하는 여러 가지 다른 병렬 컴퓨팅 방법에서는 프로그래머가 낮은 레벨의 시스템 세부 내용까지 많은 시간을 쏟아야만 한다.

## MapReduce Framework

- 빅 데이터를 이용하는 응용분야에서 주목 중
- 스케일러블 병렬 소프트웨어의 구현 쉽게 할 수 있도록 도와주는 간단한 프로그래밍 모델
- 구글의 맵리듀스 또는 오픈소스인 하둡은 맵리듀스 프레임워크의 우수한 구현의 형태
- 드라이버에 해당하는 메인 함수가 map 함수와 reduce 함수를 호출해서 처리

- 맵리듀스 프레임워크에서 각각의 레코드 또는 튜플은 키-벨류 쌍으로 표현된다.
- main 함수를 한개의 마스터 머신에서 수행하는데 이를 수행하기 전에 전처리하거나 리듀스 함수의 후처리하는데 사용할 수 있다.
- 컴퓨팅 : 맵과 리듀스의 쌍으로 이루어진 맵리듀스 페이지를 한번 수행하거나 여러 번 반복해서 수행할 수 있다.
    - 경우에 따라서 컴바인 함수를 중간헤 수행할 수 있다.

## MapReduce Phase(3단계)

- Map phase
    - 제일 먼저 수행되며 데이터의 여러 파티션에 병렬 분산으로 호출되어 수행된다.
    - 각 머신마다 수행된 mappe는 맵 함수가 입력 데이터의 한 줄 마다 map 함수를 호출한다.
    - map 함수는 key value 쌍으로 결과를 출력하고 여러 머신에 나누어 보내며 같은 key를 가진 key value 쌍을 같은 머신으로 보낸다.
- Shuffling Phase
    - map phase가 끝나면 시작된다.
    - 각각의 머신으로 보내진 쌍들을 key를 이용하여 sort한 다음 각 쌍을 모아 value-list를 만든 다음에 여러 머신에 분산해서 보낸다.
- Reduce Phase
    - 모든 머신에서 셔플링 페이즈가 다 끝나면 각 머신마다 리듀스 페이즈가 시작된다.
    - 각각의 머신에서 shuffling phase에서 해단 머신으로 보내진 key value 쌍 마다 reduce 함수가 호출되며 하나의 reduce 함수가 끝나면 다음 함수가 호출된다.
    - 출력이 있다면 key value 쌍으로 출력된다.

## Hadoop

- Apache 프로젝트의 맵리듀스 프레임워크의 오픈 소스
- 하둡 분산 파일 시스템(HDFS)
    - 빅 데이터 파일을 여러 대의 컴퓨터에 나누어서 저장
    - 각 파일은 여러 개의 순차적인 블록으로 저장
    - 하나의 파일의 각각의 블록은 fault tolerance를 위해서 여러 개로 복사되어 여러 머신에 저장됨
        - 일부 결함이 있어도 정장적, 부분적으로 기능 수행할 수 있도록 하는 것
    - 빅 데이터를 병렬 처리하기 위해 분산함(scale out)

### 주요 구성 요소

- MapReduce - 소프트웨어 수행 분산
- Hadoop Distributed File System(HDFS) - 데이터 분산
- Namenode  - 파일 시스템을 관리하고 클라이언트가 파일에 접근 가능하도록 함
- Datanode - 컴퓨터에 들어있는 데이터를 접근할 수 있도록 함

## MapReduce 함수

- Map 함수
    - org.apache.hadoop.mapreduce라는 패키지에 있는 mapper 클래스를 상속받아 mapq method를 수정한다.
    - 입력 텍스트 파일에서 라인 단위로 호출되고 입력은 key, value
    - key - 맵 함수가 호출된 해당 라인의 첫 번째 문자까지의 offset
    - value - 텍스트의 해당 라인 전체
- Reduce 함수
    - org.apache.hadoop.mapreduce라는 패키지에 있는 Reduce 클래스를 상속받아 reduce method를 수정한다.
    - suffling phase의 출력을 입력으로 받는데 key value 형태
- Combine 함수
    - reduce 함수와 유사한 함수이지만 각 머신에서 map phase의 출력 크기를 줄여 sufffling phase와 reduce phase의 비용을 줄여주는데 사용
