# Flexbox

> Contents
>
> 1. Flexbox 개요
> 2. 용어 - flex container, flex item, main axis, cross axis
> 3. Container - display
> 4. Container - flex direction
> 5. container - flex-wrap, flex-flow (shorthand)
> 6. item - order
> 7. item - flex-grow
> 8. item - flex-shrink
> 9. item - flex-basis
> 10. item - flex (shorthand)
> 11. Container - justify-content
> 12. Container - align-items
> 13. Container - align-content
> 14. item - align-self

## `1. Flexbox 개요`

- `flexbox`라 불리는 Flexible Box Module이 나오기 이전에 가로배치(레이아웃)를 하고 싶다면 `inline-block`을 쓰거나 `float` 속성을 썼다. 하지만, `inline-block`은 개행에 의한 item들간의 스페이싱 공간이 생겨서 우리가 원하는 정렬이 되지 않았고, `float`도 주는 순간 부모로부터 둥둥 부유하게되어 부모가 높이를 잃게되거나 하는 불편함이 있었다.

- 그래서 이를 해결하고 조금 더 쉽게 레이아웃을 만들기 위해서 ` flexbox`가 등장하였다.

- 일명 flexbox라 불리는 Flexible Box module은 flexbox 인터페이스 내의 아이템 간 공간 배분과 강력한 정렬 기능을 제공하기 위한 1차원 레이아웃 모델 로 설계되었다.

- flexbox를 1차원이라 칭하는 것은, 레이아웃을 다룰 때 `한 번에 하나의 차원(행이나 열)만을 다룬다`는 뜻이다.

> 이는 행과 열을 함께 조절하는 `CSS 그리드 레이아웃`의 2차원 모델과는 대조된다.

## `2. 용어 - flex container, flex item, main axis, cross axis`

- `flex container`, `flex item`

  - 문서의 영역 중에서 flexbox가 놓여있는 영역을 flex 컨테이너 라고 부른다.

  - flex-container를 생성하려면 영역 내의 컨테이너 요소의 `display 값을 flex`로 지정한다.

  - 이 값이 지정된 컨테이너의 `일차 자식(direct children)요소`가 `flex-item`이 된다.

  ![flex-container](/image/flex-container.png)

  - display: flex 속성만 지정하여 flex 컨테이너를 생성하면 다른 flex 관련 속성들은 아래처럼 기본값(initial)이 지정된다.

    - 항목은 행으로 나열된다. (flex-direction : row;)

    - 항목은 주축의 시작 선에서 시작한다.

    - 항목은 주 차원 위에서 늘어나지는 않지만 줄어들 수 있다.

    - 항목은 교차축의 크기를 채우기 위해 늘어난다. (align-items : stretch;)

    - flex-basis : auto;

    - flex-wrap : nowrap;

* `main axis(주축)`, `cross axis(교차축)`

  - flexbox를 다루려면 `주축`과` 교차축`이라는 두 개의 축에 대한 정의를 알아야 한다.

  - 주축은 `flex-direction`에 의해 정의되며 4개의 속성 값을 가질 수 있다.

  ```
  flex-direction: row (initial)

  flex-direction: row-reverse

  flex-direction: column

  flex-direction: column-reverse
  ```

  - row 혹은 row-reverse를 선택하면 `main-axis(주축)`은 페이지 좌측에서 우측으로 `인라인 방향 (행)`을 따르고

    ![row-main-axis](/image/row-main-axis.png)

  - 자동적으로 row 혹은 row-reverse를 선택하면 `cross-axis(교차축)`은 `블록 방향 (열)`이 된다.

    ![row-cross-aixs](/image/row-cross-aixs.png)

  - column 혹은 column-reverse를 선택하면 `main-axis(주축)`은 페이지 상단에서 하단으로 `블록 방향 (열)`을 따른다.

    ![column-main-axis](/image/column-main-axis.png)

  - 자동적으로 column 혹은 column-reverse를 선택하면 `cross-axis(교차축)`은 `인라인 방향 (행)`이 된다.

    ![column-cross-aixs](/image/column-cross-aixs.png)

