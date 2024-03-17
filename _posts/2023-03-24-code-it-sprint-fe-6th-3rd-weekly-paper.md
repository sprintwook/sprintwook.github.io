---
layout: post
title: 코드잇 스프린트 6기 FE 위클리 페이퍼 3주차
subtitle: CodeIt Sprint Weekly Paper 3rd Week
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: ["#코드잇스프린트", "#스프린트프론트엔드6기", "#취업까지달린다" ]
author: Jongwook Lee
---

# 3주차 위클리 과제 안내

<br>

{: .box-note}
**Git에서 branch merge 방법들과 각 방법의 특징을 설명해 주세요.**<br>
**Git Flow 브랜치 전략에 대해 설명해 주세요.**<br>
**제출은 위클리 페이퍼 답안 제출 설문에 일요일 23시 59분까지 해주시면 됩니다.**<br>


<br>

## 조사 내용

#### 1. Git에서 branch merge 방법들과 각 방법의 특징을 설명해 주세요.
- Git에서의 브랜치란, 협업 시 각자 맡은 것을 작업인 커밋을 이름 형태로 참조할 수도록 만든 라벨 같은 것
- Git에서의 병합이란, Git의 포크된 기록을 다시 통합하는 방법
	- `git merge` 명령을 사용하면 Git 브랜치가 만든 독립적인 개발 라인을 단일 브랜치로 통합 가능
	- 위 명령을 사용하면 현재 위치된 브랜치에 해당 브랜치가 병합됨
	- `git merge` 명령은 종종 `git checkout` 명령과 함께 사용되어 현재 브랜치를 선택하고 `git branch -d`와 함꼐 사용되어 사용하지 않는 브랜치를 삭제함
- 작동 원리는 하기와 같습니다.
	- `git merge` 명령은 여러 커밋 시퀀스를 하나의 통합된 기록으로 결합함
	- `git merge` 명령은 두 브랜치를 결합할 때 주로 사용됨
	- `git merge` 명령은 두 개의 커밋 포인터 (보통은 브랜치명 사용)를 사용하여 그 사이에 있는 일반적인 Base 커밋을 찾음
	- Git은 일반적인 Base 커밋을 찾으면 대기 중인 각 병합 커밋 시퀀스의 변경 사항을 결합하는 새 병합 커밋을 만듦
- 예시로 `main`브랜치를 기준으로 하는 새로운 Feature 브랜치가 있다고 하면 이 Feature 브랜치를 main 브랜치에 병합하는 경우
	- 이 명령을 호출하면 지정된 브랜치 기능이 현재 브랜치에 병합되는데,`main` 브랜치로 병합됨
	- Git은 병합 알고리즘을 자동으로 결정하여 진행함
	![](/assets/img/w3/img_01.png)
	- 병합 커밋은 상위 커밋이 두 개 있다는 점에서 다른 커밋과 구별됨
	- 병합 커밋을 만들 때 Git은 사용자를 위해 별도의 기록을 자동으로 병합하려고 시도함
		- Git이 두 기록에서 변경된 데이터 조각을 발견하면 자동으로 결합할 수 없음
	- 해당 내용은 Git 내에서 버전 충돌이 발생했을 때의 사항을 보여줌
	![](/assets/img/w3/img_02.png)
- 병합을 원할히 진행하기 위해서는 몇 가지 준비 단계를 거쳐야 합니다.
	- 수신 브랜치 확인 : `git status` 명령을 통해 `HEAD`가 올바른 병합 수신 브랜치를 가리키는지 확인
		- 필요에 따라 `git checkout` 명령을 통해 수신 브랜치로 전환함
	- 최신 원격 커밋 적용 : 수신 브랜치 및 병합 브랜치가 최신 원격 변경 사항으로 업데이트되었는지 확인
		- `git fetch`를 실행하면 최신 원격 커밋을 가져옴
		- 가져오기가 완료되면 `git pull`을 실행하여 `main` 브랜치가 최신으로 업데이트되었는지 확인
- 위 단계를 거치면 `git merge` 명령을 통해 병합할 수 있음		

- 빨리 감기 병합 (Fast-Forward Merge)
	- 현재 브랜치에서 대상 브랜치까지의 선형 경로가 존재하는 경우, 빨리 감기 병합이 발생될 수 있음
	- 브랜치를 실제로 병합하는 대신, Git은 현재 브랜치를 대상 브랜치까지 이동시키는 작업만으로 기록을 통합할 수 있음
	- 대상 브랜치에서 연결할 수 있는 모든 커밋을 이제 현재 커밋을 통해 사용할 수 있어 기록이 효과적으로 결합됨
	- 브랜치를 분기하는 경우이거나 대상 브랜치에 대한 선형 경로가 없는 경우, Git은 3방향 병합을 통해 결합할 수 밖에 없음
	![](/assets/img/w3/img_03.png)
	
