# Cascading(캐스캐이딩)

- ## Cascading이란?

  - cascade의 사전적 의미는 폭포라는 의미가 있는데 여기서는 여라기지 스타일이 하나의 태그에 동시에 적용될 때 위에서 아래로 단계적으로 적용된다는 뜻이다.

  * 즉, `css 스타일 적용 우선 순위에 따라 스타일이 적용되는 규칙이다.`

> 캐스캐이딩(우선순위)를 결정하는 요소
>
> 1. 중요도
> 2. 구체성(명시도)
> 3. 코드의 순서

- ## `중요도`

  - `저작자(프로그래머) !important > 저작자(프로그래머)CSS > 사용자 CSS> 브라우저 CSS` 순이다.

  - 저작자는 사용자나 브라우저가 설정한 기본 CSS보다 우선순위가 더 높다. 만약 저작자가 아무런 CSS 속성도 지정하지 않았을 경우에는 가장 우선순위가 낮은 브라우저 CSS가 default로 보여진다.

  - 사용자가 CSS 속성을 지정하는 것은 흔하지는 않기 떄문에 넘어간다.

  - 저작자 !important는 CSS 속성을 줄 때 !important를 뒤에 붙이는 것을 말한다. 이렇게 하면 우선순위가 가장 높아진다.

* ## `구체성 (선택자에 따른 명시도)`

  - 태그에 스타일 속성을 줄 때 `선택자`를 사용한다.

  - 선택자의 종류에 따라 구체성의 차이가 있다.

  * 구체성은 선택자를 얼마나 명시적으로 선언했느냐를 수취화한 것이다.

  ```
  0, 0, 0, 0
  ```

  - 구체성은 4개의 숫자 값으로 이루어져 있다.

  - 구체성은 아래의 규칙대로 계산된다.

  ```
   - 1, 0, 0, 0 : 인라인 스타일

   - 0, 1, 0, 0 : 선택자에 있는 모든 id 속성값

   - 0, 0, 1, 0 : 선택자에 있는 모든 class 속성값, 기타 속성, 가상클래스

   - 0, 0, 0, 1 : 선택자에 있는 모든요소, 가상요소

   - 전체 선택자(*)는 0, 0, 0, 0을 가진다

   - 조합자는 구체성에 영향을 주지 않는다. (> , + 등)
  ```

> !important 키워드는 별도의 구체성 값은 없지만, 모든 구체성을 무시하고 최우선권을 갖는다. 최대한 사용을 지양하는것이 좋다. 사용방법은 속상값 뒤 한 칸 공백을 주고 느낌표 기호와 함께 사용한다.

- 구체성 예시)

```
h1 { ... }  /* 0,0,0,1 */

body h1 { ... }  /* 0,0,0,2 */

.grape { ... }  /* 0,0,1,0 */

*.bright { ... }  /* 0,0,1,0 */

p.bright em.dark { ... }  /* 0,0,2,2 */

#page { ... }  /* 0,1,0,0 */

div#page { ... }  /* 0,1,0,1 */

/* 인라인 스타일 */
<p id="page" style="color:blue">Lorem impusm dolor sit.</p>  /* 1,0,0,0 */

/* important */
p#page { color: red !important; }
```

> 만약 구체성이 동일해서 같은 우선순위에 있는 경우 `나중에 `선언한 것이 우선되어 적용된다. (즉 코드순서와 관련있다. 더 아래,나중에 작성한것이 적용)

> 또한 상속된 속성은 아무런 구체성을 갖지 않는다.