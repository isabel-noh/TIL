# Git Advanced
## Git undoing
### git restore 
- Working directory 작업 단계
    - Working directory에서 수정한 파일을 수정 전 `(직전 commit)`으로 되돌리기 
    - 이미 버전 관리가 되고 있는 파일만 되돌리기 가능 
    - git restore을 통해 되돌리면, 해당 내용을 복원할 수 없으니 주의! 
    - `git restore {file_name}`
    - [참고] git 2.23.0 version이전에는 'git checkout -- {file_name}'

```shell
# Git 저장소 초기화
git init 
# test.md 파일 생성 후 커밋
touch test.md
git add .
git commit -m '1st'
# git log 확인
git log --oneline
# Working Directory에서 test.md 파일 수정
vi test.md
# git restore을 사용해서 test.md 파일을 수정 전으로 되돌리기
git restore test.md
```

## Staging Area 작업 단계 되돌리기
Staging Area에 반영된 파일을 working Directory로 되돌리기(==unstage)  
root-commit 여부에 따라 두가지 명령어로 나뉨
- root-commit이 있는 경우: `git rm --cached`
- root-commit이 없는 경우: `git restore --staged`

### git rm --cached
```shell
# git 저장소 초기화
git init
# test.md 파일 생성 후 add
touch test.md
git add test.md
# git status 확인
git status
# unstaging
git rm --cached
# git status 확인
# git status >>> untracked files
```

### git restore --staged
```shell
git init

touch test.md
git add .
git commit -m '1st'


```

## Repository 작업 단계 되돌리기
### git commit --amend
`git commit --amend`  
- 커밋을 완료한 파일을 Staging Area로 되돌리기
- Staging Area에 새로 올라온 내용이 없다면, 직전 커밋의 메시지만 수정
    - 커밋 메시지가 변경되며 .....
- Staging Area에 새로 올라온 내용이 있다면, 직전 커밋을 덮어쓰기

#### 커밋을 완료한 파일을 Staging Area로 되돌리기
- Staging Area에 새로 올라온 내용이 없다면, 직전 커밋의 메시지만 수정
```shell
# git 저장소 초기화
git init
# test.md 파일 생성 후 커밋
touch test.md
git add .
git commit -m '1st commit'
#  git commit --amend를 사용해서 직전 커밋의 메시지만 수정하기
git commit --amend 
# 내용 수정~ :wq
# git log확인
git log 
```
- Staging Area에 새로 올라온 내용이 있다면, 직전 커밋을 덮어쓰기
```shell
# git 저장소 초기화
git init
# test.md 파일 생성 후 커밋
touch test.md
git add .
git commit -m '1st commit'
# 직전 커밋에 누락된 file을 Staging Area에 반영하기
git commit --amend
# // 커밋 내용수정
# git commit --amend를 사용하여 직전 커밋을 덮어쓰기
```

## Git reset
특정 커밋으로 되돌아갔을 때, 해당 커밋 이후로 쌓았던 커밋들은 전부 사라짐  
### `git reset [options] {commit_id}`  
- 옵션은 soft, mixed, hard 중 하나를 작성  
- commit_id는 되돌아가고싶은 시점의 커밋 ID를 작성

### git reset의 세가지 options
- `--soft`
    - 해당 커밋으로 되돌아가고
    - 되돌아간 커밋 이후의 파일들을 Staging Area로 돌려놓음
- `--mixed`
    - 해당 커밋으로 되돌아가고
    - 되돌아간 커밋 이후의 파일들을 Working Directory로 돌려놓음
    - git reset의 default value
- `--hard`
    - 해당 커밋으로 되돌아가고
    - 되돌아간 커밋 이후의 파일들은 모두 Working Directory에서 삭제 -> **사용 주의**
    - 기존의 Untracked files는 사라지지 않고 Untracked로 남아있음

##### [참고]git reflog
- git reset의 hard옵션은 Working Directory 내용까지 삭제하므로 위험할 수 있음
- git reflog 명령어를 이용하면 reset하기 전의 과거 커밋 내용을 모두 조회할 수 있음
- 이후 해당 커밋으로 reset하면 hard 옵션으로 삭제된 파일도 복구 가능

```shell
# 실습 전 환경 세팅 
# soft 폴더에서 git reset --soft {commit_id}
# mixed 폴더에서 git reset --mixed {commit_id}
# hard 폴더에서 git reset --hard {commit_id}
```

## Git revert
- git reset과의 차이점
    1. reset은 커밋 내역을 삭제하는 반면, revert는 새로운 커밋을 생성함
    2. revert는 github을 이용하여 협업할 때     