> flexbox는 주축,교차축을 따라 항목을 정렬하고 끝을 맞추는 각종 속성들을 적용하는 방식으로 동작한다. 따라서 어느 축이 어느 방향인지 이해하는 것이 중요하다.

## `3. Container - display`

- display CSS 속성은 요소를 블록과 인라인 요소 중 어느 쪽으로 처리할지와 함께, 플로우, 그리드, 플렉스처럼 `자식 요소를 배치할 때 사용할 레이아웃을 설정`한다.

- display: inline | inline-block | block; 과 같은 아이들은 `<display-outside>(바깥쪽)` 자료형에 해당하고 display : flex | grid ; 과 같은 아이들은 `<display-inside>(안쪽)` 자료형에 해당한다. 따라서 두 자료형을 다른 개념으로 생각하는 편이 더 쉽다.

* [display - MDN](https://developer.mozilla.org/ko/docs/Web/CSS/display)

```
과거에는 바깥쪽 과 안쪽을 같이 설정 하고 싶을때는

.container{
  display: inline flex;
}

이런 식으로 하였는데 요즘은

.container{
  display: inline-flex;
}

이렇게 한번에 바깥쪽 과 안쪽을 설정 할 수 있다.container
```

## `4. Container - flex direction`

- flex-direction CSS 속성은 플렉스 컨테이너 내의 아이템을 배치할 때 사용할 주축 및 방향(정방향, 역방향)을 지정한다.

* flex-direction의 initial값은 row이다.

* flex-direction 을 row 또는 row-reverse로 주게 되면 main-axis가 행이 되고, flex-direction 을 column 또는 column-reverse로 주게 되면 main-axis가 열이 된다.

> reverse는 main-axis는 그대로이지만 시작 선과 끝 선이(방향) 서로 바뀌게 되는 것이다.

## `> 5. container - flex-wrap, flex-flow (shorthand)`

- `flex-wrap`

  - flex-item 요소들이 강제로 한줄에 배치되게 할 것인지, 또는 가능한 영역 내에서 벗어나지 않고 여러행으로 나누어 표현 할 것인지 결정하는 속성이다.

  - nowrap (initial)

    : 기본 설정값으로, flex-container 부모요소 넓이에 맞게 모두 자동으로 축소하여 flex-item 요소들을 한 줄에 배치한다.

    > 플랙스 아이템들을 더 많이 만들면 더 이상 짜부될수 없을 때 부모영역을 벗어난다.

  - wrap

    : flex-item 요소들의 총 넓이가 부모요소 넓이보다 크다면 넘어가는 순간의 flex-item 요소들을 다음줄로 줄바꿈

  - wrap-reverse

    : wrap 속성값과 동일하지만, 요소가 나열되는 시작점과 끝점의 기준이 반대로 배치된다.

    ![flex-wrap](/image/flex-wrap.png)

- `flex-flow`

  - flex-flow CSS 속성은 flex-direction, flex-wrap 속성의 단축 속성이다.

    ```
    /* flex-flow: <'flex-direction'> */
    flex-flow: row;
    flex-flow: row-reverse;
    flex-flow: column;
    flex-flow: column-reverse;

    /* flex-flow: <'flex-wrap'> */
    flex-flow: nowrap;
    flex-flow: wrap;
    flex-flow: wrap-reverse;

    /* flex-flow: <'flex-direction'>과 <'flex-wrap'> */
    flex-flow: row nowrap;
    flex-flow: column wrap;
    flex-flow: column-reverse wrap-reverse;
    ```

## `6. item - order`

- 플렉스 또는 그리드 컨테이너 안에서 현재 요소의 배치 순서를 지정한다. 컨테이너 아이템의 정렬 순서는 오름차순 order 값이고, 같은 값일 경우 소스 코드의 순서대로 정렬된다.

- order: 0; (initial)

  예를 들어, `.order`에게 1이상의 값을 주면 나머지 order를 주지 않은 item들은 order가 initial값으로 0이기 때문에 .order는 오름차순에 의하여 제일 뒤로 가는걸 볼 수 있다.

  ![order](/image/order.png)

  - 또한 음수도 사용 가능 하다.

> 참고 : order 속성은 논리적인순서나 탭 순서와는 전혀 상관 없이 `화면에 보이는 순서`에만 영향을 준다. 따라서 비시각적 매체에 적용해선 안된다.

## `7. item - flex-grow`

- flex-item 요소가, flex-container 요소 내부에서 할당 가능한 공간의 정도를 선언한다.

- 즉, item들의 크기가 container 보다 작아서 flex-container의 남는 공간을 얼마나 나눠 가지는지에 대한 것이다.

- flex-grow: 0; (initial)

> 음수값은 허용하지 않는다.

- 만약, flex-grow를 지정하지 않는다면 모두 0 으로 남는 공간을 차지하지 않고 비워두게 된다.

  ![flex-grow](/image/flex-grow.png)

* 만약 형제 요소로 렌더링 된 모든 flex-item 요소들이 동일한 flex-grow 값을 갖는다면, flex-container 내부에서 동일한 공간을 할당받는다.

  ![flex-grow](/image/flex-grow2.png)

* 하지만 flex-grow 값으로 다른 소수값을 지정한다면, 그에 따라 다른 공간값을 나누어 할당 받게 된다. (남은 공간의 1 / 1+1 의 공간씩을 갖게된다.)

  ![flex-grow](/image/flex-grow3.png)

> 보통 flex-grow를 사용할 땐, flex-shrink, flex-basis 속성을 함께 사용한다. 그리고 일반적으로 모든 값이 설정되었음을 보장하기 위하여 flex 속성을 이용해 축약형으로 사용한다. (남은공간의 1 / 1+2, 2 / 1+2 의 공간씩을 갖게된다.)

## `8. item - flex-shrink`

- flex-item 요소의 크기가 flex-container 요소의 크기보다 클 때 flex-shrink 속성을 사용한다.

- flex-shrink: 1; (initial)

> 음수 값은 허용하지 않는다.

- 우리는 이미 shrink를 경험 하였다.

![shrink](/image/shrink.png)

- flex-wrap의 예제 중 속성 값으로 nowrap을 주었을 때 item들의 크기가 부모의 크기를 넘었는데 넘쳐나지 않고 부모의 크기에 맞게 자동으로 줄어 딱 맞게 되었다. 그 이유가 flex-shrink: 1; (initial)이였기 떄문이다.

* `flex-shrink는 flex-grow의 반대 개념이라고 보면된다.` 부모 컨테이너가 줄어들면서 점점 작아지다가 item들의 크기보다 작아질때 `줄어드는 비율`에 대한 것이다.

- 따라서, flex-shrink:0; 을 주게 되면 부모 컨테이너를 넘처나게 되고, 1 이상의 값을 주면 그 비율대로 줄어들게 되어 부모 컨테이너에 맞게 된다.

![shrink](/image/shrink2.png)

- .shrink:0; 을 준 아이템만 자기 크기를 그대로 유지하고 나머지 shrink를 주지 않은 아이템들은 initial이 1이기 떄문에 같은 비율로 줄어드는걸 볼 수 있다.

## `9. item - flex-basis`

- 플렉스 아이템의 초기 크기를 지정한다. 즉, grow, shrink 되지 않은 기본 영역을 말한다.

- flex-basis: auto (initial);

- flex-item 들에게 width값을 주지 않으면 auto(initial)로 즉 content 크기만큼 width값을 가진다. (inline-block처럼)

  ![basis](/image/basis.png)

- flex-item들에게 flex-basis가 auto인 상태에서 width값을 주면 그 값이 즉 flex-basis라고 생각하면 된다.

  ![basis](/image/basis2.png)

- flex-basis를 지정하면 flex-item의 width값은 무시되고 flex-basis값이 width가 된다.

  ![basis](/image/basis3.png)

> item들의 flex-basis:0 ; 으로 지정한 뒤 flex-grow를 주면 내가 원하는 비율만큼 딱 맞게 늘릴 수 있다.

## `10. item - flex (shorthand)`

- flex는 flex-grow, flex-shrink, flex-basis의 단축 속성이다.

```
<!-- initial값 -->

flex-grow: 0;

flex-shrink: 1;

flex-basis: auto;
```

```
Syntax

/* Keyword values */
flex: auto;
flex: initial;
flex: none;

/* One value, unitless number: flex-grow */
flex: 2;

/* One value, length or percentage: flex-basis */
flex: 10em;
flex: 30%;

/* Two values: flex-grow | flex-basis */
flex: 1 30px;

/* Two values: flex-grow | flex-shrink */
flex: 2 2;

/* Three values: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;
```

> ⚠️⚠️주의 ! 단축 속성일 때 작성하지 않는다면 initial값이 들어가게 된다. 하지만, 한 개 또는 두 개의 단위 없는 숫자 값을 사용할 때, `<flex-basis>`의 값은 `auto`가 아니라 `0`이 된다.

```
flex: 1; // flex: 1 1 auto; 가아니라 flex:1 1 0;으로 된다는 말임.

따라서 flex: 1 과 flex-grow:1은 다르게 작동한다.
```

> 또한, 순서도 중요하다. 값이 두 개 일떄, 첫번 쨰 값은 `<number>`여야 하며 무조건 `<flex-grow>`가 된다.즉, grow-shrink 또는 grow-basis 순서를 따라야한다. 값이 세 개 일때는 grow-shrink-basis 순서를 따라야 한다.

```
flex: initial;   // flex: 0 1 auto;

flex: auto;  // flex: 1 1 auto;

flex: none;  // flex: 0 0 auto;
```

## `11. Container - justify-content`

- flex-container의 주 축(main-axis)을 따라 item들간에 공간을 분배하는 방법을 정의한다.

- justify-content: flex-start; (initial)

- 속성값은 많지만 브라우저별로 지원을 안하는 속성들이 있어서 많이 사용되는 값만 다뤄 보겠다.

- justify-content: flex-start;

  ![justify](/image/justify.png)

- justify-content: flex-end;

  ![justify](/image/justify2.png)

- justify-content: center;

  ![justify](/image/justify3.png)

- justify-content: space-between;

  ![justify](/image/justify4.png)

- justify-content: space-around;

  ![justify](/image/justify5.png)

## `12. Container - align-items`

- flex-container의 교차 축(cross axis)을 따라 item들간에 공간을 분배하는 방법을 정의한다.

  ![align-items](/image/aligin-items2.png)

- 위의 예시들에서는 item들에게 height값을 강제적으로 주어 stretch가 적용이 되지않았지만 만약 item들이 width와 height값을 가지지 않는다면 width는 flex-basis:auto(initial); 에 의하여 content크기만큼의 width를 가지는 것이고, height는 align-items:stretch;(initial) 에 의하여 flex-container의 height만큼 쭉쭉 뻗게 된다.

- align-items: stretch; (initial)

  ![align-items](/image/aligin-items.png)

- align-items: flex-start;

  ![align-items](/image/aligin-items3.png)

- align-items: flex-end;

  ![align-items](/image/aligin-items4.png)

- align-items: center;

  ![align-items](/image/aligin-items5.png)

> align-items 과 align-content의 차이점은 align-items는 `한 줄`에 대한 교차 축 정렬이고 aligin-content는 flex-wrap: wrap이 되어서 `두 줄 이상`에 대한 교차 축 정렬이다.

## `13. Container - align-content`

- align-content는 flex-wrap: wrap;이 되어서 두 줄 이상이 되었을 때의 cross-axis (교차 축)에 대한 정렬이다.

- align-content: normal; (initial)

  ![align-content](/image/align-content.png)

- align-content: flex-start;

  ![align-content](/image/align-content2.png)

- align-content: flex-end;

  ![align-content](/image/align-content3.png)

- align-content: center;

  ![align-content](/image/align-content4.png)

- align-content: space-between;

  ![align-content](/image/align-content5.png)

- align-content: space-around;

  ![align-content](/image/align-content6.png)

## `14. item - align-self`

- align-items와 비슷하게 작동하나 align-items는 `한 줄`에 대한 cross-axis(교차 축) 정렬이였다면 align-self는 `하나의 item`만 cross-axis(교차 축)정렬 이다.

- align-self: auto(initial);

- 즉m align-self를 쓰지 않으면 기본적으로 align-items의 값을 쓰게 되고 따로 지정하면 하나의 item만 따로 움직이게 된다.

  ![align-self](/image/align-selft.png)

* 속성 값은 align-items와 동일하다.