- 3방향 병합 (3-Way Merge)
	- Git이 브랜치 2개와 Base인 커밋 1개, 총 3개를 사용하여 병합 커밋을 만드는 것에서 유래함 
	- 전용 커밋을 사용하여 두 커밋을 연결함
	- 결과적으로 병합 커밋은 두 브랜치의 상징적 결합으로 사용됨
	![](/assets/img/w3/img_04.png)
	
- 빨리 감기 병합이나 3방향 병합 중 어느 전략이든 사용가능하나, 많은 개발자들은 버그 수정에는 빨리감기 병합을 사용하고 장기 실행 기능을 통합할 때 3방향 병합을 사용함

- 빨리 감기 병합은 하기와 같은 명령어 흐름으로 진행됨
	- 하기 코드는 새 브랜치를 만들고, 브랜치에 커밋 두 개를 추가한 다음, 빨리 감기 병합을 통해 메인 라인에 병합시킴
	- 장기 실행 기능용 조직 도구보다 개별적인 개발에 자주 사용되는 브랜치의 일반적인 워크플로에서 활용됨
	- 새로운 기능은 이제 메인 브랜치에 액세스 가능하므로 `git branch -d` 명령에서 오류가 발생하지 않음
	- 빨리 감기 병합 동안 기록을 유지하기 위한 병합 커밋이 필요하면 `--no-ff` 옵션을 사용하여 merge할 수 있음 (`git merge --no-ff <branch>`)
	~~~
	# Start a new feature
	git checkout -b new-feature main
	# Edit some files
	git add <file>
	git commit -m "Start a feature"
	# Edit some files
	git add <file>
	git commit -m "Finish a feature"
	# Merge in the new-feature branch
	git checkout main
	git merge new-feature
	git branch -d new-feature
	~~~
	
- 3방향 병합은 하기와 같은 명령어 흐름으로 진행됨
	- 하기 코드는 새로운 기능 개발이 진행되는 동안 main 브랜치에서 진행되므로 3방향 병합이 필요함
	- 대규모 기능이나 여러 개발자가 동시에 프로젝트를 작업할 때 흔히 발생하는 시나리오임
	- 백트래킹 없이 `main` 브랜치를 `new-feature` 브랜치로 이동할 방법이 없으므로 빨리 감기 병합은 어려움
	- 대부분 새로운 기능 개발은 시간이 오래 걸리는 훨씬 더 큰 기능이므로 그 동안 `main` 브랜치에서 새 커밋이 등장할 수 밖에 없음
	- 규모가 작으면 `main` 브랜치를 다시 지정하고 빨리 감기 병합을 수행하는 것이 나음
	~~~
	Start a new feature
	git checkout -b new-feature main
	# Edit some files
	git add <file>
	git commit -m "Start a feature"
	# Edit some files
	git add <file>
	git commit -m "Finish a feature"
	# Develop the main branch
	git checkout main
	# Edit some files
	git add <file>
	git commit -m "Make some super-stable changes to main"
	# Merge in the new-feature branch
	git merge new-feature
	git branch -d new-feature
	~~~
- 충돌 해결
	- 병합하려는 두 브랜치 간 동일한 파일의 동일한 부분이 변경되면 Git은 어떤 커밋을 사용해야 하는지 알 수 없음
	- 위 경우, 병합 직전에 중지하여 수동으로 해결해야 함
	- Git 병합 프로세스에서 좋은 점은 익숙한 편집/스테이지/커밋 워크 플로를 이용하여 병합 충돌을 해결함
	- 병합 충돌이 발생한 경우 `git status` 명령을 통해 해결할 파일이 표시됨
	- 충돌을 표시하는 방법은 양쪽을 표시하는 시작적 표시 마크를 사용함
		- 시각적 마커는 `<<<<<<<`, `=======` 및 `>>>>>>>`임
		- `=======`의 앞 콘텐츠는 수신 브랜치이고, 뒤 부분은 병합 브랜치임
	- 충돌한 부분을 확인한 후에 원하는 대로 병합을 수정할 수 있음
	- 병합을 완료할 준비가 되면 충돌할 파일에서 `git add` 명령을 실행하여 Git에 충돌이 해결되었음을 알리면 끝남
	- 충돌이 해결되었음을 알린 후, `git commit` 명령을 통해 병합 커밋을 생성함
	- **병합 충돌은 3방향 병합인 경우에만 발생함, 빨리 감기 병합에선 충돌이 발생될 수 없음**
	
