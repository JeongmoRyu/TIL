# vue state management

## State Management

- 상태(State) : 현재에 대한 정보(data)
- 현재 App이 가지고 있는 Data로 Web Application에서의 상태를 표현할 수 있다.

- Centralized Store
    - 중앙 저장소(store)에 데이터를 모아서 상태 관리
    - 각 Component는 중앙 저장소의 데이터를 사용한다.
    - 규모가 크거나 컴포넌트 중첩이 깊은 프로젝의 관리가 편리하다.

- Vuex(store)
    - 중앙 저장소를 통해 상태 관리를 할 수 있도록 하는 라이브러리
    - 데이터가 예측 가능한 방식으로만 변경될 수 있도록 하는 규칙을 설정하며 Vue의 반응성을 효율적으로 사용하는 상태 관리 기능을 제공한다.

```python
$ vue create vuex-app // Vue 프로젝트 생성
$ cd vuex-app
$ vue add vuex // Vue CLI를 통해 vuex plugin 적용
```