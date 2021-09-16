# DOM (Document Object Model)

![dom](/image/dom1.png)

- 우리가 간단한 웹 페이지를 만들면 HTML 파일을 브라우저에서 읽게 된다.

- 브라우저에서는 body태그, section태그 이런 각각의 태그들을 분석해서 이것을 `노드`로 변환하게 된다.

  ![dom](/image/dom2.png)

- 즉, 브라우저가 이해할 수 있는 자신들만의 `오브젝트`로 변환하게 되는 것이다.

- HTML 파일에서 쓰인 태그가 Javascript에서는 Node라는 오브젝트로 변환이 된다.

- Node 오브젝트 안에는 우리가 태그 안에 작성했었던 class 라던지 아니면 텍스트 같은 모든 정보들이 포함 되어져 있다.

  ![dom](/image/dom3.png)

- Node는 EventTarget이라는 오브젝트를 `상속`한다. 결국 Node라는 오브젝트는 EventTarget의 오브젝트이다. (즉, 모든 Node는 Event가 발생할 수 있다.)

> 상속이란? 부모 생성자의 기능을 물려받으면서 새로운 기능도 추가하는 것을 의미한다. 외국에서는 상속 대신 `확장(extend)`라는 말을 쓴다.

- Document도 Node이기 떄문에 또 Node는 EventTarget이기 떄문에 Document에서도 Event가 발생할 수 있고, image나 HTML 요소들은 Element로 변환이 된다. 그래서 Element도 Node이고 Node는 EventTarget이기 떄문에 모든 요소에서도 event가 발생할 수 있는 것이다. Text도 마찬가지이다. (Node의 종류는 다양하다.)

  ![dom](/image/dom4.png)

- Element 안에서도 굉장히 다양한 Element가 있는데 HTML요소라면 HTMLElement, SVG요소라면 SGVElement, 이렇게 각각의 타입별로 Element가 존재한다.

- HTMLElement 안에는 어떤 태그를 쓰느냐에 따라서 HTMLInputElement가 될 수 있고 HTMLDivElement가 될 수 있고 HTMLImageElement가 될 수 있고 굉장히 많은 태그별로 Element가 존재한다.

> 즉, 모든 태그의 요소들은 각각 HTML(Tag)Element이고 HTML(Tag)Element는 HTMLElement이고 HTMLElement는 결국 Element이고 Element는 Node이고 결국 Node는 EventTarget이다.

![dom](/image/dom5.png)

- 다시 브라우저가 웹페이지를 읽을 때로 가보면, 브라우저가 우리의 웹페이지 즉 HTML 파일을 한줄 한줄 읽으면서 `DOM Tree`로 변환하게 된다.

- HTML에 있는 각각의 태그들이 DOM 요소랑 하나하나씩 맞물려진다. 즉, HTML태그에는 그에 상응하는 `DOM Tree` 요소가 있다.

![window](/image/window.png)

- 큰 그림으로 보면 브라우저가 실행될 때 우리의 웹페이지를 읽으면 글로벌 오브젝트에는 `Window`가 있고, `window`에는 `document`이라는 것이 들어 있다. 그리고 `window` 안에는 `BOM `브라우저에 관련된 `오브젝트(Web API)`들 navigator, location, fetch, storage 등등 다양한 것들을 우리가 쓸 수 있고, 또 기본적인 JavaScript에 관련된 `오브젝트(Built-in Object)`들이 존재한다.

> BOM (Browser Object Model)은 웹 브라우저와 관련된 객체집합을 말하며 웹 브라우저가 제공하는 기능들을 말한다. 이것들을 Web API라고도 부른다. (JavaScript가 제공하는 기능이 아니다.)