## Git branch
Branch브랜치는 여러 개로 작업공간을 나누어 독립적으로 작업할 수 있도록 도와주는 Git 도구  
- 브랜치는 독립 공간을 형성하기 때문에 master 원본에 대해 안전함
- 하나의 작업은 하나의 브랜치로 나누어 진행되므로 체계적인 개발이 가능함
- Git은 브랜치를 만드는 속도가 굉장히 빠르고, 적은 용량을 소모함

### git branch
> master branch : 상용 버젼  

브랜치 조회, 생성, 삭제와 관련된 Git 명령어
- 조회
    - git branch : 로컬 저장소의 브랜치 목록 확인
    - git branch -r : 원격 저장소의 브랜치 목록 확인
- 생성
    - git branch {branch_name} : 새로운 브랜치 생성
    - git branch {branch_name} {commit_id} : 특정 커밋 기준으로 브랜치 생성
- 삭제 
    - git branch -d {branch_name} : 병합된 브랜치만 삭제 가능
    - git branch -D {branch_name} : 강제 삭제

### git switch
현재 브랜치에서 다른 브랜치로 이동하는 명령어  
- git switch {branch_name} : 다른 브랜치로 이동
- git switch -c {branch_name} : 브랜치를 새로 생성 및 이동
- git switch -c {branch_name} {commit_id} : 특정 커밋 기준으로 브랜치 생성 및 이동
- **switch하기 전에 해당 브랜치의 변경 사항을 반드시 커밋해야함!!**
    - 다른 브랜치에서 파일을 만들고 커밋을 하지 않은 상에서 switch하게 되면 브랜치를 이동했음에도 불구하고 해당 파일이 그대로 남아있게 됨

##### [참고] HEAD
This is a `pointer` to the `local branch` you're currently on.  
HEAD는 현재 브랜치를 가리키고, 각 브랜치는 자신의 최신 커밋을 .... .... . .. . . .. ! 
- git switch는 현재 브랜치에서 다른 브랜치로 HEAD를 이동시키는 명령어 
```cmd
(master) $ git branch hotfix(branch_name)
```

## git merge
분기된 브랜치들을 하나로 합치는 명령어  
master branch가 상용이므로, 주로 master브랜치에 병합  
- `git merge {합칠_branch_name}` 
    - 병합하기 전에 브랜치를 합치려고 하는, 즉 main 브랜치로 switch해야함 
    - ... .... 


### fast-forward
마치 빨리감기처럼 브랜치가 가리키는 커밋을 앞으로 이동시키는 방법   
`(master) $ git merge {머지할_branch_name}`

### 3-way Merge
각 브랜치의 commit 2개와 공통 조상 1개를 사용하여 병합하는 방법  


### Merge Conflict
두 브랜치에서 같은 부분을 수정한 경우, Git이 어느 브랜치의 내용으로 작성해야 하는지 판단하지 못하여 충돌(conflict)이 발생했을 때 이를 해결하여 ,, ,,

##### [참고] 충돌이 일어나는 경우 
- 두 브랜치에서 같은 파일의 같은 부분을 수정하는 경우 ... 


---
```cmd
# git log를 그래프 형식으로 확인할 수 있게 해주는 명령어
git log --graph --all 
```


## Shared Repository Model

#### Fork와 Pull Request의 Process
- 다른 사람의 Repository Fork -> 내 Repository로 복제됨 
- 내 remote Repository에서 clone해서 local Repository로 복사
- 기능 구현 
- 내 remote Repository에 push 
- 다른 사람의 Repository에 내가 만든 변경 사항을 반영하고 싶으면 Pull Request를 보내면 원본자(기여자) 측에서 반영하고 싶다면 해당 request를 승인하고 pull 받아서 적용할 것

> Forking과 Cloning의 차이점  
Forking은 GitHub 계정에서 수행되고 복제는 Git을 사용하여 수행된다. Repository를 포크할 때 원본 Repository(Upstream Repository)의 복사본을 생성하지만 Repository는 GitHub 계정에 남아 있다. 반면에 저장소를 복제하면 저장소가 Git의 도움으로 로컬 컴퓨터에 복사된다. 포크된 저장소에 대한 변경 사항은 pull 요청을 통해 원래 저장소와 병합할 수 있다.   
Pull request는 저장소 소유자를 노크하고 “일부 변경을 수행했습다. 원하는 경우 이 변경 내용을 리포지토리에 병합하십시오.”라고 말한다. 반면에 로컬 머신(복제된 저장소)에서 변경한 사항은 업스트림 저장소로 직접 푸시할 수 있다.  
이를 위해 사용자는 저장소에 대한 쓰기 권한이 있어야 한다. 그렇지 않으면 불가능하다. 사용자에게 쓰기 액세스 권한이 없는 경우 분기된 요청을 통해서만 이동할 수 있다. 따라서 이 경우 복제된 리포지토리에서 변경된 사항이 먼저 포크된 리포지토리로 푸시된 다음 풀 요청이 생성된다.

## Git 브랜치 전략
### git-flo