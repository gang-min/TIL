# GIT

> contents
>
> - GIT이란
> - GIT과 GITHUB의 관계
> - GIT 초기화 하고 삭제하기
> - GIT의 중요한 컨셉 이해하기
> - Git 명령어 이용 방법
> - 기본 명령어
>   1.  로컬 파일들 추가하기(add)
>   2.  Staging Area에서 제거하기(rm --cached)
>   3.  절대 추가 하면 안되는 아이들(ignore)
>   4.  현재 상태 확인하기(status)
>   5.  파일 비교하기(diff)
>   6.  버전 등록하기(commit)
>   7.  버전들 목록 보기(log)
>   8.  태그는 왜 필요할까?(tag)
>   9.  전환(checkout)
> - Branch
>   1.  브랜치를 왜 꼭 써야 할까?
>   2.  브랜치 기본 사용법
>   3.  머지란? (fast-forward merge, Three-way merge)
>   4.  Conflict 해결 방법
>   5.  Rebase란 무엇일까? 왜 꿀일까? 🐝
>   6.  필요한 커밋만 쏘옥~! 🍒 (cherry-pick)

# `GIT이란`

- GIT은` VCS(버전 관리 시스템)`중 하나로 VCS는 Version Control System에 약자이다.

- `버전 관리 시스템`이란?

  - 변경점 관리: 어떤 내용을 누가 작성해서 어느 시점에 들어갔는지 확인할 수 있게 해 준다.
  - 버전 관리: 특정 시점에 꼬리표(Tag)를 달아 버전을 표시해주고, 브랜치(Branch) 등으로 동시에 여러 버전을 개발할 수 있게 해 준다.
  - 백업&복구: 무언가가 잘못되었을 때 다시 특정 시점으로 돌아가게 해 주고, 사고로 내용이 날아간 경우에도 복구할 수 있게 해 준다.
  - 협업: 같이 일하는 사람들에게 수정사항을 쉽게 공유.

- 두가지의 버전 관리 시스템

1.  `CVCS(Centralized Version Control System , 중앙 버전 관리 시스템)`
    - 서버에 히스토리를 관리해서 각각의 개발자들이 원하는 내용을 서버에 업데이트해서 즉각적으로 동기화가 이루어지는 시스템
    - 대표적으로 CVS, Subversion, Perforce

```
문제점
1. 서버에 문제가 생기면 많은 개발자들이 일을 하지 못하는 경우가 많다.
2. 오프라인에서 인터넷이 없을때 일을 하지 못한다.
```

- 이러한 문제점을 개선하기 위해서 나온 것이 바로  
   2. `DVCS(Distributed Version Control System, 분산 버전 관리 시스템)`
  - 서버에만 히스토리 정보가 있는 것이 아니라 모든 개발자들이 동일한 히스토리 정보를 가지고 있는 것
  - 대표적으로 `Git`, Mecurial, Bazzar, Darcs

```
장점
1. 서버에 문제가 생기거나 다운이 되어도 각각의 개발자들이 동일한 히스토리를 가지고 있기 때문에 서로의 정보를 이용해서 서버를 보관하고 또 계속 일을 이어 나갈 수 있다.
2. 인터넷이 없어도 오프라인에서 일을 진행할 수 있다.
```

# `GIT과 GITHUB의 관계`

- 일을 하다보면 협업하고 있는 `코드를 저장할 서버`가 필요하다.
- 이때 VCS을 지원하는 웹호스팅 서비스(GITHUB)의 기능을 통해 push, pull, request와 같은 이벤트에 반응하여 자동으로 작업을 실행하게 할 수 있다.

# `GIT 초기화하고 삭제하기`

- 프로젝트를 시작하고 소스 코드를 GIT으로 관리하고자 한다면 먼저 git init을 해야하는데

  - `git init`: `GIT 저장소(repository)를 초기화하고 새로운 GIT 저장소(repository)를 생성 한다.` 저장소나 디렉토리 안에서 이 명령을 실행하기 전까지는 그냥 일반 폴더이다. 이것을 입력한 후에야 추가적인 깃 명령어들을 줄 수 있다.

  - git을 초기화하게 되면 기본적으로 `main branch`가 생성이 된다.

- GIT을 삭제하려면
  - `rm -rf .git`: `GIT 저장소(repository)를 삭제한다.`

# `GIT의 중요한 컨셉 이해하기`

