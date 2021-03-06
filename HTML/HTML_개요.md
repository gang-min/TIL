# HTML 개요

> Contents
>
> - HTML과 웹 브라우저
> - HTML, CSS 그리고 JavaScript
> - 웹 표준, 웹 접근성, 웹 호환성

# `HTML과 웹 브라우저`

```
.pdf ➡️ PDF뷰어
.doc , .docx ➡️ MS Word
.html ➡️ 웹 브라우저
```

- `웹 브라우저`는 단순히 HTML 문서를 보여주는 역할(Viewer)만 하는것이 아니라
  사용자입장에서는 웹 서핑을 도와주는 다양한 부가기능(즐겨찾기, 방문기록 저장 등..)도 가지고 있다. 또한, 개발자 입장에서는 웹페이지를 분석할 수 있는 개발도구들도 웹브라우저가 제공하고 있다.

- 웹 브라우저 종류

  - 크롬, 엣지, 익스플로러, 사파리 ....

## `HTML`: Hyper Text Markup Language

- 하이퍼텍스트 마크업 언어는 웹페이지를 위한 지배적인 `마크업 언어`다. 또한, HTML은 제목,단락,목록 등과 같은 본문을 위한 구조적 의미를 나타내는 것뿐만 아니라 링크,인용과 그 밖의 항목으로 `구조적 문서`를 만들 수 있는 방법을 제공한다.

- `HyperText`란 웹페이지를 다른 페이지로 연결하는 링크를 말합니다. 링크는 웹의 근본적인 속성으로, 인터넷에 자료를 올리고 다른 사람이 만든 페이지로 링크함으로써 우리도 월드 와이드 웹 세계의 능동적인 일원이 될 수 있다.

- 이전에는 `HyperText`가 다른 페이지로 연결하는 링크만을 가리켰다면 지금은 웹 문서를 이루고 있는 요소 하나하나를 전부 `HyperText`로 보면 된다.

- HTML은 웹 브라우저에 표시되는 글과 이미지 등의 다양한 콘텐츠를 표시하기 위해 `마크업`을 사용합니다. HTML 마크업은 다양한 `요소`를 사용하는데, `요소`에는 `<head>, <title>, <body>, <header>, <footer>, <article>, <section>, <p>, <div>, <span>, <img>, <aside>, <audio>, <canvas>, <datalist>, <details>, <embed>, <nav>, <output>, <progress>, <video>, <ul>, <ol>, <li>` 등 많은 종

# `HTML, CSS 그리고 JavaScript`

```
* [구조]HTML: 웹 문서의 기본적인 골격을 담당.
* [표현]CSS: 각 요소들의 레이아웃, 스타일링을 담당.
* [동작]JavaScript: 동적인 요소(사용자와의 인터렉션)을 담당.
```

# `웹 표준, 웹 접근성, 웹 호환성`

**웹 표준**

- HTML5 는 W3C에서 2014년에 공식 표준화.
- 2019년에 WHATWG(애플,모질라,구글,MS)에 의해 HTML Living Standard가 표준화됨.
- HTML이 표준화 되기 이전에는, 익스플로러의 액티브X처럼 독자적인 플러그인이 존재하기도 하였음.
- 웹 표준을 준수하여 작성한다면 운영체제,브라우저마다 의도된 대로 보여지는 웹 페이지를 만들 수 있음.
  > [웹 표준화](https://library.gabia.com/contents/domain/2614/)

**웹 접근성(Web Accessibility)**

- 웹 접근성은 `장애를 가진 사람과 장애를 가지지 않은 사람 모두가 웹사이트를 이용할 수 있게 하는 방식`을 가리킨다. 사이트가 올바르게 설계되어 개발되고 편집되어 있을 때 모든 사용자들은 정보와 기능에 동등하게 접근할 수 있다.

- 또한 웹 접근성은 `장애를 갖지 않은 사람`에게도 이점을 줍니다. 예를들어:
  - 작은 화면,다른 입력 모드 등을 가진 휴대폰,스마트 워치, 스마트 TV 및 다른 디바이스를 사용하는 사람
  - 나아가 들어감에 따라 기능적 능력이 변한 연로한 사람
  - 팔이 부러지거나 안경을 잃어버려서 "일시적인 장애"를 겪는 사람
  - 밝은 햇빛이나 소리를 드기 힘든 환경에 있어 "상황적 제약"을 겪는 사람
  - 느린 인터넷을 사용하거나 제한적이거나 비싼 대역폭을 사용하는 사람
- `웹 브라우징에 쓰이는 보조과학기술`: 스크린리더,화면 돋보기,음성 인식,키보드 오버레이 등

**웹 호환성(Cross Browsing)**

- 웹 브라우저 버전,종류와 관계없는 웹사이트 접근
- 웹 표준 준수를 통한 브라우저 호환성 확보

  - HTML,CSS 문법 준수
  - 동작,레이아웃,플러그인 호환성
