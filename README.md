# TIL

---
### Ground Rule


### Markdown 학습
 #### 제목(Heading) 표현하기
  제목은 제목 앞에 '#'를 작성하여 표현할 수 있다. 
  '#'의 개수에 따라 H1, H2, H3, H4, H5, H6으로 중요도가 작은 제목을 달 수 있다. 
  # Heading1
  ## Heading2
  ### Heading3
  #### Heading4
  ##### Heading5
  ###### Heading6

  #### 순서가 있는 리스트(ordered list)
  1. 아이스크림
  2. 젤리
  3. 푸딩

  #### 순서가 없는 리스트(unordered list)
  * 쿠팡
  * 마켓컬리

  ####  코드블럭 작성
  '백틱' 3개씩으로 감싸 코드블럭을 작성할 수 있다. 
  ```list.sort(type=int) ``` 

  #### inline 코드 작성
  '백틱' 1개씩으로 감싸 인라인 코드를 작성할 수 있다. 
  `print()`함수로 출력할 수 있다. 

  #### [ 링크 이름 ] ( url ) 링크 입력하기
  [노현정의 깃허브](https://github.com/isabel-noh)

  #### ! [사진 이름] ( img_url ) 사진 입력하기
  

#### bold, italic, strikeout로 글씨 작성
- **bold** : '*' 2개로 감싸 bold를 나타낼 수 있다. 
- *italic* : '*' 1개로 감싸 italic을 나타낼 수 있다. 
- ~~strikeout~~ : '~' 2개로 strikeout을 나타낼 수 있다. 

#### `*` 혹은 `_` , `-` 를 3개 이상 사용하여 선을 그을 수 있다. 
___

##### `*` 대신 ` _`을 사용할 수 있다


### Git
#### Git_"협업, 복구, 백업"
 리눅스 개발자인 리누스 토르발스이 개발한 것으로 분산 버전 관리 시스템이다. 다른 개발자들과 함께 업무를 할 때 예전에는 중앙집중식으로 버전 관리를 했으나 중앙집중식으로 관리를 하게 되면 서버의 데이터가 다 타버렸을 때, 복구할 수 없다는 단점이 있다. 이러한 단점을 방지하기 위해 만든 것이 `git`이다. 로컬에 원격 Repository의 모든 데이터를 복제하기 때문에 개발자의 수만큼 백업이 되어있다. 
##### GitHub 장점
1. Microsoft사의 서비스이기 때문에 비교적 안정적임
2. 개인 이용 시 무료 
3. Git저장소임에 동시에 개발 관련 정보를 공유할 수 있는 플랫폼

##### 그런데도 회사에서 GitHub 말고 Gitlab을 사용하는 이유는? 
1. 보안상의 이유
2. 비용상의 이유 - 기업으로 사용할 경우 GitHub이 요금이 더 비쌈
3. GitHub 이용 시 소스코드를 Microsoft사에 올리는 것으로 영업 비밀 유출 가능성 있다고 생각되어 꺼림

##### CIL 
CLI(Command-Line Interface) <-> GUI(Graphic User Interface)
CLI : 명령어를 통해 사용자와 컴퓨터가 상호작용을 하는 방식 ex)MacOS - terminal / Windows - 명령 프롬프트(.cmd)
Why CLI? 
 - GUI는 CLI에 비하여 컴퓨터의 성능을 더 많이 소모함
 - 많은 서버 / 개발 시스템이 CLI를 통한 조작 환경을 제공함

---

- home == C:> user > 현재 로그인한 사용자 

- git bash: bash는 'Bourne Again Shell'의 줄임말로, 스티브 본(Steve Bourne)이라는 사람이 개발한 최초의 유닉스 '쉘 프로그램'인 sh의 확장판이라는 의미  **쉘(Shell)**이란 키보드로 입력한 명령어(Command)를 운영체제(OS)에 전달하여, 키보드로 입력한 명령어를 실행하게끔 하는 프로그램


##### README.md (md: Markdown)
| 활용: 오픈소스의 공식문서 작성 / 개인 프로젝트 소개 문서 작성 / WIL(Weekly I Learned) 작성 / 블로그 작성 / 소프트웨어의 배포 방법 안내

Markdown - e.g) velog, notion에성 마크다운 형식으로 글을 작성하게 되어있음
마크다운을 활용하게 되면 텍스트와 코드(w/ highlight syntex)를 같이 작성할 수 있음

#### Repository 
	##### 원격 Repository 
	##### Local Repository 
		- git init 명령어: local repository 생성 및 초기화 
 		(git을 사용하기 위해 가장 기본적으로 필요한 요소를 초기화)


git - 3가지 영역을 바탕으로 관리함
![](https://velog.velcdn.com/images/isabel_noh/post/4d0d10d7-fde4-46a0-9a83-754b09dd8e06/image.png)
#### Staging Area를 거치는 이유???
- Staging Area : commit으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 있는 곳
- commit: Staging Area안의 파일 하나 하나를 기록하는 것이 아니라, Staging Area 자체를 새로운 버전으로 기록함
	
> ### git 로컬에서 작업하기
- **git init**: local repository 생성 및 초기화 
- **git add 파일 이름**: 작업 디렉토리(working directory) 상의 변경 내용을 스테이징 영역(staging area)에 추가하는 명령어
- **git add .** : 현재 디렉토리의 모든 파일을 스테이징 영역에 추가하는 명령어
- **git status**: 현재 폴더의 git 상태를 확인하는 명령어
- **git commit -m 메시지내용**: '메시지 내용'을 커밋 메시지(수정 이유)로 남기면서 commit하는 명령어
- **git log**: 커밋한 기록을 확인하는 명령어
- **git log --oneline** : 커밋한 기록을 간단하게 한 줄로만 확인하는 명령어
- 

>### git과 GitHub 연결하기
- **git remote add 원격레포지토리url**: git과 Github 연결하는 명령어
- **git push origin master**: 연결된 Github에 로컬의 변경사항 업데이트 하기

#### Remote Repo 생성 및 연결하기
##### GitHub

1. 기본 브랜치 이름 master로 변경하기
2. new Repo 생성 버튼 클릭 
  	1. 이름 설정
  	2. 생성

##### Local

3.  새로운 디렉토리 생성 
 	 1. mkdir
 	 2. cd 경로로 이동
 	 3. **git init**
 	 4. git remote add origin 원격레포지토리url
	  5. git remote: origin 이름으로 remote 추가된 것 확인하기
	  6. touch README.md
   		  1. 내용 수정(Optional)

4. 버전 남기기(remote repository로 push하기 전에 반드시 commit해야 함)
 	 1. git add 파일명.확장자 / git add .
 	 2. git commit -m '커밋메시지'
	 3. git push origin master