# Mapreduce

![image](https://i.stack.imgur.com/199Q1.png)

map reduce 함수를 바탕으로 여러 머신들을 통해 word를 count를 할 수 있게 되었다.

## Map Reduce

- Mapper and Reducer
    - 각 머신에서 독립적으로 수행
    - mapper는 map 함수를 reducer는 reduce 함수를 각각 수행
- Combine functions
    - 각 머신에서 map 함수가 끝난 다음에 reduce 함수가 하는 일을 부분적으로 수행한다.
    - 셔플링 비용한 네트웍 트레픽을 감소시킨다.
- Mapper와 Reducer가 필요하다면 setup() and cleanup()를 수행할 수 있다.
    - setup() - 첫 map함수나 reduce 함수가 호출되기 전에 먼저 수행한다.
        - 파라미터들 정보를 main함수에서 받아오는데 사용
        - 자료구조를 초기화하는데 사용
    - cleanup() - 마지막 map 함수나 reduce 함수가 끝나고 나면 수행
        - 결과 출력
- mapreduce job을 수행할 때에 map phase만 수행하고 중단 가능
