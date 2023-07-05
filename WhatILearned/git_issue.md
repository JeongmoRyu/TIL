# Git issue 관리

## 순서

issue start(open) →  make new branch → issue solve → commit(with issue number) →merge at master → close issue (delete branch)

## New Issue

- github - issue - New issue
- title, write
- Projects
    - 해당 Projects 불러오기
- Labels
    - bug, documentation, duplicate, enhancement, good first issue, help wanted  등
    - custom
- milestone
    - 사전에 issue 탭에서 milestone를 만들어서 적용할 수 있다.
- Submit new issue

## Make new branch **with issue name**

이슈 생성시 나온 번호를 기반으로 브렌치를 생성합니다

```jsx
git checkout -b issue_num
```

## Issue solved

## Commit & Push

```jsx
git add .
git commit
i
issue_num
우리가 이슈가 발생하였다.
이슈를 해결하였다.

esc - :wq로 저장

git push origin issue_num
```

## Merge at master

```jsx
git checkout master
git merge issue_num
git push origin master
```

### After Issue

- 이슈 닫기
- 브렌치 제거

