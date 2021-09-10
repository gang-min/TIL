# Transition

> Contents
>
> 1. transition (전환) 개요
> 2. transition - property, transition-duration
> 3. transition - delay, transition-timing-function
> 4. transition (shorthand)

## `1. transition (전환) 개요`

- CSS 트랜지션은 CSS 속성을 변경할 때 애니메이션 속도를 조절하는 방법을 제공한다.

- 속성 변경이 즉시 영향을 미치게 하는 대신, 그 속성의 변화가 일정 기간에 걸쳐 일어나도록 할 수 있다. 예를 들어, 여러분이 어떤 요소의 색상을 흰색에서 검은색으로 변경한다면, `변화는 대개 즉시 일어나는데 CSS 트랜지션을 이용하면, 모두 커스터마이즈 가능한 어떤 가속도 곡선을 따르는 시간 주기마다 변화가 일어난다.`

* CSS transitions는 여러분이 (명시적으로 목록을 작성해서) `어떤 속성을 움직이게 할지`, (딜레이를 설정해서) `언제 애니메이션이 시작할지`, (지속 시간을 설정해서) `트랜지션을 얼마나 지속할지`, 그리고 (예를 들면, 선형이거나 초기 빠름, 종료 느림과 같은 타이밍 함수를 정의해서) `어떻게 트랜지션을 실행하는지 결정`하게 한다.

* 이 속성으로 엘리먼트의 두 가지 상태 사이에 변화를 줄 수 있다.

* 엘리먼트의 각 상태는 가상 클래스 를 사용해 정의된 :hover 이나 :active 또는 자바스크립트를 사용해 동적으로 만들어진 것들이다.

## `2. transition - property, transition-duration`

- `transition-property`

  - 전환 효과를 적용해야 하는 CSS 속성을 설정한다.

  ```
  예시)

  div{
    background-color: red;
    transition-property:background-color;
  }

  div:hover{
    background-color-blue;
  }

  //  transition-property:background-color;는 div에 hover하였을 때 background-color색을 red -> blue로 바꾸려고 할 때 background-color 즉, 바꾸려고 하는 속성이 property가 된다.
  ```

* transition-property의 `initial값은 all`이다.

  - all은 어떤 css속성이든 모두 변경하겠다 라는 의미이고, 특정 css만 바꾸고 싶다면 바꾸고 싶은 css property를 작성하면 된다.

  - (,)를 이용하여 여러 개의 css property도 작성 가능하다.

* `transition-duration`

  - transition animation이 완료되는 데 걸리는 시간을 설정한다.

  - transition-duration의 `initial값은 0s` 이므로 작성하지 않으면 animation이 발생하지 않는다.

  * 속성값은 s(second) 와 ms(millisecond)가 있다. 1초는 1s를 뜻하고 millisecond로 하면 1000ms가 된다.

```
  예시)

  div{
    background-color: red;
    transition-property:background-color;4
    transition-duration:0.5s;
  }

  div:hover{
    background-color-blue;
  }

  // 즉, transition-duration:0.5s;은 background-color를 변경하는데 걸리는 시간을 0.5초로 하겠다 라는 뜻이다.
```

## `3. transition - delay, transition-timing-function`

- `transition-delay`

  - transition될 속성이 transition 요청을 받은 이후 실제로 transition하기 까지 기다려야 하는 시간의 양을 지정한다.

  - transition-delay의 `initial 값은 0s`이다.

    - 즉, transition-delay:1s; 이면 1초 지연되다가 transition이 발생된다.

* `transition-timing-function`

  - transition효과의 영향을 받는 CSS 속성에 대한 중간값을 계산하는 방법 (예를 들면, 선형이거나 초기 빠름, 종료 느림과 같은 타이밍 함수를 정의해서)을 설정한다.

  - 기본적으로, 이를 통해 전환 속도가 지속 시간에 따라 달라질 수 있도록 가속 곡선을 설정할 수 있다.

  * 이 가속 곡선은 전환될 각 속성에 대해 하나의 `<easing-function>`를 사용하여 정의된다.

  * transition-timing-function의` initial 값은 ease`이다.

  ```
   transition-timing-function: ease;
  ```

  - `<easing-function>`

    - ease : cubic-bezier(0.25, 0.1, 0.25, 1.0)와 같으며 전환 중간을 향해 속도가 증가하여 마지막에 속도가 느려진다. (default)

    * linear : cubic-bezier(0.0, 0.0, 1.0, 1.0)와 같으며 일정한 속도로의 전환

    * ease-in : cubic-bezier(0.42, 0, 1.0, 1.0)와 같으며 완료될 때까지 전환 속도가 증가하면서 서서히 시작된다.

    * ease-out : cubic-bezier(0, 0, 0.58, 1.0)와 같으며 빠른 전환을 시작하고, 느린 전환을 계속한다.

    * ease-in-out : cubic-bezier(0.42, 0, 0.58, 1.0)와 같으며 느리게 전환하기 시작하고, 속도를 높인 다음, 다시 느려진다.

    * cubic-bezier(p1, p2, p3, p4) : 작성자 정의 방법 여기서 p1 및 p3 값은 0에서 1 사이여야 한다.

  > 이 사이트를 이용하면 내가 원하는 cubic-bezier(p1, p2, p3, p4)를 쉽게 만들 수 있다.

  - [cubic-bezier(p1, p2, p3, p4)](https://matthewlein.com/tools/ceaser)

## `4. transition (shorthand)`

- transition CSS 속성은 transition-property, transition-duration, transition-timing-function 과 transition-delay를 위한 단축 속성 이다.

* 다시한번 작성하지 않았을 떄의 initial값을 보면 아래와 같다.

  ![transition](/image/transition.png)

* 둘다 `시간을 사용하는 속성`이기 떄문에 transition-duration과 transition-delay의 `순서가 중요`하다.

* 첫 번쨰에 위치한다면 transition-duration로 적용되고 두 번째에 위치한다면 transition-delay로 적용된다.

* 즉 시간이 하나밖에 없다면 무조건 duration으로 적용되고 둘 있다면 첫 번쨰가 duration 두 번쨰가 delay가 된다.

```
/* Apply to 1 property */
/* property name | duration */
transition: margin-left 4s;

/* property name | duration | delay */
transition: margin-left 4s 1s;

/* property name | duration | timing function | delay */
transition: margin-left 4s ease-in-out 1s;

/* Apply to 2 properties */
transition: margin-left 4s, color 1s;

/* Apply to all changed properties */
transition: all 0.5s ease-out;
```
