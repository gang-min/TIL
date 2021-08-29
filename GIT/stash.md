# Stash

> Contents
>
> - Stash란 무엇이고 왜 중요할까?

# `1. Stash란 무엇이고 왜 중요할까?`

- git workflow에서 열심히 `Working Directory`에서 일을 하다가 마음에 들면 `Staging area`에 옮겨 놓고 이것들을 commit을 이용해서 `.git directory(git repository)`에 저장하게 된다. 이렇게 저장하게 된 commit들은 `(git history,git repository)`에 남기게 된다.

- 만약 Working Directory에서 작업을 하고 있는데 아직 commit할 단계는 아니여서 Staging area로 옮기진 않았다. 그때 만약 다른 작업을 해야할 상황이 온다면 어떻게 해야 할까...
- `이떄 유용하게 쓸 수 있는 것이 바로 Stash 이다.` stash를 이용하면 git history에 저장 하지 않고도 작업하는 내용들을 잠시 저장해 둘 수 있다.

- 갑자기 다른상황이 생긴다면 준비되지 않은 파일을 commit 하기보다는 stash command를 이용해서 stash에 잠시 저장을 해 두고 다시 내가 원하는 순간에 stash에 있는 내용들을 다시 working directory로 가지고 올 수 있다.
- `내가 잠시 작업하고 있는 내용들을 저장해두고 branch 전환을 위해서 쓸 수도 있고, 또는 내가 버그를 고치고 있는데 각각의 시도를 잠시 저장해두고 싶다면 이럴때도 stash가 유용하게 쓰일 수 있다.`
  ![stash](/image/stash.png)

* stash 저장하는법

```
1. working directory와 staging area에 있는 모든 것이 stash에 저장된다.

git stash push : 아무런 타이틀이 없이 저장이 된다.
git stash push -m "메시지작성": 타이틀 작성 후 저장
----------------------------------------------------------------
2. working directory와 staging area에 있는 모든 것이 stash에 저장되지만 staging area에 있는 것을 유지하면서 stash에 저장하고 싶다면

git stash push -m "메시지작성" --keep-index
----------------------------------------------------------------
주의 : 새로만든 파일(즉, untracked)은 stash에 저장되지 않는다.
3. 아직 tracking 되지 않는 파일들도 stash에 저장 하고 싶다면

git stash push -u(untracking)
```

- stash 저장 목록 확인 방법

```
git stash list

ex)
stash@{0}: WIP on main: 4e0f857 asdasd
stash@{1}: WIP on main: 4e0f857 asdasd
stash@{2}: WIP on main: ed322f2 Merge branch 'test'
----------------------------------------------------------------

각각 stash에서 어떤 것이 수정 되었는지 확인하고 싶다면
git stash show stash@{2}(확인하고싶은 stash id)

git stash show stash@{2} -p : 조금 더 자세하게
```

- 다시 working directory로 불러 오고 싶다면
  1. `git stash apply`는 stash를 불러 오지만 `stash list 는 그대로 유지`
  2. `git stash pop`을 이용하게되면 stash를 불러옴과 `동시에 stash list에서도 삭제`

```
git stash apply : apply뒤에 아무것도 작성하지 않으면 제일 위에있는 stash가 불러와짐

git stash apply stash@{2}(불러오고싶은 stash id) : 특정한 stash를 불러오는 방법
----------------------------------------------------------------
git stash pop : pop뒤에 아무것도 작성하지 않으면 제일 위에있는 stash가 불러와짐

git stash pop stash@{2}(불러오고싶은 stash id) : 특정한 stash를 불러오는 방법
```

- stash에서 삭제하는 방법

```
git stash drop stash@{2}(삭제하고싶은 stash id)

git stash clear : 전체 삭제
```