- GIT을 정확하게 이해하고 잘 활용하기 위해서는 GIT의 workflow를 이해하는 것이 정말 중요하다.
- GIT에는 크게 총 3가지의 작업환경이 나눠져 있다.

  1. `Working Directory`: 프로젝트의 파일들을 수정하는 작업을 하고 있는 곳
     - working directory는 엄밀히 말하면 2가지로 나누어 볼 수 있다.
       1. `Untracked` : 새로 만들어진 파일이거나 기존에 존재하던 프로젝트에서 Git을 초기화 하게 되면 Git이 파일에 대한 정보가 전혀 없는 파일들
       2. `tracked` : Git이 이미 알고있는(tracking) 파일들
          - Git이 tracking하고 있는 파일들 중에서도 오직 수정이 된 Modified 파일만 Staging Area로 옮겨 갈 수 있다.
          1. `Modified`: 지금 이 시점에서 수정이 되었다면
          2. `Unmodified`: 이전 버전과 비교해서 수정이 되지 않은 것
  2. `Staging Area`: 어느정도 작업하다가 버전 히스토리에 저장(Commit)할 준비가 되어있는 파일들을 옮겨놓는 곳
  3. `.git Directory(Git Repository)`: 버전의 `히스토리`를 가지고있는 곳

- 이렇게 저장된 `Git 히스토리`는 `나의 컴퓨터(Local)`에만 보관 되기 떄문에 내컴퓨터에 문제가 생기면 이런 히스토리를 다 잃어버릴 수가 있다. 그래서 보통 `git directory(git repository)`를 나의 컴퓨터(Local)에만 저장해 두는 것이 아니라 `GitHub와 같은 서버`에 push라는 명령어를 이용해서 나의 git directory를 서버에 업로드 해 둘 수가 있다.

- 그리고 서버에서 다시 내컴퓨터(Local)로 다운로드 받고 싶을 때는 pull 이라는 명령어를 이용할 수 있다.

- 각각의 `버전(commit)`들에는 스냅샷된 정보들을 기반으로 해서 아래와 같은 정보들이 포함 되어있다.

```
고유한 해쉬코드 : 버전 정보를 참조 할 수 있다.
message : 어떤 버전인지 버전에 관련된 메세지
author : 누가 작성했는지
date/time : 날짜와 시간
```

# `Git 명령어 이용 방법`

- `git 명령어 -option`

```
예시
1. git config
2. git add
3. git commit
4. git status
5. git add -option
6. git commit -option
...등
```

- option들이 여러가지가 있어서 같은 명령어를 수행하더라도 어떤 옵션을 붙이냐에 따라서 조금씩 다른 방식으로 진행할 수 있다.

# `기본 명령어`

## 1. `로컬 파일들 추가하기(add)`

- `Working Directory에 있는 파일을 Staging Area로 옮긴다.`
- Untracked 파일들은 tracked 파일로 바꾸며 Staging Area로 옮기고
- 이미 Tracked 파일들중 Modified 파일들은 바로 Staging Area로 옮긴다.

* 사용법

```
git add <파일명> :  <파일명>만
git add <파일명> <파일명> <파일명> :  <파일명> 다수 작성 가능
git add *.txt : 확장자가 txt인 파일들 전부
git add * : .gitignore에 있는 것 상관없이 모든 파일
git add . : .gitignore에 명시된 것을 고려한 모든 파일 (추천)
```

## 2. `Staging Area에서 제거하기(rm --cached)`

- 사용법

```
git rm --cached <파일명>
```

## `3. 절대 추가 하면 안되는 아이들(ignore)`

- tracking하고 싶지 않은 파일들, Git과 GitHub에 올리고 싶지 않은 파일들은 .gitignore파일에 추가하면 된다.

## `4. 현재 상태 확인하기(status)`

- 작업하고 있는 모든 내용들을 간단하게 확인해 볼 수 있다.
- 사용법

```
git status --long(default)
```

## `5.파일 비교하기(diff)`

- git status를 이용하여 어떤 파일들이 수정 되었고 Staging Area에 있는지 확인할 수 있지만, 정확하게 어떤 내용이 수정이 되었는지는 확인할 수 없다.

- 그래서 정확하게 어떤 파일의 내용이 수정이 되었는지 확인해 보려면` git diff`를 이용하면 된다.
- 사용법

```
git diff : 아무런 옵션이 없으면 Working Directory에 있는 것만 비교해서 볼 수 있다.

예시)

 git diff
diff --git a/add.txt b/add.txt
index e69de29..893b969 100644
--- a/add.txt
+++ b/add.txt
@@ -0,0 +1 @@
+add
```

