# Grid

> Contents
>
> 1. Grid 개요
> 2. Container - display
> 3. Container - grid-template-rows, grid-template-columns
> 4. Container - grid-template-areas
> 5. Container - row-gap, column-gap, gap (shorthand)
> 6. Container - grid-auto-rows, grid-auto-columns
> 7. Container - grid-auto-flow
> 8. Container - grid (shorthand)
> 9. Container - justify-content, align-content
> 10. Container - justify-items, align-items
> 11. Item - grid-row (shorthand), grid-column (shorthand)
> 12. Item - grid-area (shorthand)
> 13. Item - order
> 14. Item - z-index
> 15. Gird 단위 - fr, min-content, max-content
> 16. Grid 단위 - auto-fill, auto-fit

## `1. Grid 개요`

- CSS 그리드 레이아웃은 웹페이지를 위한 `이차원 레이아웃 시스템`이다.

> flex는 `일차원 레이아웃 시스템`이다. 비슷하지만 확실히 다르다

- grid를 통해 콘텐츠를 행과 열에 배치할 수 있으며, 복잡한 레이아웃을 직접 직관적으로 구축할 수 있는 많은 기능이 있다.

- grid는 row와 column으로 이루어진 집합체로, 디자인 요소를 정렬할 수 있는 대상 패턴을 생성한다.

- 하나의 grid는 대게 rows,columns로 구상되며, 각 행과 열 사이에 공백이 있는데, 대게는 이를 일컬어혀 `gutters`라고 부른다.

  ![gutters](/image/gutters.png)

## `2. Container - display`

- display CSS 속성은 요소를 블록과 인라인 요소 중 어느 쪽으로 처리할지와 함께, 플로우, 그리드, 플렉스처럼 자식 요소를 배치할 때 사용할 레이아웃을 설정한다.

* display: inline | inline-block | block; 과 같은 아이들은 `<display-outside>`(바깥쪽) 자료형에 해당하고 display : flex | grid ; 과 같은 아이들은 `<display-inside>`(안쪽) 자료형에 해당한다. 따라서 두 자료형을 다른 개념으로 생각하는 편이 더 쉽다.

