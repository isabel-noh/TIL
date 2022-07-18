
# Git_"협업, 복구, 백업"
 리눅스 개발자인 리누스 토르발스이 개발한 것으로 분산 버전 관리 시스템이다. 다른 개발자들과 함께 업무를 할 때 예전에는 중앙집중식으로 버전 관리를 했으나 중앙집중식으로 관리를 하게 되면 서버의 데이터가 다 타버렸을 때, 복구할 수 없다는 단점이 있다. 이러한 단점을 방지하기 위해 만든 것이 `git`이다. 로컬에 원격 Repository의 모든 데이터를 복제하기 때문에 개발자의 수만큼 백업이 되어있다. 
 
##  GitHub ? Gitlab ?
GitHub과 Gitlab은 git을 통해 이용하는 Cloud서비스


##### GitHub 장점
1. Microsoft사의 서비스이기 때문에 비교적 안정적임
2. 개인 이용 시 무료 
3. Git저장소임에 동시에 개발 관련 정보를 공유할 수 있는 플랫폼

#### 그런데도 회사에서 GitHub 말고 Gitlab을 사용하는 이유는? 
1. 보안상의 이유
2. 비용상의 이유 - 기업으로 사용할 경우 GitHub이 요금이 더 비쌈
3. GitHub 이용 시 소스코드를 Microsoft사에 올리는 것으로 영업 비밀 유출 가능성 있다고 생각되어 꺼림

CLI(Command-Line Interface) <-> GUI(Graphic User Interface)
CLI : 명령어를 통해 사용자와 컴퓨터가 상호작용을 하는 방식 ex)MacOS - terminal / Windows - 명령 프롬프트(.cmd)
Why CLI? 
 - GUI는 CLI에 비하여 컴퓨터의 성능을 더 많이 소모함
 - 많은 서버 / 개발 시스템이 CLI를 통한 조작 환경을 제공함

home : C: > user > 현재 로그인한 사용자 

git bash: 쉘(Shell)이란 키보드로 입력한 명령어(Command)를 운영체제(OS)에 전달하여, 키보드로 입력한 명령어를 실행하게끔 하는 프로그램


- Markup vs Markdown
Markdown - e.g) velog, notion에성 마크다운 형식으로 글을 작성하게 되어있음
마크다운을 활용하게 되면 텍스트와 코드(w/ highlight syntex)를 같이 작성할 수 있음




- README.md (md: markdown)
활용: 오픈소스의 공식문서 작성 / 개인 프로젝트 소개 문서 작성 / WIL(Weekly I Learned) 작성 / 블로그 작성 / 소프트웨어의 배포 방법 안내


왜 Typora ?
1. 실시간 마크다운 변환 
2. 제공이미지 / 표 삽입


---

# Repository 
### 원격 Repository 
### Local Repository 
 - git init 명령어: local repository 생성 및 초기화 
 		(git을 사용하기 위해 가장 기본적으로 필요한 요소를 초기화)


### git - 3가지 영역을 바탕으로 관리함
> Working Directory
Staging Area
Repository

