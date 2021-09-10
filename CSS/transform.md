# Transform

> Contents
>
> 1. transform (변형) 개요
> 2. 크기 - scale
> 3. 회전 - rotate
> 4. 이동 - translate
> 5. 기울이기 - skew
> 6. 기준점 - transform-origin

## `1. transform (변형) 개요`

- 요소에 회전, 크기 조절, 기울이기, 이동 효과를 부여할 수 있다.

```
/* 키워드 값 */
transform: none; (initial)

/* 함수 값 */
transform: matrix(1.0, 2.0, 3.0, 4.0, 5.0, 6.0);
transform: matrix3d(1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1);
transform: perspective(17px);
transform: rotate(0.5turn);
transform: rotate3d(1, 2.0, 3.0, 10deg);
transform: rotateX(10deg);
transform: rotateY(10deg);
transform: rotateZ(10deg);
transform: translate(12px, 50%);
transform: translate3d(12px, 50%, 3em);
transform: translateX(2em);
transform: translateY(3in);
transform: translateZ(2px);
transform: scale(2, 0.5);
transform: scale3d(2.5, 1.2, 0.3);
transform: scaleX(2);
transform: scaleY(0.5);
transform: scaleZ(0.3);
transform: skew(30deg, 20deg);
transform: skewX(30deg);
transform: skewY(1.07rad);

/* 다중 함수 값 */
transform: translateX(10px) rotate(10deg) translateY(5px);
transform: perspective(500px) translate(10px, 0, 20px) rotateY(3deg);

```

- transform 속성은 키워드 `none` 또는 하나 이상의 `<transform-function>` 값을 스페이싱을 구분해서 지정할 수 있다.

  - 여러 개의 `<transform-function>` 값을 사용하면 요소에 변형을 `오른쪽부터 왼쪽`으로 하나씩 순서대로 적용하는 것과 같다. (순서가 상관이 있다.)

> transform 하게되면 진짜 그 요소의 width나 height을 직접 변경하는 것이 아니라 원래 크기나 위치는 그대로 가지고 눈에 보이 크기만 줄이거나 늘리거나 회전시키거나 이동시킨다.

## `2. 크기 - scale`

- 2D 평면에서 요소의 크기를 조정하는 변환을 정의한다.

> 2D로만 크기를 조정하는 변환이된다. 3D 크기를 조정하려면 scale3d()를 대신 사용한다.

-` 요소의 중앙을 기준`으로 늘어나거나 줄어든다.

- 양수 값을 사용하면 늘어나고 음수 값을 사용하면 줄어든다.

```
Syntax

scale(sx)   //  scale(2) === scale(2, 2)

scale(sx, sy)
```

## `3. 회전 - rotate`

- 2D 평면의 `고정점`을 중심으로 요소를 변형하지 않고 회전시키는 변환을 정의한다.

  - 고정점은 변환 원점이라고도 하는데, 기본값은 `요소의 중앙`이지만 `transform-origin` 속성을 사용하여 사용자 지정 변환 원점을 설정할 수 있다.

```
Syntax

rotate(a)
```

- 회전량은 `<angle>`자료형에 의해 지정된다. 양수이면 시계 방향으로 이동하고 음수이면 시계 반대 방향으로 이동한다.

  - `<angle>` : deg, grad, rad, turn

    - 90deg(90도) = 100grad = 0.25turn = 1.5708rad

    - 180deg(180도) = 200grad = 0.5turn ≈ 3.1416rad

    - -90deg(-90도) = -100grad = -0.25turn ≈ -1.5708rad

## `4. 이동 - translate`

- 요소를 수평 및/또는 수직 방향으로 재배치한다.

```
/* Single <length-percentage> values */
transform: translate(200px);
transform: translate(50%);

/* Double <length-percentage> values */
transform: translate(100px, 200px);
transform: translate(100px, 50%);
transform: translate(30%, 200px);
transform: translate(30%, 50%);
```

```
Syntax

translate(x축, y축)
```

- 양수이면 x축은 오른쪽으로, y축은 아래쪽으로 이동하고 음수이면 x축은 왼쪽으로 y축은 위쪽으로 이동한다.

* 또한, translate는 translateX()와 translateY()를 별도로 지정해 사용할 수도 있다.

```
transform:translateX(150px);  //  X축으로 150px 이동

transform:translateY(150px);  //  y축으로 150px 이동
```

```
translate(200px) !== translate(200px, 200px),  translate(200px) = translate(200px, 0px)
```

> ⚠️ ⚠️ 한가지 값만 입력할 떄 scale과 translate는 다르게 동작한다 주의하여라.

- translate의 value는 `<length>` or `<percentage>`이다.

- `<percentage>`는 x축은 본인의 width의 백분율이고 y축은 본인의 height의 백분율이다.

  ![translate](/image/translate2.png)

> ⚠️ ⚠️ 또한 scale | rotate는 요소의 중앙이 기본값이였는데 translate는 왼쪽 상단이 원점(기준점)이다.

![translate](/image/translate.png)

## `5. 기울이기 - skew`

- 2D 평면에서 요소를 꼬아(기울이는)내는 변환을 정의한다.

* 이 변환은 요소 내의 각 점을 수평 및 수직 방향으로 특정 각도로 왜곡하는 전단 매핑(변환)이다. 이 효과는 요소의 각 모서리를 잡고 특정 각도를 따라 잡아당기는 것과 같다.

* skew의 value는 `<angle>`이다.

```
Syntax

skew(ax)

skew(ax, ay)
```

```
skew(45deg) !== skew(45deg, 45deg),  skew(45deg) = skew(45deg, 0px)
```

> ⚠️ ⚠️ 한가지 값만 입력할 떄 scale과 skew는 다르게 동작한다. skew는 translate와 같이 동작한다.

- 또한, skew는 skewX()와 skewY()를 별도로 지정해 사용할 수도 있다.

* 예시) skewX(20deg); // skew(20deg, 0) 과 동일.

![skew](/image/skew.png)

- 예시) skewY(20deg); // skew(0, 20deg) 과 동일.

![skew](/image/skewY.png)

## `6. 기준점 - transform-origin`

- 요소의 `변환 원점`을 설정한다.

* 변환 원점은 변환이 적용되는 지점이다. 예를 들어 rotate() 함수의 변환 원점이 회전 중심이다.

```
Syntax

/* One-value syntax */
transform-origin: 2px;
transform-origin: bottom;

/* x-offset | y-offset */
transform-origin: 3cm 2px;

/* x-offset-keyword | y-offset */
transform-origin: left 2px;

/* x-offset-keyword | y-offset-keyword */
transform-origin: right top;

/* y-offset-keyword | x-offset-keyword */
transform-origin: top right;

/* x-offset | y-offset | z-offset */
transform-origin: 2px 30% 10px;

/* x-offset-keyword | y-offset | z-offset */
transform-origin: left 5px -3px;

/* x-offset-keyword | y-offset-keyword | z-offset */
transform-origin: right bottom 2cm;

/* y-offset-keyword | x-offset-keyword | z-offset */
transform-origin: bottom right 2cm;
```

- transform-origin을 별도로 지정하지 않으면 `initial로 transform-origin: 50% 50% 0; 즉, 요소의 중앙`이다.

  - 50% 50% 0을 키워드로 사용하게 되면 `center`이다.

* `키워드`

  ![transform-origin](/image/transform-origin.png)

* 예시)

  ![transform-origin](/image/transform-origin2.png)