- [display - MDN](https://developer.mozilla.org/ko/docs/Web/CSS/display)

```
과거에는 바깥쪽 과 안쪽을 같이 설정 하고 싶을때는

.container{
  display: inline grid;
}

이런 식으로 하였는데 요즘은

.container{
  display: inline-grid;
}

이렇게 한번에 바깥쪽 과 안쪽을 설정 할 수 있다.container
```

## `3. Container - grid-template-rows, grid-template-columns`

- `grid-template-rows`

  - 그리드 행의 선 이름 및 트랙 크기 조정 기능을 정의한다.

  - grid-template-rows:none; (initial)

- `grid-template-columns`

  - 그리드 열의 라인 이름과 트랙 크기 조정 기능을 정의한다.

  - grid-template-columns:none; (initial)

> 속성 값으로 `<length>`, `<percentage>` 도 쓸 수 있지만 `fr`이라는 단위도 쓸 수 있다.

![grid-columns](/image/grid-columns2.png)

- display:grid; 를 주었지만 아무련 변화가 없다. 그 이유는 grid-template-rows, grid-template-columns를 지정하지 않았기 떄문에 initial값으로 none 이기 떄문이다.

![grid-columns](/image/grid-columns.png)

- 먼저 grid-template-columns:80px 80px 80px;을 주었다. 80px을 3번 적은 것은 column(열)을 3열 을 만들 것이고 열의 넓이를 각각 80px 80px 80px로 하겠다는 의미이다.

![grid-rows](/image/grid-rows.png)

- 그 다음 grid-template-row:100px 100px;을 주었다. 100px 100px 을 2번 적었기 때문에 row(행)을 2행에 높이를 100px 100px 주겠다는 의미이다. 3행의 값은 주지 않았기 떄문에 자신의 content크기만큼의 높이를 가지게 된다.

![fr](/image/fr.png)

- fr 단위는 부모 container의 넓이에 맞게 비율을 나눠 갖겠다는 뜻이다. 위의 예제에서는 1:1:2의 비율로 행의 넓이를 가진다.

> 만약 grid-template-columns: 100px 100px 100px; 처럼 동일한 값을 가진다면 repeat()함수를 써 쉽게 표현할 수 있다. 사용 방법은 간단하다. repeat(반복횟수, 값) 이다. 즉, grid-template-columns:repeat(3, 100px); 하면 동일한 효과를 얻을 수 있다.

## `4. Container - grid-template-areas`

- 명명된 그리드 영역을 지정하고 그리드에 셀을 설정하고 `이름(Item - grid-area)`을 지정한다.

![areas](/image/areas.png)

> 주의 ! 각각의 아이템들의 덩어리가 네모를 띄도록 나눠야 정상적으로 작동한다. (layout)

![areas](/image/areas2.png)

- 우선, columns 와 rows를 저렇게 주면 grid item은 4개밖에 없지만 container의 칸은 3 \* 5으로 나눠져있는거와 동일하다.

  ![areas](/image/areas3.png)

- 만약 layout을 위와 같이 만들고 싶다고 가정해보자.

- 우선 선행되어야 할 것이` grid-area속성`을 이용해 각 item들에게 이름을 정해 주어야 한다.

  ![area](/image/area.png)

- 그 뒤, grid-template-areas 속성을 이용해 마치 땅따먹기처럼 영역을 차지해주면 된다.

  ![areas](/image/areas4.png)

> 차지하고 싶지않은 영역 즉, 비워두고 싶은 영역은 . 을 사용하면 된다.

```
예시)

"a a ."
"a a ."
". b c"
```

## `5. Container - row-gap, column-gap, gap (shorthand)`

- `row-gap`

  - 각각의 행들간의 간격을 설정한다. 즉, gutter의 넓이를 설정하는 것이다.

  - row-gap:0(initial);

  ![row-gap](/image/row-gap.png)

  - 속성 값으로는 `<length>` | `<percentage>`를 쓸 수 있다.

  > percentage는 부모 container의 백분율이다.

  ![row-gap](/image/row-gap2.png)

  > gap을 주어서 gutters가 생기면 남은 영역들을 fr로 준다면 fr비율로 나눠 가진다.

- `column-gap`

  - 각각의 열들간의 간격을 설정한다. 즉, gutter의 넓이를 설정하는 것이다.

    ![column-gap](/image/column-gap.png)

- `gap (shorthand) `

  - row-gap과 column-gap의 단축 속성이다.

  - 순서는 무조건 앞 쪽이 row-gap, 뒤 쪽이 column-gap이다.

  ```
  주의 !

  만약, column-gap을 생략하고 row-gap만 지정한다면

  gap: 20px;

  row-gap:20px , column-gap: 0px; 이아니라

  column-gap은 row-gap과 동일한 값을 가진다.a

  즉, gap:20px; === row-gap:20px; , column-gap:20px;
  ```

## ` 6. Container - grid-auto-rows, grid-auto-columns`

![auto-rows](/image/auto-rows.png)

- grid-template-rows와 grid-template-columns로 3 \* 3 총 9칸에 넓이와 높이를 명시했다. 현재는 5개의 item들이 있고 추가로 더 생긴다면 9개 까지는 명시해놓은 넓이와 높이를 가지게 될것이다.

- 만약 9개가 넘는 item들이 생긴다면 어떻게 될까?

![auto-rows](/image/auto-rows2.png)

- 넘쳐 흐르게 된 item들은 본인으 content크기 만큼의 값만 가진다. 그 이유는 넘쳐 흐르는 item들의 넓이와 높이를 지정해주는 속성이 grid-auto-rows 와 grid-auto-columns 인데 initial값이 auto이기 떄문이다.

> container의 높이가 지정 안되어 있다면, 넘쳐흐르는 item들은 자신의 content크기만큼의 높이를 가지는데 만약, container의 높이가 지정되어있어 명시적인 grid 높이 이외의 높이에 item들이 흘러넘친다면 auto로 되어있을 때 그 높이를 같은 비율로 나눠가진다.

- 즉, 두 속성을 이용하면 넘쳐흐르는 item들에 대한 넓이와 높이를 지정할 수 있다.

- `grid-auto-rows`

  - grid-auto-rows:auto(initial);

  - grid-template-rows에 명시적으로 작성 못했지만 `넘쳐 흐르는` item들에게 암시적으로 행의 높이를 지정한다.

  ![auto-rows](/image/auto-rows3.png)

- `grid-auto-columns`

  - grid-auto-columns:auto(initial);

  - grid-template-columns에 명시적으로 작성 못했지만 `넘쳐 흐르는` item들에게 암시적으로 열의 넓이를 지정한다.

  - 나중에 추가로 배울 속성중에 item들을 내가 원하는 위치로 지정할 수 있는데 만약 지정한 column이 grid-template-columns로 명시하지 않은 column이라면 그때 `grid-auto-columns`로 암시적으로 지정 할 수 있다.

> 중요 ! grid-template 와 grid-auto의 비슷하지만 가장 큰 차이점은 명시적 / 암시적이라는 차이가 있고 grid-template-rows 와 grid-template-columns로 만들어놓은 grid 영역은 `명시적`이기 떄문에 내부에 item들이 없더라도 그 영역을 차지하고 있어서 container의 영역도 그만큼 커진다. 하지만, grid-auto-rows 와 grid-auto-columns로 지정해놓은 영역은 `암시적`이기 떄문에 item들이 없다면 그 영역을 볼 수 없다.

![암시적명시적](/image/암시적명시적.png)

## `7. Container - grid-auto-flow`

- 자동 배치 알고리즘의 작동 방식을 제어하여 자동 배치 항목이 `그리드로 유입되는 방법`을 정확하게 지정한다.

- `grid-auto-flow:row(initial);`

  ![auto-flow](/image/auto-flow.png)

- item들이 생겨 grid 칸에 배치될 때 row 방향으로 하나씩 배치된다.

- `grid-auto-flow:column`;

  ![auto-flow](/image/auto-flow2.png)

- item들이 생겨 grid 칸에 배치될 때 column 방향으로 하나씩 배치된다.

> 또 하나의 속성값중 row + dense, column dense 가 있다.

- ` grid-auto-flow:row dense`;

- 만약, 하나의 item이 grid-column 속성을 써서 3칸의 column 영역을 차지한다면 1행에는 위치하지 못하고 빈칸을 남겨둔채 아래행으로 내려가서 3칸을 차지하게 된다.

  ![dense](/image/dense.png)

- 이떄, grid-auto-flow:row dense 을 사용하면 빈칸을 남겨두지 않을 수 있다.

  ![dense](/image/dense2.png)

-` grid-auto-flow:column dense`;

![dense](/image/dense3.png)

- 원리는 같다.

![dense](/image/dense4.png)

## `8. Container - grid (shorthand)`

- grid CSS 속성은 shorthand property 이다. `외재적(명시적)`인 속성인 (grid-template-rows, grid-template-columns, grid-template-areas), 값과 `내재적(암시적)`인 속성인 (grid-auto-rows, grid-auto-columns, grid-auto-flow), 값을 한번에 설정한다.

> 너무 많은 속성들을 한번에 쓰다보니 처음 grid를 쓸 떄에는 각각의 속성들을 개별 작성해주는 것이 좋고, 익숙해 지면 grid shorthand를 쓰는 것을 추천한다.

```
예시)

grid: auto-flow / 1fr 1fr 1fr;

grid: auto-flow dense / 40px 40px 1fr;

grid: repeat(3, 80px) / auto-flow;

(/)를 기준으로 앞쪽은 row 뒤쪽은 column이다.  // grid (row에 관한 것) / (column에 관한것)
```

![grid](/image/grid.png)

- grid-auto-flow: row | column이 있는데 원하는 곳에 써주면 된다.

![grid](/image/grid2.png)

## `9. Container - justify-content, align-content`

> flex의 justify-content와 동일하다. 반드시 container가 item보다 커 남는 공간이 있어야 한다.

- `justify-content`

  : main-axis(주 축)에 대한 정렬이다.

- justify-content:start(=normal, initial);

  ![justify](/image/justify6.png)

- justify-content:start(initial) | end | center | space-between | space-around;

  ![justify](/image/justify7.png)

> flex와 동일하므로 나머지 설명은 생략한다.

- `align-content`

  : cross-axis(교차 축)에 대한 정렬이다.

- align-content:start(initial) | end | center | space-between | space-around;

> flex에서 flex-wrap:wrap; 이 되어서 여러 줄이 생겼을 떄 사용했었는데 사실 flex는 1차원 레이아웃이라 align-content 속성은 grid에 쓰는 것이 더 적합하다.

![align-content](/image/align-content7.png)

## `10. Container - justify-items, align-items`

> content와 item의 차이점은 content는 `덩어리(여러 줄을 container안에서의 배치 개념)`이고 item은 말 그대로 item`(한 개의 item을 각각 한 칸 그 안에서의 배치)` 그 자체이다.

> 그러니까 content는 container안에서의 배치이고 item은 grid 각각의 칸칸 안에서의 배치이다.

![content-items](/image/content-items.png)

- content는 container의 크기가 커서 그 안에서의 배치를 하고 싶을 떄 사용하는 것이고

![content-items](/image/content-items2.png)

- item은 grid 행 렬의 각각의 칸안에서의 item들의 배치를 하고 싶을 때 사용하는 것이다.

> 검은선 = container, 빨간선 = grid 행 렬, 파란선 = item들

![items](/image/items.png)

- justify-items와 align-items을 지정하지 않으면 initial값이 stretch이기 떄문에 각각의 칸안에서 쭉쭉 뻗어 가득 차있다.

- `justify-items`

  - justify-items:stretch(initial);

  - justify-items:stretch | start | end | center;

  ![items](/image/items2.png)

- ` align-items`

  - align-items:stretch(initial);

  - align-items:stretch | start | end | center;

  ![items](/image/items3.png)

> justify-items와 align-items를 둘다 center를 주게 되면 각각의 칸 안에서 item들이 center로 가게된다.

![items](/image/items4.png)

> flex와 마찬가지로 (Item)`justify-self` 또는 (Item)`align-self`를 이용하면 item 하나의 위치만 지정할 수 있다.

## `11. Item - grid-row (shorthand), grid-column (shorthand)`

- `grid-row`

  - grid-row-start 와 grid-row-end의 단축 속성이다.

  - grid-row-start:auto(initial);

  - grid-row-end:auto(initial);

  ```
  Syntax

  grid-row: (start) / (end);

  ```

  - grid-row-start와 grid-row-end를 지정하지 않으면 auto로 1칸씩만 차지한다.

  ![start-end](/image/start-end.png)

  - 지정하면 그리드 영역에 시작위치와 끝위치를 지정할 수 있다. `(몇번쨰 열, 행이 아니라 몇번쨰 선에대한 것이다.)`

  ![start-end](/image/start-end2.png)

  > 우측에보면 선에 마이너스(-)로 된 숫자도 있는데 이는 거꾸로 셀 떄의 숫자이고 마이너스는 명시적으로 지정한 선에만 있다.

  > 따라서 grid-row: 1 / -1; 을 하면 한 줄 을 다 차지하게 된다. === grid-row: 1 / 4;

  > grid-row: 1 / 3; 으로 2칸을 차지할 수도 있지만 span키워드를 이용해서 grid-row: 1 / span 2; 도 동일하다. 시작점을 1선으로해서 두 칸을 차지하여라 라는 뜻이다.

- `grid-column`

  - grid-column-start 와 grid-column-end의 단축 속성이다.

  - grid-column-start:auto(initial);

  - grid-column-end:auto(initial);

  - 원리는 동일하다.

## `12. Item - grid-area (shorthand)`

- 속성의 사용 방법은 두 가지 이다.

- 위에서의 grid-template-areas에서 사용하기 위해 grid-area로 item의 이름을 지정할 떄도 쓰이고.

- grid-area 속성은 grid-row-start, grid-column-start, grid-row-end and grid-column-end 값을 한번에 설정하는 shorthand property 이다. 해당 속성값은 grid item의 크기와 위치를 결정할 떄도 쓰인다.

```
Syntax 1

grid-area:name;

Syntax 2 (순서가 중요하다.)

grid-area: grid-row-start / grid-column-start / grid-row-end / grid-column-end ;
```

## `13. Item - order`

- order CSS 속성은 플렉스 또는 그리드 컨테이너 안에서 현재 요소의 배치 순서를 지정한다. 컨테이너 아이템의 정렬 순서는 오름차순 order 값이고, 같은 값일 경우 소스 코드의 순서대로 정렬한다.

- order:0(initial);

  ![order](/image/order2.png)

  > 설명은 flex에서 해서 생략한다.

## `14. Item - z-index`

- CSS z-index 속성은 위치 지정 요소와, 그 자손 또는 하위 플렉스 아이템의 Z축 순서를 지정한다. 더 큰 z-index 값을 가진 요소가 작은 값의 요소 위를 덮는다.

![z-index](/image/z-index.png)

- 명시적으로 값을 주지 않으면 겹칠 일이 없지만 명시적으로 값을 주다보면 영역이 겹칠 수도 있다.

## `15. Gird 단위 - fr, min-content, max-content`

- `fr`

  : container를 길이를 비율로 가진다. 절대길이와도 혼합하여 사용할 수 있다. 그러면 절대길이는 그 값을 가지고 나머지 길이를 fr 비율대로 가진다.

```
ex)
1fr 2fr // 1 : 2

2fr 1fr 3fr // 2 : 1: 3

100px 1fr 2fr // 100px 가지고 나머지를 container의 길이를 1 : 2
```

- `min-conten`t

  : 한글과 영어는 조금 다르게 동작하는데 한글은 한글자 한글자 글자별로 쪼갤 수 있어 min 최소한의 글자 content 크기만큼 가지는데 영어는 한단어를 그 이하로 쪼개지 못해 한단어의 크기만큼 가지게 된다.

  ![min-content](/image/min-content.png)

  ![min-content](/image/min-content2.png)

  : 만약, 영어가 여러 단어가 있다면 단어 별로 쪼개고 제일 긴 단어가 기준이 된다.

  ![min-content](/image/min-content3.png)

- `max-content`

  : max에서 알 수 있듯이 한 줄에 볼 수 있게끔 영어와 한글을 상관없이 최대한 늘린다.

  ![max-content](/image/max-content.png)

> min-content 와 max-content는 내부의 content에 따라 유동적으로 길이를 변경할 때 사용한다.

## `16. Grid 단위 - auto-fill, auto-fit`

- `auto-fill`

  - grid-template-columns: repeat(3, 1fr); 이렇게 딱 3열 을 지정하는 것이 아니라 auto-fill을 지정하면 container의 넓이에 따라 반응형으로 배치된다.

  ![auto-fill](/image/auto-fill.png)

  > 남는 공간이 100px이 되지않아 우측에 여백이 생기는게 보기 싫다면 minmax()함수를 사용해서 해결할 수 있다.

  ![minmax](/image/minmax2.png)

  - 최소 100px의 값을 가지고 최대한 1fr을 가진다. 그래서 남는공간이 100px보다 적게남았을 땐 최대의 길이인 1fr을 가져 여백없이 쭉 차다가 남는공간이 100px이 될 때 하나의 열이 더 생기게된다.

- ` auto-fit`

  - auto-fill 과 minmax()를 사용하더라도 더 이상 들어올 item들이 없다면 container에 빈 공간이 생길 수 밖에 없다.

    ![auto-fit](/image/auto-fit.png)

  - 이를 해결하기 위해서 auto-fit을 쓴다.

    ![auto-fit](/image/auto-fit2.png)
