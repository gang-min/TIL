# Animation

> Contents
>
> 1. animation 개요
> 2. @keyframes
> 3. animation-name, animation-duration
> 4. animation-delay, animation-timing-function
> 5. animation-iteration-count, animation-direction
> 6. animation-play-state
> 7. animation-fill-mode
> 8. animation (shorthand)

## `1. animation 개요`

- CSS3 애니메이션은 엘리먼트에 적용되는 CSS 스타일을 다른 CSS 스타일로 부드럽게 전환시켜준다.

* 애니메이션은 애니메이션을 나타내는 CSS 스타일과 애니메이션의 중간 상태를 나타내는 키프레임들로 이루어진다.

* ### `animation 과 transition의 차이점`

  1.  transition은 시작하기 위해서 유저의 특정 액션(hove 라든지 class가 추가된다던지)이 필요하지만 animation은 유저의 특정 액션이 없어도 변경 될 수 있도록 자동으로 설정 할 수 있다.

  2.  transition은 A -> B로의 전환만 가능한데 animation은 A->B->C->A 등 내가 원하는 대로 custom 할 수 있다. 또 사이사이 의 시간도 내가 설정할 수 있다.

## `2. @keyframes (중간상태)`

- `@keyframes` @규칙은 개발자가 애니메이션 `중간중간의 특정 지점들을 거칠 수 있는 키프레임들을 설정`함으로써 CSS 애니메이션 과정의 중간 절차를 제어할 수 있게 한다. 이 룰은 브라우저가 자동으로 애니메이션을 처리하는 것 보다 더 세밀하게 중간 동작들을 제어할 수 있다.

* 키프레임을 사용하려면 `@keyframes` 룰을 애니메이션과 키프레임 리스트를 매칭시킬 `animation-name 속성`에서 사용할 이름과 함께 생성한다.

* 키 프레임 리스트가 유효하려면 최소한 0% 와 100% 같은 시간에 대한 규칙은 포함해야 한다.

> 0%, from === 시작 , 100%, to === 끝

- 만약 이 타임 오프셋이 정해져 있지 않으면, 키 프레임 선언이 무효가 된다.

- `중복 해상도`

  - 만약 한개의 이름에 대해서 여러개의 키프레임 셋이 존재하면, 파서가 마지막으로 마주치는 키프레임 셋만 유효하게 적용 된다.

  - 즉, 모든 속성이 각 키 프레임이 지정된 게 아니라 키 프레임이 여러번 정의 된 경우에는 가장 최근의 키 프레임에 선언된 값 들만 유효하다.

  * 아래의 예시에서는 50%키프레임에서 50% { top: 30px; left: 20px; }은 무시되고 50% { top: 10px; }만 적용된다.

  ```
   @keyframes identifier {
     0% { top: 0; }
     50% { top: 30px; left: 20px; }
     50% { top: 10px; }
     100% { top: 0; }
   }
  ```

* @keyframes의 애니메이션을 식별하는 이름은 대소문자 구분 문자 `a부터 z, 숫자 0부터 9까지, 밑줄(_) 및/또는 대시(-)의 조합으로 구성`된다. 대시되지 않은 첫 번째 문자는 문자여야 한다. 또한, 식별자 시작부분에 두개의 대시가 금지된다.

## `3. animation-name, animation-duration`

- ` animation-name`

  - 이 애니메이션의 중간 상태를 지정한다. 중간 상태는 @keyframes 규칙을 이용하여 기술한다.

  - initial 값은 none 이다.

  ```
  Syntax

  animation-name: @keyframes의 identifier;
  ```

* `animation-duration`

  - 한 싸이클의 애니메이션이 얼마에 걸쳐 일어날지 지정한다.

  - initial 값은 0s 이다.

  - 음수 값은 유효하지 않으므로 선언이 무시된다.

## `4. animation-delay, animation-timing-function`

- `animation-delay`

  - 엘리먼트가 로드되고 나서 언제 애니메이션이 시작될지 지정한다.4

  - animation-delay는 필수 값이다.

  - 시작 즉시, 잠시 후에, 또는 애니메이션이 일부 진행한 시점부터 시작할 수 있다.

  - initial 값은 0s 이다.

  - 양수 값은 지정된 시간이 경과 한 후 애니메이션이 시작되어야 함을 나타낸다. 기본값인 0의 값은 애니메이션이 적용되는 즉시 시작해야 함을 나타낸다.

  > `animation-duration과 다르게` 음수 값이 지정이 되지만 음수 값을 지정하면 애니메이션이 즉시 시작되지만 애니메이션 주기의 도중에 시작된다. 예를 들어 애니메이션 지연 시간으로 -1s를 지정하면 애니메이션이 즉시 시작되지만 애니메이션 시퀀스의 1초부터 시작된다.

* `animation-timing-function`

  - 중간 상태들의 전환을 어떤 시간간격으로 진행할지 지정한다.

  - 사용할 수 있는 값은 transition-timing-function과 동일하다.

  - initial값은 ease이다.

## `5. animation-iteration-count, animation-direction`

- ` animation-iteration-count`

  - transition은 한번 반복되고 끝나지만 animation은 반복횟수를 정할 수 있다. 심지어 무한히 반복도 지정 가능하다.

  - 애니메이션이 몇 번 반복될지 지정한다.

  - infinite로 지정하여 무한히 반복할 수 있다.

  - initial 값은 1이다.

  - `<number>`자료형으로 지정하면 횟수가 된다. (1 = 1회, 2 = 2회)

