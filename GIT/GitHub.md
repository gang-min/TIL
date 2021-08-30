# GitHub 사용하기

> Contents
>
> 1.  GitHub의 필요성
> 2.  원격 저장소란? (Remote Repository)
> 3.  Git으로 프로젝트를 server로 연결하는 2가지 방법  
>      3-1. 이미 진행중인 프로젝트에 참여 `(clone)`  
>      3-2. 프로젝트를 최초 시작 `(remote add)`
> 4.  local에 있는 commit을 server에 저장하기 `(push)`
> 5.  fetch Vs pull 차이점

# `1. GitHub의 필요성`

- `git`은 나의 `Local환경(내 컴퓨터)`에서 git repository를 생성하고 history를 만든다.

* git의 큰 특징이자 장점은 `distributed(분산형)` 시스템이다. server에만 정보가 모여있는 중앙집중식과는 다르게 각각의 개발자들이 history를 local에 가지고 있음으로써 서로 공유할 수도 있고 또 문제가 생겼을 때 복원이 가능하고 오프라인에서 작업할 수 있는 큰 장점도 있다.

- Local환경에서만 git repository를 만들고 간직하다가 내 PC에 문제가 생기거나 다른 환경에서 작업을 하고 싶을 때 repository에 접근이 불가능하다.
- ❗️❗️이것을 방지하고 다른 사람들과의 협업을 위해서 `remote라는 server에` 나의 git repository를 업로드해두어서 항상 다른 PC에서도 접근이 가능하고 다른 개발자들과 함께 일을 할 수 있도록 하기 위해서 server를 이용한다.

```
.git repository(local repository) === 로컬 저장소

remote repository(server repository) === 원격저장소
```

![github](/image/github.png)

# `2. 원격 저장소란? (Remote Repository)`

- `원격 저장소`란` 내 로컬PC 저장소가 아닌 네트워크상의 다른 위치에 존재하는 Git 저장소`를 말합니다. 여기서 네트워크상의 어딘가는 인터넷상일 수도 있고 우리팀의 사설 네트워크상의 위치일수도 있습니다.

* 원격 저장소는 어디에?  
   : Git의 원격 저장소는 네트워크상 어딘가에 존재한다고 했는데, 인터넷을 통해 원격 저장소 공간을 제공해주는 서비스들이 있습니다.

  대표적인 원격 저장소 서비스로는 `GitHub`, GitLab 등이 있는데, 이런 Git 서비스들은 원격 저장소 공간을 인터넷 상에서 제공하며, 각각의 정책에 따라 공개 저장소와 비공개 저장소를 유료 또는 무료로 제공하고 있습니다.
  ![github](/image/github2.png)

# ` 3. Git으로 프로젝트를 server로 연결하는 2가지 방법`

- Git으로 프로젝트를 관리하는 경우 두 가지 프로세스가 있습니다.

* 첫 번재 프로세스는 이미 진행중인 프로젝트에 참여하게 되는 경우인데 팀원들이 Git을 통해 프로젝트를 진행하고 있었다면 이미 원격 저장소가 만들어져 있을 것이므로 이것을 내 로컬 PC의 Git 저장소로 복사(Clone) 하는 경우입니다.
* 두 번째 프로세스는 프로젝트를 최초 시작하면서 내 로컬에 Git 저장소를 만들어 작업하다가 협업을 위해 원격 저장소를 만들고 작업 내역을 업로드 하는 것입니다.

## 3-1. 이미 진행중인 프로젝트에 참여 `(clone)`

![clone](/image/clone.png)

- 이미 진행중인 프로젝트가 있는 `Remote Repository(원격저장소)`를 들어가보면 이렇게 전체적인 메뉴와 옵션들을 확인해 볼 수 있다.

![clone](/image/clone2.png)

- server에 있는 repository를 나의 local로 가지고 오고싶다면 우측 상단에 있는 Code를 눌러보면 git을 clone할 수 있는 주소가 나온다.

