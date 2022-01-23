# 목차

[Git 개요](#git-개요) <br/>
[Git Branch](#git-branch) <br/>
[Git Branch 전략](#git-branch-전략) <br/>
[Git Workflow](#git-workflow) <br/>
[Git Conflict]() <br/>
[Git Wrap up](#git-wrap-up) <br/>

---

# Git 개요

| 싱글(개인) 플레이 | 멀티(팀) 플레이 |
| --- | --- |
| 코드 관리/백업 | - 협업 Workflow<br/> - 커밋 컨벤션 통일<br/> - 배포 자동화<br/> - 코드리뷰 |

![Git구조 및 명령어](https://user-images.githubusercontent.com/45352173/150685635-b3589c31-8554-47e2-bccb-d61f062cc657.png)


Git구조 및 명령어 <br/>
📚 [git cheat sheet](https://training.github.com/downloads/ko/github-git-cheat-sheet/)을 검색하면 자주 사용하는 명령어를 정리한 문서가 나온다. 

<br/><br/>

# Git Branch
![git graph](https://user-images.githubusercontent.com/45352173/150685430-cd1974df-3679-47db-9ee7-21c7a1a31896.png)

### Branch
코드관리를 위해서 가지처럼 분기되는 흐름을 만들어내는 용도<br/>
업무에 따라서 Branch의 이름으로 작업하고 정리하는 방식<br/>
Branch는 가지보다는 **'강'**으로 이해하면 더 쉽다.<br/>

- 큰 강에는 작은 지류들이 뻗어 나올 것이고, 해당 지류는 다시 큰 강으로 합쳐질 것이다.
- 큰 강이란 'master' 브랜치와 같은 중심이 되는 공간이고, 각 업무를 진행하기 위해서 지류로 나왔다가 다시 merge 과정을 통해 'master'(develop) 브랜치로 들어간다.

<br/>

> 💡 Git Bash 명령어 :: branch <br/>
> 
> git branch `브랜치명` [`분기 시작 브랜치명`] <br/>
>  : `분기 시작 브랜치명`에서 새로운 branch가 생성된다. <br/>
>  : `분기 시작 브랜치명`을 생략하면 자동으로 현재 커밋에서 새로운 branch가 생성된다. <br/>
>
> git checkout `브랜치명` <br/>
>  : `브랜치명` 으로 현재 branch를 변경한다. 이 때, commit 되지 않은 코드들은 사라진다. <br/>
>
> git push [`--set-upstream`] [origin/`브랜치명`] <br/>
>  : 원격 저장소에 branch를 저장한다. <br/>
>  원격 저장소에 branch가 존재하지 않으면 `--set-upstream` 명령어를 입력해줘야한다. <br/>
>  origin/`브랜치명`을 입력하면 해당 branch로 현재 branch의 커밋상태를 저장한다. <br/>

<br/><br/>

# Git branch 전략
![Git flow](https://user-images.githubusercontent.com/45352173/150685814-4aa47816-aed8-4b8e-a18f-fbeecd20448a.png)

### Feature
- 기능을 개발하는 branch
- 개발단계의 각 기능들이며 에러 이슈가 많이 발생한다.
- develop branch에서 feature/`기능명` 형태로 생성한다.
- 기능을 완성하면 develop branch로 merge를 요청한다.

### Develop
- 기능들을 모아놓고 일정 기능 구현이 완료가 되면 Release branch로 merge를 요청한다.
- release/`버전`

### Bugfix
- Release branch에 merge하기 전 버그를 발견
- 버그를 수정하는 branch 단계
- bugfix/`기능명`

### Release
- QA 등의 업무가 이뤄지는 곳
- 스테이징 서버, 테스트용 서버에 올라가서 지금 이 기능들이 모두 정상 작동하는지 확인한다.
- 확인이 완료되면 Master branch로 merge를 요청한다.

### Master
- 여기서 작동되는 코드가 상품화되어 고객에게 보여진다.

### Hotfix
- 상품화한 후 기능이 돌아가지 않는 오류가 발생
- 긴급히 수정해야한다.
- 빠른 수정을 요구하므로 수정하자마자 merge request하지 않고 바로 merge한다.
- hotfix/`기능명`

## Git flow 시작하기
```bash
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [main]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
```

```bash
(사용자 PC) MINGW64 ~/[프로젝트 경로명] (develop)
$ git branch
* develop   // <-- 현재 브랜치
master 

$ git flow feature start sign_up
Switched to a new branch 'feature/sign_up'    // 브랜치 만들기

summary of actions:
- A new branch 'feature/sign_up' was created, based on 'develop'
- You are now on branch 'feature/sign_up'

Now, start committing on your feature. When done, use:
		git flow feature finish sign_up

(사용자 PC) MINGW64 ~/[프로젝트 경로명] (feature/sign_up)  // 브랜치 바뀜.
```

➡ [자세한 기능은 다음을 참고](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

# Git WorkFlow

### TBD(Trunk Based)
- **모든 개발자들이 Master브랜치를 기반으로 개발을 진행**한다.
- 모든 Feature 브랜치는 가능한 짧은 주기로 가져가며 항상 Master브랜치를 fresh하게 유지한다.
- 능숙한 개발자들이 하루에도 수십번 배포하는 과정의 비즈니스에서 자주 사용 한다.

<image width="40%" src="https://user-images.githubusercontent.com/45352173/150685955-99b5cb3e-3ea3-4b90-86c6-a9183ac75c7d.png"/>

### 권장되는 Git Flow 모델
- feature → develop → master 단계만 거치는 모델
- hotfix branch로 긴급 오류 수정

<image width="40%" src="https://user-images.githubusercontent.com/45352173/150686096-7e51d7d6-330e-4dfa-900b-c09befdca21a.png"/>


> **학습자료**
>
> 📕 [pro git](https://git-scm.com/book/ko/v2)<br/>
> 🌐 [git with D3](https://onlywei.github.io/explain-git-with-d3/)<br/>
> ⌨ [git 명령어 연습](https://learngitbranching.js.org/?locale=ko)<br/>
> 

# Git Wrap up
✅ 개발에 방해되지 않을 정도까지는 Git 기본 개념/명령어 숙지<br/>
✅ Git Branch를 사용한 코드관리의 흐름(flow) 이해<br/>
✅ 회사/팀별 상황에 맞는 Git Branch 전략 선택<br/>
✅ 팀 별 합의된 정책에 맞춰 일관된 Git 사용 노력 필요<br/>
✅ 궁금하거나 자주 마주하는 케이스에 대한 Git 사용법은 꼭 연습<br/>

<br/>

## 스크럼 개발 프로세스
**다기능 팀**이 제품이나 프로젝트를 **반복적이고 점진적**으로 개발하는 방식

![https://dbscthumb-phinf.pstatic.net/4666_000_1/20161005133248144_GPEOCX8WT.jpg/ka37_53_i2.jpg?type=w690_fst_n&wm=Y](https://dbscthumb-phinf.pstatic.net/4666_000_1/20161005133248144_GPEOCX8WT.jpg/ka37_53_i2.jpg?type=w690_fst_n&wm=Y)

### 스크럼 스탠드업 미팅(stand-up-meeting)
참석자들이 신체가 서있는 채로 참여하는 미팅<br/>
미팅을 짧은 시간으로 유지하기 위해 장시간 서있는 것으로 인한 인한 불편함을 초래시킨다.

<br/>

**미팅 취지**<br/>
프로젝트를 진행한다는 것은 많은 **불확실성**을 내포하고 있다는 것<br/>
이 불확실성을 줄이기 위해서 데일리 스크럼을 진행

<br/>

**미팅 필요성**<br/>

<image width="30%" src="https://user-images.githubusercontent.com/45352173/150686149-628e819c-ab77-4b9e-8902-1ca7c8c47be6.png"/>

- 프로젝트 초반부에는 프로젝트에 대한 정보가 한정적이기 때문에 일의 분배가 효율적이지 못하다.
- 프로젝트 정보가 많은 후반부에는 업무를 효율적으로 분배할 수 없다.
- 따라서, 지속적으로 팀원 들간 정보를 공유하여 계속적인 조율을 통해 효율적인 업무 분배를 진행할 수 있다.

<br/><br/>

> 💡 **프로젝트가 진행됨에 따라 높아져야 할 것과 낮아져야 할 것은?**
> 
> ![image](https://user-images.githubusercontent.com/45352173/150686320-0cc788cd-01cb-448d-9fae-e5659039d5b6.png)
> 
> ➕ 높아져야 할 것
> 
> - 프로젝트 해상도(가시성)
> - 프로젝트 이해도
> - 팀원과 친밀도, 신뢰도
> - 커뮤니케이션 능력
> - 문제해결 능력
> - 개발자 역량, 성장
> - 개발생산성
> - 배포 속도
> - 프로젝트 결과물
> - ...