![](https://velog.velcdn.com/images/isabel_noh/post/4d0d10d7-fde4-46a0-9a83-754b09dd8e06/image.png)


#### Staging Area를 거치는 이유???
Staging Area : commit으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 있는 곳
commit: Staging Area안의 파일 하나 하나를 기록하는 것이 아니라, Staging Area 자체를 새로운 버전으로 기록함
	
### git 로컬에서 작업하기
> - **git init**: local repository 생성 및 초기화 
- **git add 파일이름.확장자**: 작업 디렉토리(working directory) 상의 변경 내용(삭제, 수정, 파일 생성 등... )을 버전으로 관리하고자, Staging Area에 추가하는 명령어
- **git add .** : 현재 Working Directory의 모든 변경사항을 Staging Area에 올리는 명령어
- **git status**: 현재 폴더의 git 상태를 확인하는 명령어
- **git commit -m 메시지내용**: '메시지 내용'을 커밋 메시지(수정 이유)로 남기면서 버전을 기록하는 명령어
- **git log**: 커밋한 기록을 확인하는 명령어
- **git log --oneline** : 커밋한 기록을 간단하게 한 줄로만 확인하는 명령어


### git과 원격저장소 연결하기
> - **git remote add origin 원격레포지토리url**: git과 원격 저장소 연결하는 명령어
- **git remote -v**: origin http://github.com/~~ 등록한 Remote Repository 정보 확인
- **git push origin master**: 연결된 원격 저장소(여기서 원격 저장소의 이름은 origin, 브랜치는  master 브랜치)에 로컬의 변경사항 업데이트 하기(master 브랜치에 업데이트)
- **git push -u origin master**:
	- git push
- **git pull origin master** : 원격 저장소의 변경 사항을 업데이트(원격 저장소로부터 받아와서 sync)
- **git clone 원격레포지토리url** : 원격 저장소를 로컬 저장소로 복제해온다

## 협업과 복구 및 백업
### Remote Repo 생성 및 연결하기
`원격 저장소에 Push하기 전에 반드시 최소 하나 이상의 Commit을 가져야한다.`
#### GitHub

1. 기본 브랜치 이름 master로 변경하기
2. new Repo 생성 버튼 클릭 (원격 저장소 생성)
  	1. 이름 설정
  	2. 생성

#### Local

3.  새로운 디렉토리 생성 
 	 1. mkdir
 	 2. cd 경로로 이동
 	 3. **git init**: Local Repository 생성
 	 4. git remote add origin 원격레포지토리url
	 5. git remote: origin 이름으로 remote 추가된 것 확인하기
	 6. touch README.md
   		  1. 내용 수정(Optional)

4. 버전 남기기(remote repository로 push하기 전에 반드시 commit해야 함)
 	 1. git add 파일명.확장자 / git add .
 	 2. git commit -m '커밋메시지'
	 3. git push origin master
     
     
### Branch
`흐름의 분기`
**pointer**는 하나의 커밋만 바라볼 수 있음
**master**은 일반적으로 상용 pointer

>- **git branch** : branch 리스트를 확인하는 명령어
	- `*`이 붙은  branch가 HEAD가 바라보는 branch
- **git branch branch이름** : 새로운 'branch이름'이름의 branch 생성하는 명령어
- **git switch branch이름** : HEAD가 바라보는 branch를 변경하는 명령어
- **git switch -c branch이름** : (-c : create ) 'branch이름'이름의 branch를 생성하고 pointer을 생성한 branch로 옮기는 명령어



### 3-way Merging
3-way Merging의 방법으로 머지를 하면 merge commit의 상태를 비교적 확실하게 확인할 수 있다. 
#### 3-way Merging의 순서 
> 1. 내 브랜치 commit
> 2. 다른 사람의 브랜치 commit
> 3. 두 브랜치의 공통 조상이 되는 merge commit

git은 merge를 할 때 각 브랜치의 마지막 커밋, 브랜치의 공통 조상 커밋을 비교하여 새로운 커밋을 만들어 병합을 수행한다.
[3-way Merge 참고](https://wonyong-jang.github.io/git/2021/02/05/Github-Merge.html)


### Git Ignore
github에 올리기 전에 여러가지 이유로 add에서 제외해야하는 파일들이 있다. 
> 보안상으로 위험성이 있는 파일
> 프로젝트와 관계없는 파일
> 용량이 너무 커서 제외해야되는 파일
`.gitignore` : 저장소에 추가되면 안 되는 파일과 폴더 목록을 모아놓은 디렉토리
git init을 한 폴더에 `.gitignore`이라는 이름의 파일을 만들고 그 안에 제외시키고 싶은 파일이나 폴더이름을 작성한다. 
**git repository를 생성하자마자 .gitignore파일을 생성해야 함**
> 참고 [gitignore.io](https://www.toptal.com/developers/gitignore)
>  gitignore.io: 언어, OS 나 Framework, IDE 별로 저장소에 추가되면 안 되는 파일과 폴더 목록인 .gitignore 를 자동으로 생성해 주는 서비스