- a라고 하는 것은 `이전 버전`을 의미
  - 이전버전 : Working Directory에 있는 파일이라면 이전에 commit된 버전을 가리키거나 또는 Staging Area에 변경된 내용이 있다면 그것이 이전 버전일 수도 있다.
- b 라고 하는 것은 `지금 버전`을 의미

```
git diff --staged : Staging Area에 있는 것을 확인 하고 싶을 때
git diff --cached(동의어)
```

## `6. 버전 등록하기(commit)`

- Staging Area에 있는 변경사항을 Git Repository에 옮겨 주는 역할을 한다.
- 사용법

```
git commit -m "메시지 작성"
```

- Working directory에 있는 모든 변경 사항이 마음에 들어 그래서 `add` 라는 것을 굳이 사용 하지 않고도 바로 `commit` 할 수 있다.
- 사용법

```
git commit -a -m "메시지 작성"
git commit -am "메시지 작성"
 : 여기서 -a의 a는 all(Working directory, Staging area)를 의미.
```

> 커밋할때 팁 💯
>
> - 열심히 만들어서 commit해 나가는 Git Repository에는 어떤 규모의 commit이 적당할까?  
>   : Git Repository는 우리의 commit(작업)들을 버전별로 나누어서 관리할 수 있는 `창고(history)이다`. 그렇기 떄문에 전체적인 어플리케이션을 만들어서 하나의 commit으로 저장하게되면 아무런 의미가 없다. 어플리케이션을 조금 더 세분화해서 `기능별로 작은 단위로 만들어 나가는 것이 중요`, 그리고 `의미 있는 이름을 지정해서` 히스토리를 바라봤을 때 작업한 내용도 빠르게 확인해 볼 수 있고, 내가 원하는 변경사항을 빠르게 찾아서 자세히 확인해 볼 수 있고,
>   또 원하지 않는 commit을 취소하기가 편하다.
> - 보통 commit의 -m(메세지)는 현재형과 동사로 만들어진다.
> - 만약 commit을 할때 `crash를 고쳤다고 하면 정말 그 고친 내용만 포함한 commit을 만들어야한다.` 하는김에 다른 버그도 하나 고치고 리펙토링도 하고 새로운 기능도 추가해서 commit을 하면 혼동이 오기 떄문이다.

## `7. 버전들 목록 보기(log)`

- git 버전 히스토리를 간편하게 볼 수 있는 명령어
- 사용법

```
1. git log

ex)
commit e9ca0b5f309ff81753655854acab9775632f6751 (HEAD -> main)
Author: gang-min <rudals8920@naver.com>
Date:   Sat Aug 28 22:09:23 2021 +0900

    3

commit ac1326c8d70a164f803e05758d510409dcb985c1
Author: gang-min <rudals8920@naver.com>
Date:   Sat Aug 28 22:09:11 2021 +0900

    2

commit 9276a007362d590478efce538cf880fe358c3b1a
Author: gang-min <rudals8920@naver.com>
Date:   Sat Aug 28 22:08:53 2021 +0900

    1

------------------------------------------------------
2. git log -p(patch) : -p옵션을 쓰면 수정된 파일의 내용들도 확인해 볼 수 있다.
------------------------------------------------------
3. git log --oneline : 간편하게 해쉬코드의 앞자리 문자열과 간단한 commit 메시지도 확인가능하고 HEAD가 가리키고있는 위치도 알 수 있다.
ex)

e9ca0b5 (HEAD -> main) 3
ac1326c 2
9276a00 1
------------------------------------------------------

```

