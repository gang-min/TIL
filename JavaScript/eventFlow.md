# Event Flow - Bubbling & Capturing

![bubbling-capturing](/image/bubbling-capturing.png)

- 위의 예시에서 button을 클릭하였는데 button에 등록된 클릭 리스너 뿐만 아니라 .middle 과 .outer에 등록된 클릭 리스너가 호출 되었다. 무엇 떄문일까?

![bubbling-capturing](/image/bubbling-capturing2.png)

- 그 이유는 브라우저에서 이벤트를 처리하는 `Bubbling & Capturing` 때문이다.

- `Bubbling & Capturing` 이란?

  : 만약, 위의 예제처럼 button을 click하면 button의 클릭 리스너만 호출하는 것이 아니라 button을 감싸고 있는 부모 중에서 똑같이 click event가 있으면 다같이 호출 해준다.

- button과 middle과 outer의 쌓임을 입체적으로 보면 아래와 같다.

![bubbling-capturing](/image/bubbling-capturing5.png)

- `event.target`과 `event.currentTarget`을 구분하는 것이 중요한데 `event.target`은 이벤트의 시발점을 말하고, `event.currentTarget`은 event의 진짜 주인 즉, event.target떄문에 이벤트가 일어나는 요소를 말한다.

- 그래서 위에서의 결과를 살펴보면 button을 눌렀지만 button을 감싸고 있는(HTML상) middle, outer가 똑같은 클릭 리스너를 가졌기 떄문에 모두가 호출 되었다. 결과를 다시 한번 보면

![bubbling-capturing](/image/bubbling-capturing4.png)

- button을 click하였기 떄문에 button의 currentTarget과 target 모두 자기 자신을 가리킨다. middle은 currentTarget은 본인이지만 target은 시발점은 button을 가리킨다. 마찬가지로 outer도 currentTarget은 본인이지만 target은 시발점은 button을 가리킨다.

> button을 눌렀을 떄 관련된 부모의 모든 event를 실행시키다 보니까 순차적으로 실행시켜야하는 문제가 생긴다. 즉, 순서가 중요하기 떄문에 event는 eventFlow 흐름을 가진다. `그 flow가 바로 Bubbling & Capturing이다.`

![bubbling-capturing](/image/bubbling-capturing3.png)

-
