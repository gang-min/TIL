# Reset CSS

## `Reset CSS를 찾아보게 된 이유`

: HTML은 구조 CSS는 표현 Javascript는 동적 처리를 담당으로 각각의 역할이 있다고 이해를 하였는데 HTML의 태그 들 중 default 스타일이 있길래 HTML은 구조인데 왜 스타일링도 첨가 되어 있을까 모든 태그를 동일한 조건으로 만든 뒤 마크업 용도로만 쓰고 CSS로 표현을 하면 안되는 것인가? 라는 의문점이 들어 css를 초기화 할 수 있는 방법에 대해 찾아보게 되었습니다.

## `Reset CSS란?`

- 웹 브라우저마다 `각기 다른 default 스타일`이 지정되어 있어, 이를 초기화함으로써 다양한 웹브라우저에서도 동일한 스타일이 적용되도록 하는 설정

- W3C에서 공식적으로 권장하는 기법이라기 보다는 실무에서 편의에 의해 임의로 지정하는 설정임

## `방법들`

### `1. Eric Meyer's reset`

- 구글링 해본 결과 리셋 방법이 굉장히 다양하게 나와있는데 그중 유명한 Eric Meyer라는 개발자가 만들어 놓은 `CSS reset`이다.

- 가장 최근 업데이트가 2011년이고 오래된 자료이기도 하고 유용한 스타일까지도 초기화해서 비효율을 초래할 수 있다는 비판도 있다.

[Eric Meyer's reset](https://meyerweb.com/eric/tools/css/reset/)

### `2. CSS Normalize`

- 그래서 최근에는 필요한 부분만 초기화를 하여 사용하기도 하거나 `CSS Normalize`라는 기법을 사용하는 전략이 생겨났다.

* CSS Normalizes는 브라우저 간 유저 에이전트 스타일의 오차를 줄이고, 버그만 줄이는 방향으로 스타일을 재지정하는 거다. CSS Reset는 기본값을 다 싸그리 엎는 데 반해 CSS Normalize는 기본값들을 최대한 보존하고 수정을 최소화한다.

* 즉Normalize RESET CSS의 특징은 기본 스타일은 남겨두고, 브라우저별로 다른 스타일만 초기화하는 방식으로 적용(즉, 모든 효과를 RESET시키는 것이 아님)

* 오픈 소스이기 때문에 이 코드를 파일로 저장해 HTML에 연결해 사용하면 된다.

[CSS Normalize](https://necolas.github.io/normalize.css/)
