# Jira

Issue Tracking Tools

Project management

Agile - 상황에 따라 유연하게 (형용사처럼 사용되고 있다.)

DevOps

## 방법론

- SCRUM
    - 이슈 해결 및 관리
    - sprint
    - 빠르게 끝내기 위해서 일어서서 meeting을 하거나 플랭크 하며 … ㅎㅎ

- KANBAN
    - 상태만 관리
    - WIP(work in progress)
        - 한 개인에게 할당량이 많을 시 다른 개인에게 할당해주는 방식

![image](https://hygger.io/guides/wp-content/uploads/2021/04/kanban-vs-scrum.jpg)

### SRE

- SRE - Site Reliability Engineering

## JQL

- JQL - Jira Query Language
- jira issue를 구조적으로 검색하기 위해 제공하는 언어
- SQL과 비슷한 문법
- Jira의 각 필드들에 맞는 특수한 예약어 들을 제공한다.
- 쌓인 Issue들을 재가공해 유의미한 데이터를 도출해 내는데 활용(Gadget, Agile Borad)

### JQL Operators

- =, ≠, >, ≥
- in, not in
- ~ (contain), !~(not contains)
- is empty, is not empty, is null, is not null

### JQL Keywords

- and, or, not, empty, null, order by (SQL과 유사)