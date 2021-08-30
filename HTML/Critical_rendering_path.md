# HTML Critical rendering Path의 이해

- 브라우저가 서버에서 페이지에 대한 HTML 응답을 받으면 화면에 표시되기 전에 많은 단계를 거쳐야 한다.

- 브라우저가 페이지의 초기 출력을 위해 실행해야하는 이 순서를 `Critical Rendering Path`(이하 CRP)라고 한다.
- 사이트의 성능을 향상시키는 방법을 이해하는데 CRP에 대한 지식은 매우 유용하다.

- CRP는 아래와 같이 6단계로 구성된다.
  1. DOM 트리 구축 (Constructing the DOM Tree)
  2. CSSOM 트리 구축 (Constructing the CSSOM Tree)
  3. JavaScript 실행 (Running JavaScript)
  4. 렌더링 트리 구축 (Creating the Render Tree)
  5. 레이아웃 생성 (Generating the Layout)
  6. 페인팅 (Painting)

![path](/image/path.png)

## `1. DOM 트리 구축 (Constructing the DOM Tree)`

- DOM(Document Object Model) 트리는 완전히 구문 분석된 HTML 페이지의 Object 표현이다. 루트 요소 <`html>`로 시작하여 페이지의 각 element/text에 대한 노드가 만들어진다. 다른 요소 내에 중첩된 요소는 자식 노드로 표시되며 각 노드에는 해당 요소의 전체 특성이 포함된다. 예를 들어, `<a>` 요소는 노드와 관련된 href 속성을 갖는다.

- 예를들어 아래의 html 문서를 보자.

```
<html>
<head>
  <title>Understanding the Critical Rendering Path</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
      <h1>Understanding the Critical Rendering Path</h1>
  </header>
  <main>
      <h2>Introduction</h2>
      <p>Lorem ipsum dolor sit amet</p>
  </main>
  <footer>
      <small>Copyright 2017</small>
  </footer>
</body>
</html>
```

- 위 html 문서는 다음과 같은 DOM 트리를 생성한다.
  ![dom](/image/dom.png)

* HTML의 장점은 부분적으로 실행될 수 있다는 것이다. 페이지에 내용이 표시하기 위해 전체 문서를 로드할 필요가 없다. `그러나 다른 리소스인 CSS와 JavaScript는 페이지 렌더링을 차단할 수 있다.`

## `2. CSSOM 트리 구축(Constructing the CSSOM Tree)`

- CSSOM(CSS Object Model)은 DOM과 연관된 스타일의 Object 표현이다. 이것은 DOM과 비슷한 방식으로 표현되지만 명시적 또는 암시적 선언과 상속 여부에 관계없이 각 노드의 관련 스타일로 표시된다.

* 위에서 언급한 html 문서의 style.css 파일에는 아래와 같은 style이 정의되어 있다.
  ![css](/image/css.png)
* 위 CSS는 다음과 같은 CSSOM 트리를 생성한다.
  ![cssom](/image/cssom.png)

* CSS는 `"렌더링 차단 리소스(render blocking resource)"`로 간주된다. 즉, 먼저 리소스를 완전히 파싱하지 않으면 렌더링 트리를 구성 할 수 없다. HTML과 달리 CSS는 계단식 상속 특성 때문에 부분적으로 실행될 수 없다. 문서의 뒷부분에 정의된 스타일은 이전에 정의된 스타일을 무시하고 변경할 수 있다. 따라서 스타일 시트 전체가 파싱되기 전에 스타일 시트에서 앞에서 정의한 CSS 스타일을 사용하기 시작하면 잘못된 CSS가 적용되는 상황이 발생할 수 있다. 즉, 다음 단계로 넘어 가기 전에 CSS를 완전히 파싱 해야 한다.

\*CSS 파일은 현재 장치에 적용되는 경우에만 렌더링 차단 리소스로 간주된다. `<link rel = "stylesheet">` 태그는 미디어 속성을 받아 들일 수 있다. 미디어 속성은 스타일이 적용되는 미디어 쿼리를 지정할 수 있다. 예를 들어 media 속성이 orientation:landscape 인 스타일 시트가 있고 페이지를 세로 모드로 보고 있는 경우 해당 리소스는 렌더링 차단 리소스로 간주되지 않는다.

- `CSS는 "script blocking"일 수도 있다.` 이것은 JavaScript 파일이 실행되기 전에 CSSOM이 생성 될 때까지 기다려야 하기 때문이다.

## `3. JavaScript 실행(Running JavaScript)`

- JavaScript는 "파서 차단 리소스(parser blocking resource)"로 간주된다. 즉, HTML 문서가 한줄한줄씩 parsing되다가 `<script>`를 만나면 차단된다.

\*파서가 내부 태그이든 외부 태그이든 `<script>` 태그에 도달하면 (외부 태그 인 경우) fetch를 중단하고 실행한다. 따라서 문서 내의 요소를 참조하는 JavaScript 파일이 있는 경우 해당 문서가 표시된 후에 배치 해야 한다.

- JavaScript가 파서 차단(parser blocking)되는 것을 피하기 위해 async 속성을 적용하여 비동기적으로 로드 할 수 있다.  
  ![script attribute](/image/js.png)

## `4. 랜더링 트리 구축(Creating the Render Tree)`

- `렌더링 트리는 DOM과 CSSOM의 조합이다.` 페이지에서 최종적으로 렌더링 될 내용을 나타내는 트리다. 즉, 표시되는 내용만 캡쳐하가 때문에 display:none을 사용하여 CSS로 숨겨진 요소는 포함하지 않는다.

* 위의 예제 DOM과 CSSOM을 사용하여 다음 렌더링 트리가 생성된다.
  ![renderTree](/image/renderTree.png)

## `5. 레이아웃 생성(Generating the Layout)`

- 레이아웃은 뷰포트의 크기에 관련된 CSS 스타일에 대한 컨텍스트에 의해 뷰포트의 크기를 결정한다. 비율 또는 뷰포트 단위. 뷰포트 크기는 문서 헤드에 제공된 메타 뷰포트 태그에 의해 결정되거나, 태그가 제공되지 않으면 기본 뷰포트 너비 인 980px가 사용된다.

* 브라우저의 뷰포트(Viewport) 내에서 각 노드들의 정확한 위치와 크기를 계산합니다. 풀어서 얘기하자면 생성된 Render Tree 노드들이 가지고 있는 스타일과 속성에 따라서 `브라우저 화면의 어느위치에 어느크기로 출력될지 계산하는 단계`라고 할 수 있습니다. Layout 단계를 통해 %, vh, vw와 같이 상대적인 위치, 크기 속성은 실제 화면에 그려지는 pixel단위로 변환됩니다.
  ![layout](/image/layout.png)

## `6. 페인팅(Painting)`

- Layout 계산이 완료되면 이제 요소들을 실제 화면을 그리게 됩니다. 이전 단계에서 이미 요소들의 위치와 크기, 스타일 계산이 완료된 Render Tree 를 이용해 실제 픽셀 값을 채워넣게 됩니다. 이 때 텍스트, 색, 이미지, 그림자 효과등이 모두 처리되어 그려집니다.

* 페인트 단계에서 처리에 걸리는 시간은 DOM의 크기와 적용되는 스타일에 따라 다르다. 어떤 스타일은 다른 스타일보다 더 많은 작업을 필요로 한다. 예를 들어, 복잡한 그래디언트 배경 이미지는 단순한 단색 배경색보다 더 많은 시간을 필요로 한다.
