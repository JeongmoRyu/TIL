# 가상 환경 만들기

## 장점
- 협업을 하는 과정에서 컴퓨터 환경에서의 차이로 인하여 문제 발생을 막기 위해서 가상환경을 만든다.

## Do Practice

ignore 만들기

- touch .gitignore
- .gitignore 파일을 직접 만들어도 된다.

mkdir xxxxxx

- 폴더 만들기

python -m venv venv

- 가상 환경 venv 폴더 만들기

source venv/Scripts/activate

- 가상 환경으로 만들기

pip install 패키지 명

- 패키지를 설치한다

pip freeze > requirements.txt

- 가상 환경 목록 .txt로 만들기

pip install -r requirements.txt

- txt의 목록을 설치하기