![clone](/image/clone3.png)

- 주소를 복사하여 terminal을 열고 `git clone <복사한 주소>`를 하게 되면 저장소 복제가 성공적으로 진행된다.

```
git clone [REPO_URL] [DIR]
```

- 특별한 이유가 없다면 보통 [DIR]을 생략하는데 생략하게되면 server repository의 이름의 폴더안에 clone이 되고 [DIR]을 따로 작성해주게 되면 작성한 [DIR]이름으로 폴더가 만들어져 그 안에 clone이 된다.

* ❗️❗️ 또한, 저장소를 Clone 하면 `origin`이라는 `리모트 저장소`가 자동으로 등록되기 때문에 `origin`이라는 이름을 볼 수 있다.

> Remote / Origin
>
> - 우선 `Remote`는 말 그대로 리모트 서버 자체를 의미한다.
>
> - Git을 사용할 때는 내가 어떤 리모트 서버에 변경 사항을 업로드 할 것인지 정해야하는데, 반드시 하나의 리모트 서버만 사용할 수 있는 것이 아니기 때문에 `내가 사용하는 리모트 서버의 이름을 정해줘야한다`. 이때 주로 사용하는 관례적인 이름이 바로 `Origin`이다.

- server에 관련된 정보를 확인 하려면 git remote 명령어를 사용하면 된다.

![remote](/image/remote.png)

## 3-2. 프로젝트를 최초 시작 `(remote add)`

- 내 로컬에 Git 저장소를 만들어 작업하다가 협업을 위해 원격 저장소를 최초로 만들면 아래와 같이 나온다.

![remote](/image/remote2.png)

- git clone과 다르게 최초 시작할 떄는 `remote를 수동적으로 연결`해줘야 한다.

```
git remote add origin [REPO_URL]
```

- 여기서 origin은 remote의 이름이다 보통 관례로 origin으로 쓴다.

# `4. local에 있는 commit을 server에 저장하기 (push)`

- Local 개인 작업을 팀원들에게 공유하기 위해 작업 내용을 Remote repository에 업로드해야 한다.
- 이 때 사용하는 명령어가 `Push` 이다.

* 사용법

```
git push [remote name] [remote branch]

ex)

git push origin main
: origin이라는 이름의 remote의 main branch에 push 하겠다.
```

# `5. fetch Vs pull 차이점`

![pull](/image/pull.png)

```
git pull [remote name] [remote branch]
```

- server에 새로운 commit이 발생해서 `pull`를 이용하는 경우에는 server에 있는 history를 가지고 오면서 나의 local에 있는 내용을 함께 `merge`한다.

- 그래서, 나의 main과 origin/main이 동시에 C를 가리키고 있다.

* pull은 나의 local버전도 server와 함께 동일하게 만들고 싶을 때 사용한다.

![fetch](/image/fetch.png)

```
git fetch [remote name] [remote branch]
```

- server에 새로운 commit이 발생해서 `fetch`를 이용하는 경우에는 server에 있는 git history를 받아와서 나의 git history를 업데이트 하게 된다.

* ❗️❗️ 하지만, `fetch`는 history를 업데이트 하지만 내가 현재 바라보고 있는 작업환경 HEAD는 그대로 유지가 된다. 즉, history는 이제 C라는 commit을 가지고 있지만 여전히 나의 local main(mater) branch는 여전히 B를 가리키고 있다.

* `fetch 후 git merge origin/main을 하게 되면 git pull 상태와 같아진다.`
* fetch는 내가 server에 있는 history 정보를 업데이트해서 server에서 어떤 일등이 지금 발생하고 있는지, 누가 어떤 일을 했는지 확인하고 싶은 경우에 많이 쓴다.

## `fetch와 pull의 차이점`

: `pull은 받아옴과 동시에 local과 merge를 하지만, fetch는 받아오기만 할뿐 merge하지 않는다.`
