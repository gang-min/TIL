# Data 속성

## `1. Data 속성이란?`

- HTML5부터 데이터 속성이라는 개념이 추가되었는데, 어느 엘리멘트(요소)에나 `data-`로 시작하는 속성은 무엇이든 사용할 수 있다.

- 이러한 데이터 속성은 화면에 보이지 않게 글이나 추가 정보를 엘리멘트(요소)에 담아 놓을 수 있다.

- 즉,` 특정한 데이터를 DOM요소에 저장해두기 위함이 목적`이다.

* 또한 개발자들이 원하는 속성을 custom 할 수 있다.

```
문법

<article id="html" data-columns="3" data-index-number="123" data-parent="cars"> ... </article>

⚠️⚠️data-뒤에 붙는 이름은 대문자를 포함할 수 없습니다.
```

- `data-*` 전역 특성은 `사용자 지정 데이트 특성(custom data attribute)`이라는 특성 클래스를 형성함으로써 임의의 데이터를 스크립트로 HTML과 DOM 사이에서 교환할 수 있는 방법을 제공한다.

## `2. Data 속성 장점`

- 데이터 속성의 장점은 이전과 같이 hidden으로 태그를 숨겨두고 데이터를 저장할 필요가 없다는 점이다. 따라서 HTML 이 훨씬 간결해진다.

* 하나의 HTML 요소에 여러 data 속성을 동시에 사용할 수도 있다.

## `3. 데이터 속성 접근하기 (JavaScript || CSS)`

- `JavaScript에서 접근하기`

  - JavaScript에서 이 속성 값들을 읽는 방법은 간단하다.

  - HTML 이름과 함께 `getAttribute()` 를 사용하면 된다.

  ![데이터셋](/image/데이터셋.png)

  - 그러나 표준은 더 간단한 방법을 정의한다. `DOMStringMap`은 `dataset` 속성을 통해 읽어낼 수 있다.

    - `DOMStringMap` interface는 엘리멘트(요소)에 추가된 `사용자 지정 데이트 특성(custom data attribute)`의 데이터를 나타내기 위해 HTMLElement.dataSet/ SVGElement.dataSet 속성에 사용된다.

  * `dataset` 객체를 통해 `data 속성`을 가져오기 위해서는 속성 이름의 `data-` 뒷부분만 사용한다.

  * ⚠️⚠️ `data-` 뒷부분의 -(대시)들은 `camelCase`로 변환되는 것에 주의하여라.

  ```
  camelCase 예시)

  data-index-number=123     -->   dataset.indexNumber

  ```

  ![데이터셋](/image/데이터셋2.png)

  - ⚠️⚠️ 각 속성의 값은 `문자열`만 가능하며 읽거나 쓸 수 있다. 만약 `data-index-number=123` 같이 number로 설정하여도 "123" string으로 변경한다.

  ![데이터셋](/image/데이터셋3.png)

- `CSS에서 접근하기`

  - 데이터 속성은 순 HTML 속성이기 때문에 CSS에서도 접근할 수 있다.

  ```
  [data-columns="3"]{
    color:red;
  }
  ```

  - CSS - attr()함수로도 사용 가능하다.

    - attr()함수는 요소의 속성 값(attribute의 value)를 반환해주는 함수이다.

  ```
  article::before{
    content: attr(data-columns); // === content:3;
  }
  ```

## `4. 문제점`

- 보여야 하고 접근 가능해야하는 내용은 데이터 속성에 저장하면 안된다. 왜냐하면 접근 보조 기술이 접근할 수 없기 떄문이다. 또한 검색 크롤러가 데이터 속성의 값을 찾지 못한다.