- 여기에서 `HEAD`라는 것은 지금 내가 있는(내가 바라보는)이 시점에 버전을 가리킨다.
- 만들어진 commit들은 언제든지 내가 원할 때 원하는 시점으로 돌아갈 수 있다. \* 만약 commit 2 로 돌아 가고 싶다면 `git checkout 2의해쉬코드 또는 HEAD~1`하면 된다.
  > [[git] 과거로 갔다가 돌아 오기](https://mytory.net/archives/10078)
- 위에 있을수록 최근에 commit한 log이다. 방향키를 이용해서 아래로 내려가면 제일 처음에 commit한것까지 볼 수 있다.

## `8. 태그는 왜 필요할까?(tag)`

- git 히스토리에 commit들이 점점 더 많아기지 시작한다면 git log가 굉장히 길어진다면 어떤 특정한 부분으로 돌아가고 싶을때 어려울 수 있다.
- 어떤 특정한 commit을 `북마크` 해두고 싶을 때 쓸 수 있는 것이 바로 `git tag`이다.

  - 이렇게 특정한 commit을 tag를 해놓음으로써 내가 원하는 부분으로 빠르게 전환할 수 있는 큰 장점이 있다.
  - 내가 원하는 문자열을 사용해서 tag를 이용해도 되고 대부분의 경우에는 우리가 제품을 릴리즈 할 때 그 버전을 tag를 많이 해 놓는다.
    - 대부분 Semantic Versioning 시스템을 따라가는데 `v2.0.0`에서 2(major).0(minor).(fix)로 구분해서 정한다.

- 사용법

```
git tag v1.0.0 <tag를 달고싶은 commit 해쉬코드>
---------------------------------------------------
* 이 버전에는 어떤 기능들이 포함이 되어 있는지 상세하게 작성하고 싶을 때
git tag v1.0.0 <해쉬코드> -a(annotate) -m "정보 작성"
---------------------------------------------------
* Repository에 있는 모든 tag들을 확인해 보고 싶다면
git tag
---------------------------------------------------
* tag 삭제
git tag -d <tagName(v1.0.0)>
```

- 만들어진 tag는 언제든지 git checkout 이라는 명령어를 이용해서 그 tag로 이동이 가능하다.

## `9. 전환(checkout)`

- Git 용어로 "checkout"은 대상 개체가 가지고 있는 버전들에서 원하는 버전으로 전환하는 것이다. `git checkout` 명령은 세개의 개체 `파일, 커밋, 브랜치`에 대한 동작이다.
- 사용법

```
git checkout <파일명>
git checkout <commit 해쉬코드>
git checkout <브랜치명>
  * git checkout -b(branch) (만들고자하는 브랜치명): 새로운 브랜치를 만들면서 동시에 바로 그 브랜치로 이동됨.
git checkout (tagName)
```

# `Branch`

## `1. 브랜치를 왜 꼭 써야 할까?`

- Git에서 따로 지정을 하지 않는 이상 `main branch`가 기본적으로 쓰인다. 즉 별도로 branch를 따로 만들지 않으면 이 main 한줄기에서 걔속 commit이 발생이 되고, 보통 main branch는 코드가 검증이 되고 기능에 문제가 없는 정확하게 검증된 제품에 포함이 되어도 되는 내용들만 포함이 되어져 있디.
- 만약 새로운 기능인 Feature A를 개발한다고 한다면 main branch에서 바로 작업을 하기 보다는 Feature A라는 branch를 새로 만들어서 거기에서 commit을 해 나가는 것이 좋다.

* 기능별로 리팩토링별로 또는 버그픽스별로 branch를 만들어서 일을 하게되면 동시다발적으로 다수의 branch 위에서 다수의 개발자가 개발을 해 나갈 수 있기 때문에 `병렬적으로 업무를 진행`할 수 있는 큰 장점이 있다.
* 이렇게 branch 위에서 따로 개발을 하다가 이제 Feature A의 branch가 제품에 포함이 될 준비가 되었다면 `main branch로 merge 할 수가 있다.`
  merge가 완벽하게 이루어졌다면 이제 Feature A branch는 더 이상 필요없으므로 Feature A branch는 삭제를 한다.
* 이렇게 branch 위에서 했던 commit들을 그대로 main branch에 전부 다 merge 하는 경우도 있지만 대부분은 이런 Feature A에서 작업했던 히스토리가 main branch에 더럽게 다 merge 될 필요가 없기 떄문에` Feature A의 commit들을 합해서(스쿼시드) 새로운 하나의 commit을 만든 다음에 그 commit만 깔끔하게 main branch로 가져오는 방법`도 있다.

## `2. 브랜치 기본 사용법`

- 사용법

```
git branch : 내컴퓨터(Local)에 있는 현재 repository에 있는 branch들 확인 가능
git branch --all : 원격 Github과 같은 서버와 연결된 repository에 있는 모든 branch들 확인 가능
git branch <만들고자하는 브랜치명> : 새로운 branch 만들기
    - git switch <이동하고자하는 브랜치명>: branch로 이동할 때
    - git switch -C <만들고자하는 브랜치명> : 새로운 branch를 만들고 곧 바로 그 branch로 이동
git branch --merged : 현재 branch에 merge가 된 brach들을 확인 가능
git branch --no-merged : 현재 branch에 merge가 되지 않은 branch 확인 가능
git branch -d <지우고싶은 브랜치명> : branch 삭제
git branch --move (바꾸고싶은 브랜치명) (바꿀 브랜치명) : branch명 변경

```

- `switch`와 비슷한 명령어는 위에서 공부한 `checkout`이다.

## ` 3. 머지란? (fast-forward merge, Three-way merge)`

## `3-1 fast-forward merge`

- `fast-forward merge` 같은 경우는 main(master) branch에서 `새로운 branch가 생성된 이후에 main branch의 변동사항이 없다면` fast-forward merge로 된다.

* 사용법

```
git merge <merge할 branch명>

merge 완료후

git branch -d <merge한 branch명>

merge가 된 branch는 삭제해주는 것이 좋다.

```

![fast-forward merge](/image/fast-forward_merge.png)

![fast-forward merge](/image/fast-forward_merge2.png)

- `fast-forward merge` 같은 경우는 main(master) branch에서 `새로운 branch가 생성된 이후에 main branch의 변동사항이 없다면` merge를 할 때 단순히 main branch가 가리키고 있는 포인터를 d가 아닌 f로 옮겨 놓기만 하면 된다.

* 그리고 `branch(feature A)를 삭제`하면 깔끔하게` fast-forward merge`가 발생할 수 있다.
* fast-forward의 단점이라고 생각하면 단점일수도 있는데 히스토리에 merge가 되었다는 사실이 남지 않는다.(워낙 깔끔하게 merge가 되기 떄문에)
  > - `fast-forward가 가능하지만 Three-way merge방식으로 하는 방법`
  > - 사용법
  >
  > ```
  > git merge --no-ff(fast-forward) <merge할 branch명>
  >
  > merge 완료후
  >
  > git branch -d <merge한 branch명>
  >
  > merge가 된 branch는 삭제해주는 것이 좋다.
  > ```
  >
  > - 정말 순수하게 모든 것들을 히스토리에 남기길 좋아하는 사람(팀)이라면 이렇게 fast-forward가 가능해도 `따로 merge commit을 만든다`.
  > - 이렇게 `h라는 commit은 d와 f를 합한 새로운 commit`을 만들어서 main branch에 commit 하게 된다.
  >   ![fast-forward merge](/image/merge-commit.png)

## `3-2 Three-way merge`

- `Three-way merge` 같은 경우는 main(master) branch에서 `새로운 branch가 생성된 이후에 main branch의 변동사항이 있다면` fast-forward merge는 불가능하고 three-way merge를 이용해야 한다.
- `즉, 베이스 branch인 main branch와 파생된 feature A branch의 변동사항을 모두 합해서 merge commit을 만든 다음에 main branch에 commit을 해야 한다.`
- 사용법

```
(fast-forward merge와) 사용법은 같다.

git merge <merge할 branch명>
```

- 아무런 옵션없이 사용하게 되면 fast-forward가 가능한 경우라면 merge commit을 만들지 않고 fast-forward merge를 진행하고 만약 아래와 같이 `fast-forward merge가 불가능한 상황이라면 three-way merge를 진행한다`
  ![fast-forward merge](/image/three-way_merge.png)
  ![fast-forward merge](/image/three-way_merge2.png)

## `4. Conflict 해결 방법`

- git이 merge를 할 때 무언가 문제가 있어서 자동적으로 해결이 안 된 무언가 충돌이 났을 때 발생할 수 있다.
- 즉, 두 가지의 branch에서` 동일한 파일을 수정을 했다면 Git이 도대체 '어떤 내용을 추가해야 하는지' 혼동스러울 때` conflict가 발생한다.
- `⚠️⚠️동일한 파일, 동일한 위치(같은 내용 수정)여야함⚠️⚠️`
- 이런 경우에는 우리가 직접 수정을 해줘야 한다.
  ![conflict](/image/conflict.png)
- 만약 HEAD commit과 feature branch commit이 `동일한 파일 동일한 위치를 수정` 하였고 이때 `merge(git merge feature)`를 하려고 하면
  ![conflict](/image/conflict2.png)
- Auto-merging 자동으로 merging하려고 했으나 `Conflict`가 발생하였다.
  ![conflict](/image/conflict3.png)
- 발생한 파일의 내용을 보면 이렇게 알 수 없는 문자열이 추가된 것을 볼 수가 있다. 이제 이것은 `Git에서 merge conflict가 어디에서 발생했는지 우리에게 정보를 주기위해서` 자동으로 삽인된 문자열이다.

* merge하는 것을 취소하고 싶다면 `git merge --abort`

- `해결방법1`

```
Conflict가 발생한 파일을 직접 열어서 수동적으로 해결할 수도 있다.

merge conflict를 해결한 후

conflict를 해결했다고 알려주기 위해서

git add <conflict해결한 파일>을 한 다음에

git merge --continue를 하면 완료.

```

- `해결방법2`

* 우선 git config --global -e 을 열어서 아래 4줄을 추가해 준다.  
  ![conflict](/image/conflict4.png)

```
Conflict가 발생하면

git mergetool 명렁어를 입력하면 vscode가 열린다.

하나의 옵션을 선택하고 저장한 후 vscode를 끈다.

자동적으로 commit할 준비가 되어있다.(즉 add 생략)

이제 git merge --continue를 해주면 완료.
```

![conflict](/image/conflict5.png)

- 수동적으로 파일을 연것과 동일하게 문자열이 생성되어 있지만 4가지의 기능이있는 버튼들이 추가로 있다. 이것을 이용해서 간편하게 해결할 수 있다.
- Accept Current Change : 현재 있는 branch의 내용을 받아들이는 것
- Accept Incoming Change : 현재 branch로 merge될 branch의 내용을 받아들이는 것
- Accept Both Changes : 둘다 쓰는 것
- Compare changes : Current와 Incoming 차이점을 확인하고 싶을 때

* `⚠️⚠️merge conflict를 해결하는 것만 해야지 이왕 하는 김에 조금 다른 문장도 넣고 다른 코드도 넣고 은근슬쩍 변경사항을 넣는 것은 절대 안된다⚠️⚠️`

## `5. Rebase란 무엇일까? 왜 꿀일까? 🐝`

- 만약 나 `혼자서` 다른 branch에서 작업을 하고 있다면 언제든지 rebase를 자유롭게 할 수 있지만 만약에 `다른 개발자와 함께` 같은 branch에서 작업을 하고 있다면 rebase하는 것은 위험하다.
- 그이유는 e가 가리키고 있는 포인터를 d가 아니라 g로 변경해야 되는데 이렇게 포인터의 정보를 변경하게 되면 기존의 commit을 유지하는 것이 아니라 `commit은 불변의 진리이다.` 그래서 변경사항이 발생하면 새로운 commit을 만들게 된다. 그렇기 떄문에 겉으로는 똑같아 보이지만 실제로는 다른 e와 f commit이 생기기 떄문에
- 만약에 다른 개발자가 동일한 branch에서 작업을 하고 있다면 내가 rebase를 하고 push를 해서 서버에 변경된 정보를 업데이트하게 된다면 다른 개발자가 가지고 있는 feature A 의 e와 f는 전혀 다른 e'와 f' commit이기 떄문에 나중에 merge conflict가 발생할 수 있다.

### ⚠️⚠️그래서 rebase는 정말 유용하지만 다른 개발자와 함께 branch 위에서 작업을 하고 있고 이미 히스토리가 서버에 업로드 되어 있는 경우라면 `업로드된 히스토리는 절대 rebase하면 안된다.`⚠️⚠️

### ⚠️⚠️서버에 업데이트되지 않는 `나의 로컬에 있는 commit에 한에서는 rebase를 자유롭게` 해도 된다.⚠️⚠️

![Rebase](/image/rebase.png)
![Rebase](/image/rebase1.png)

- 사용법

```
git checkout feature A 로 간다음

git rebase main(master) 하면 main 제일 최신 commit에 rebase된다.

git checkout main 으로 다시 돌아와서

git merge feature A 하면

fast-forward merge로 깔끔하게 merge된다.

merge후 merge된 branch는 삭제
```

## `6. 필요한 커밋만 쏘옥~! 🍒 (cherry-pick)`

![cherry pick](/image/cherrypick.png)

- 만약 service branch에서 서비스를 개발하고 있는데 서비스 프로젝트중 딱 f commit 기능만 필요해서 main branch에 merge하고 싶을 때 `cherry pick`을 이용하면 된다.

- 사용법

```
git cherry-pick <가지고오고싶은 commit 해쉬코드>
```

![cherry pick](/image/cherrypick2.png)

- branch에서 작업 기간이 굉장히 오래걸리거나 또는 내가 특정한 commit을 가지고 오고 싶을 때 유용하게 사용할 수 있다.
