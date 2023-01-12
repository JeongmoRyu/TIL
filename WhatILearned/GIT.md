# Git의 정의

Linux 서버 os 

**분산 버전 관리 프로그램**

버전 - 컴퓨터 소프트웨어의 특정 상태

관리 - 어떤 일의 사무, 시설이나 물건의 유지 개량

프로그램 - 컴퓨터에서 실행될 때 특정 작업을 수행하는 일련의 명령어들의 모음

중앙 집중식 버전 관리에서 분산 버전 관리로 전환

 - 변경 사항에 대한 업데이트를 진행 

## **git**

코드의 **히스토리(버전**)을 관리하는 도구

개발되어온 **과정** 파악 가능

이전 버전과의 **변경 사항 비교 및 분석**

- 상태에 따라(변경사항을 기준으로) 관리해준다.
- 참여자들이 모든 소스 코드를 다 들고 있다.
- git 사용자의 방식에 따라, 회사의 정책에 따라 다르다.

- git vs gitub vs gitlab
```
- git  : 분산 관리 ‘프로그램’
- github : git을 활용해서 관리 사용하는 ‘서비스’
- gitlab : git을 활용해서 관리 사용하는 ‘서비스’
```

## GIT 활용

GUI vs CLI
---

**그래픽유저인터페이스(GUI)** - 이전의 활용, **그래픽**으로 상호작용

**CLI(Command LIne Interface)** - GIT Bash - git을 배우면서 컴퓨터와 **명령어**를 전달하는 방식



**Why CLI**
---

GUI는 사용하기 쉽지만 단계가 많고 컴퓨터의 성능을 더 소모

수 많은 서버/개발 시스템이 CLI를 통한 조작 환경을 제공




### 절대경로 VS 상대경로

---

절대 경로

- 루트 디렉토리부터 목적 지점까지 거치는모든 경로를 전부 작성한 것
- 윈도우 바탕 화면의 절대 경로 _ C:/Users/SSAFY/Desktop

상대 경로

- 현재 작업하고 있는 디렉토리를 기준으로 계산된 상대적 위치를 작성한 것
- 현재 작업하고 있는 디렉토리가 C:/Users일때 윈도우 바탕화면으로의 상대 경로는 ssafy/Desktop
- ./ : 현재 작업하고 있는 폴더
- ../ : 현재 작업하고 있는 폴더의 상위 폴더

## Repository

특정 디렉토리를 버전 관리하는 **저장소**

- **git init** 명령어로 로컬 저장소를 생성(보기 - 숨긴폴더보기)
- **.git** 디렉토리에 **버전 관리에 필요한 모든 것**이 들어있음

특정 버전으로 남긴다. = ‘커밋(commit)한다’


### git의 세가지 영역

1. 프로젝트의 일부가 아닌 것 ‘git add’ 
2. 프로젝트에 추가하고자 하는 것 ‘git commit’
3. 프로젝트에 추가된 것



### 새로운 주제

git add

git commit

git status

git log


## CLI 용어 설명



```
- -q! 문제시 돌아오기,  esc키, q
- ls : 폴더 내의 파일들을 보여준다
- ls -a : 숨긴 파일까지 다 보여준다.
- cd : (change direction)현재 폴더를 보여준다. ex)더블클릭
- cd .. : 이전 폴더로 돌아가기
- touch file_2.txt : 새로운 파일 만들기
- mkdir new_dir : 새 폴더 만들기
- rm : 삭제하기 ex)rm file_2.txt 파일 삭제(휴지통 x 바로 삭제)
- rm -r new_dir : 폴더 삭제
- clear : 빈 화면 만들기
- explorer : gui로 파일 탐색기 오픈
- explorer . : gui로 현재 폴더 위치 오픈
- ctrl + shift + P
- create new terminal
- + git bash
- add : 추가 ex)git add README.md
- git add
- git commit -m “add README.md”
- git commit -m “why this commit happened>”
- git config --global user.email “[you@example.com](mailto:you@example.com)”
- git config --global [user.name](http://user.name/)"Your Name"
- git status
- ‘git log’, ‘git log —oneline’
- shift + insert 붙여넣기
- git clone  프로젝트를 이제 관여하겠다.
- git push 인터넷에 올리기
- git pull 인터넷에서 당겨오기
```