```
Syntax

/* Keyword value */
animation-iteration-count: infinite; // 무한대

/* <number> values */
animation-iteration-count: 3;
animation-iteration-count: 2.4;
```

- `animation-direction`

* 애니메이션이 종료되고 다시 처음부터 시작할지 역방향으로 진행할지 지정한다.

* animation-direction의 속성 값으로 normal, reverse, alternate, alternate-reverse 가 있다.

  1. normal (initial)

     : 애니메이션은 매 사이클마다 정방향으로 재생된다. 즉, 순환 할 때마다 애니메이션이 시작 상태로 재설정되고 다시 시작된다.

  2. reverse

     : 애니메이션은 매 사이클마다 역방향으로 재생된다. 즉, 순환 할 때마다 애니메이션이 종료 상태로 재설정되고 다시 시작된다. 애니메이션 단계가 거꾸로 수행되고 타이밍 기능 또한 반대로된다. 예를들면 ease-in 타이밍 기능은 ease-out형태로 변경된다.

  3. alternate

     : 애니메이션은 매 사이클마다 각 주기의 방향을 뒤집으며, 첫 번째 반복은 정방향으로 진행된다. (normal -> reverse -> normal -> reverse... 형태이다.)

  4. alternate-reverse

     : 애니메이션은 매 사이클마다 각 주기의 방향을 뒤집으며, 첫 번째 반복은 역방향으로 진행된다. (reverse -> normal -> reverse -> normal... 형태이다)

## `6. animation-play-state`

- 애니메이션을 멈추거나 다시 시작할 수 있다.

- animation-play-state의 속성값으로 paused, running이 있다

- initial값은 running이다.

* running은 현재 재생 중을 뜻하고 paused는 현재 일시 중지를 뜻한다.

* 별도의 javascript나 css hover와 같은 것들로 제어할 수 있다.

> ⚠️⚠️일시 중지된 애니메이션을 다시 시작하면 애니메이션 시퀀스의 처음부터 다시 시작하지 않고 일시 `중지된 시점`에서 애니메이션이 시작된다.

## `7. animation-fill-mode`

- 애니메이션이 시작되기 전이나 끝나고 난 후 어떤 값이 적용될지 지정한다.

* animation-fill-mode의 속성 값으로 none, forwards, backwards, both가 있다.

  1. none

     : 애니메이션은 실행되지 않을 때 대상에 스타일을 적용하지 않는다. 즉, @keyframes에 정의한 스타일 말고 자기가 원래 가진 스타일만 그대로 가지고 @keyframes스타일은 적용하지 않는다. animation이 재생 될 떄만 @keyframes의 스타일을 쓸 수 있다.

     : 쉽게 말하면 animation이 끝나면 원래 본인의 스타일로 돌아온다 라는 뜻이다.

     ![애니메이션](/image/애니메이션.png)

  2. forward

     : 대상은 실행 된 애니메이션의 마지막 keyframe에 의해 설정된 계산 된 값을 유지한다.

     ![애니메이션](/image/애니메이션2.png)

     : animation이 끝나면 본인의 원래 스타일로 돌아오는 것이 아니라 keyframes에 마지막에 설정된 스타일이 유지된다 라는 뜻이다 (단, animation-direction및 animation-iteration-count의 값에 따라 다르다. )

     ![animation](/image/animation.png)

  3. backwards

     : 애니메이션은 대상에 적용되는 즉시 첫 번째 관련 keyframe 에 정의 된 값을 적용하고 `animation-delay 기간 동안 이 값을 유지`한다. (단, 첫 번째 관련 키프레임은 animation-direction의 값에 따라 다르다.)

     ![animation](/image/animation2.png)

     - 즉, 1번의 기존스타일부터 시작하는게 아니라 1번을 제외한 2번부터 시작이 된다.

     ![애니메이션](/image/애니메이션3.png)

  4. both

     : 애니메이션은 앞뒤 양쪽 모두의 규칙을 따르므로 애니메이션 속성이 양방향으로 확장된다. 즉 forwards와 backwards 둘 다 적용이 된다.

     : 즉, 2,3,4 만 되고 기존스타일의 1,2는 아예 제외된다.

     ![애니메이션](/image/애니메이션4.png)

* initial값은 none이다.

## `8. animation (shorthand)`

- animation CSS 속성은 다수의 스타일을 전환하는 애니메이션을 적용한다.

* . animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode, animation-play-state의 단축 속성이다.

* 각각의 initial값들을 다시 한번 확인 해보자. 작성하지 않은 값들은 initial값들로 적용된다.

![애니메이션](/image/애니메이션5.png)

```
/* @keyframes duration | timing-function | delay |
iteration-count | direction | fill-mode | play-state | name */
animation: 3s ease-in 1s 2 reverse both paused slidein;

/* @keyframes duration | timing-function | delay | name */
animation: 3s linear 1s slidein;

/* @keyframes duration | name */
animation: 3s slidein;
```

> ⚠️⚠️순서는 상관없지만 transition과 마찬가지로 둘다 시간을 사용하는 속성이기 떄문에 animation-duration과 animation-delay의 `순서가 중요`하다. 첫 번쨰에 위치한 속성을 animation-duration 두 번쨰에 위치한 속성을 animation-delay로 한다.
