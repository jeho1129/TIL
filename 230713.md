# <center>TIL<center>
## 2023/07/13(1일차)

# 오늘 배운 내용 :memo:

1. **Markdown**
   - **Heading**
     - ```#의 개수에 따라 제목의 수준을 구별```   
     - ```#의 개수가 적을 수록 제목의 크기가 커진다```
    - **Code Block**
      - ```python 
        print('hello')
        ```
      - 일반 텍스트와 달리 해당 프로그래밍 언어에 맞춰서 텍스트 스타일을 변환
      - 개발에서 마크다운을 사용하는 가장 큰 이유이다.
---
2. **git**(분산 버전 관리 시스템)
    1. **git의 구성 요소**
    </br>- Working Directory
      - 실제 작업 중인 파일들이 위치하는 영역
    - Staging Area
      - Working Directory에서 변경된 파일 중, 다음 버전에 포함시킬 파일들을 선택적으로 추가하거나 제외할 수 있는 중간 준비 영역
    - Repository
      - 버전(commit) 이력과 파일들이 영구적으로 저장되는 영역
        - commit : 변경된 파일들을 저장하는 행위
  
    2. **git의 동작**
    ```</br>
    git init : 로컬 저장소 설정(로컬 저장소 내에 또 다른 git 로컬 저장소를 만들지 말 것)
    ```
    ```</br>
    git add : 변경 사항이 있는 파일을 staging area에 추가
    ```
    ```</br>
    git add . : 변경 사항이 있는 폴더 내 모든 파일을 staging area에 추가
    ```
    ```</br>
    git commit : staging area에 있는 파일들을 저장소에 기록
    ```
    ```</br>
    git status : 로컬 저장소의 파일 상태 확인
    ```
    ```</br>
    git log : 로컬 저장소의 파일 상태 확인
    ```
    ```</br>
    git remote add origin(원격 저장소 별칭) remote_repo_url : 로컬 저장소에 원격 저장소 주소 추가
    ```
    ```</br>
    git remote -v : 추가된 원격 저장소 목록 확인
    ```
    ```</br>
    git push : 원격 저장소에 commit 목록을 업로드
    ```
    ```</br>
    git pull : 원격 저장소의 변경 사항을 받아옴
    ```
    ```</br>
    git clone remote_repo_url : 원격 저장소 전체를 복제(clone으로 받은 프로젝트는 이미 git init이 되어있다.)
    ```
    ```</br>
    gitignore : Git에서 특정 파일이나 디렉토리를 추적하지 않도록 설정하는 데 사용하는 텍스트 파일(프로젝트에 따라 공유하지 않아야 하는 것들도 존재하기에...)
    ```