- Github에서의 지원되는 Merge 방식은 총 Merge, Squash and Merge, Rebase Merge로 총 3가지가 존재함
	- Merge는 하나의 브랜치와 다른 브랜치의 모든 변경 이력을 합치는 방식으로 Merge Commit에서부터 뒤로 돌라가면서 부모를 모두 찾고 브랜치를 구성하게 됨
		- Merge Commit은 C와 Init을 모두 부모로 가지게 되는 특징을 띄게 되고, 역으로 되돌아가면서 C는 B, B는 A, A는 Init을 다시 부모로 가지게 됨
		~~~
		$ git checkout master
		$ git merge my-branch
		~~~
		![](/assets/img/w3/img_05.png)	
	
	- Squash and Merge는 각각 Commit되었던 A, B, C를 합쳐서 하나의 새로운 commit으로 생성하고 브랜치에 추가함
		- 새롭게 생성된 A,B,C 통합 Commit은 부모를 Init 하나만 가지게 됨
		~~~
		$ git checkout master
		$ git merge --squash my-branch
		$ git commit -m "commit message"
		~~~
		![](/assets/img/w3/img_06.png)	
	
	- Rebase and Merge는 이전에 수행되었던 Commit A,B,C 간의 관계를 그대로 유지하면서 main 브랜치에 추가함
		- Commit A는 메인 브랜치의 이전 커밋인 Commit e를 부모로 가지게 됨
		- Rebase and Merge 작업 이후에 이전에 존재했던 브랜치의 A,B,C Commit과 메인 브랜치의 Init, D,E,A,B,C Commit과 연관성이 없어짐
		~~~
		$ git checkout my-branch
		$ git rebase master
		$ git checkout master
		$ git merge my-branch
		~~~
		![](/assets/img/w3/img_07.png)	
	
		
<br>

#### 2. Git Flow 브랜치 전략에 대해 설명해 주세요.
- Git Flow에는 5가지 종류의 브랜치가 존재함
	- 항상 유지되는 메인 브랜치들(master, develop)과 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)가 있음
- Git Flow 브랜치의 종류
  | 브랜치명      | 설명                                                  |
  | :------------ | :----------------------------------------------------- |
  | `master` | 제품으로 출시될 수 있는 브랜치 |
  | `develop` | 다음 출시 버전을 개발하는 브랜치 |
  | `feature` | 기능을 개발하는 브랜치 |
  | `release` | 이번 출시 버전을 준비하는 브랜치 |
  | `hotfix` | 출시 버전에서 발생한 버그를 수정하는 브랜치 |

- Git Flow의 흐름 이미지  
	![](/assets/img/w3/img_08.png)	
	
	- 처음에는 master	와 develop 브랜치가 존재함
		- develop 브랜치는 master에서부터 시작된 브랜치임
	- develop 브랜치에서는 상시로 버그를 수정한 커밋들이 추가됨
	- 새로운 기능 추가 작업이 있는 경우, develop 브랜치에서 feature 브랜치를 생성함
		- feature 브랜치는 언제나 develop 브랜치로부터 시작됨
		- 기능 추가 작업이 완료되면 feature 브랜치는 develop 브랜치로 merge함
	- develop 브랜치에 이번 버전에 포함되는 모든 기능이 merge 되었다면 품질 검증을 위해 develop 브랜치에서 release 브랜치를 생성함
		- 품질 검증이 진행하면서 발생된 버그는 release 브랜치에서 수정됨
	- 품질 검증을 통과하면 release 브랜츠를 master와 develop 브랜치로 merge함
	- 마지막으로 추신된 master 브랜치에서 버전 태그를 추가함
	
<br>	

#### 3. 참조
  | Features      | Links                                                  |
  | :------------ | :----------------------------------------------------- |
  | Atlassian 공식 문서  | [링크로 이동](https://www.atlassian.com/ko/git/tutorials/using-branches/git-merge)|
  | 참조 블로그 | [링크로 이동](https://datalibrary.tistory.com/194) |
  | 우아한기술블로그 | [링크로 이동](https://techblog.woowahan.com/2553/) |