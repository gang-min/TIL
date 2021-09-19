# Event Flow - Bubbling & Capturing

![bubbling-capturing](/image/bubbling-capturing.png)

- 위의 예시에서 button을 클릭하였는데 button에 등록된 클릭 리스너 뿐만 아니라 .middle 과 .outer에 등록된 클릭 리스너가 호출 되었다. 무엇 떄문일까?

![bubbling-capturing](/image/bubbling-capturing2.png)

- 그 이유는 브라우저에서 이벤트를 처리하는 event flow - `Bubbling & Capturing` 때문이다.

- `Bubbling & Capturing` 이란?

  : 만약, 위의 예제처럼 button을 click하면 button의 클릭 리스너만 호출하는 것이 아니라 button을 감싸고 있는 부모 중에서 `똑같이` click event가 있으면 다같이 호출 해준다.

- button과 middle과 outer의 쌓임을 입체적으로 보면 아래와 같다.

![bubbling-capturing](/image/bubbling-capturing5.png)

- `event.target`과 `event.currentTarget`을 구분하는 것이 중요한데 `event.target`은 이벤트의 시발점을 말하고, `event.currentTarget`은 event의 진짜 주인 즉, event.target떄문에 이벤트가 일어나는 요소를 말한다.

- 그래서 위에서의 결과를 살펴보면 button을 눌렀지만 button을 감싸고 있는(HTML상) middle, outer가 똑같은 클릭 리스너를 가졌기 떄문에 모두가 호출 되었다. 결과를 다시 한번 보면

![bubbling-capturing](/image/bubbling-capturing4.png)

- button을 click하였기 떄문에 button의 currentTarget과 target 모두 자기 자신을 가리킨다. middle은 currentTarget은 본인이지만 target은 시발점은 button을 가리킨다. 마찬가지로 outer도 currentTarget은 본인이지만 target은 시발점은 button을 가리킨다.

> button을 눌렀을 떄 관련된 부모의 모든 event를 실행시키다 보니까 순차적으로 실행시켜야하는 문제가 생긴다. 즉, 순서가 중요하기 떄문에 event는 eventFlow 흐름을 가진다. `그 flow가 바로 Bubbling & Capturing이다.`

![bubbling-capturing](/image/bubbling-capturing3.png)

- 만약 Bubbling & Capturing 순서대로 event가 실행이 된다면 button을 눌렀을 때 middle과 outer는 capturing에서 1번 bubbling에서 1번 총 2번이 실행되야 하는데 결과에선 그렇지 않고 `1번만 실행`이 되었다.

- 즉 1 -> 2 -> 3 -> 4 -> 5의 순서를 따르지 않았다는 말이된다. 그 이유는 무엇일까?

![bubbling-capturing](/image/bubbling-capturing6.png)

- 1 -> 2 -> 3 -> 4 -> 5의 순서를 따른다면 나는 button을 눌렀을 뿐인데 middle과 outer는 2번씩이나 event가 발생하기 떄문에 내가 원하지 않는 결과를 발생시킬수 있다. 이를 방지하기 위해서 브라우저가` 제약`을 둔다.

- `event.currentTarget 과 event.target이 동일하지 않는 경우`라면 Capturing 또는 Bubbling 단계에서 이벤트 리스너가 호출될지를 선택할 수 있다. 그래서 Capture떄 실행이 된다면 Bubble때 실행이 되지 않고, Bubble떄 실행이 된다면 Capture때 실행이 되지 않는다.

- 브라우저의 `기본값은 Bubble`이다.

- 그렇기 떄문에 위에 예제에서는 button을 클릭하였을 때 `middle과 outer는 currentTarget과 target이 동일하지 않기 떄문에` Capturing 또는 Bubbling 단계를 선택하여야 하는데 별다른 지정을 하지 않았기에 기본값인 Bubbling 단계에서 이벤트가 호출이 된 것이다.

- 즉, 위의 예제에서는 3 -> 4 -> 5의 순서로 이벤트가 발생하였다.

![bubbling-capturing](/image/bubbling-capturing7.png)

- 사실, addEventListener는 3가지의 인자를 받을 수 있다.

  1. event type

  2. listener (callbackFunction)

  3. UseCapture (true || false) 기본값은 false이다. (option)

- 위에서의 스크립트에서는 3번째 인자를 지정하지 않았기 떄문에 use Capture가 기본값인 false로 되었고, 따라서 Bubble이 선택 된것이다.

![bubbling-capturing](/image/bubbling-capturing8.png)

- 만약 middle의 usecapture를 true로 지정했다면 eventFlow가 아래와 같이 실행될 것이다.

![bubbling-capturing](/image/bubbling-capturing9.png)

- 즉, 순서가 2 -> 3 -> 5가 되는 것이다.

![bubbling-capturing](/image/bubbling-capturing10.png)

> 브라우저의 event flow인 Bubbling & Capturing을 막을수는 없지만 propagation(전파)를 막는 방법이 있다.

- `event.stopPropagation();`

- button에 event.stopPropagation();을 주면 button만 실행되는 걸 볼 수 있다.

![bubbling-capturing](/image/bubbling-capturing11.png)

- 원리는 이러하다. Capturing과 Bubbling의 event flow는 막지 못하지만 button에서 middle과 outer로 넘어가는 propagation(전파)를 막은 것이다.

- middle과 outer를 bubble로 지정하였다면 원래 3 -> 4 -> 5의 순서로 이벤트가 호출되어야 하지만 button에 event.propagation()을 하면 그 이상의 전파는 막게된다. 따라서 3에서 끝나 3번만 호출되는 것이다.

![bubbling-capturing](/image/bubbling-capturing12.png)

> event.stopPropagation();과 거의 비슷한데 조금 다른 event.stopImmediatePropagation(); 도 있다.

- 하지만 stopPropagation 이나 stopImmediatePropagation을 사용하는 것은 위험하고 나쁘다. 가능하면 사용하지 않는것이 좋다.

- event.target 과 event.currentTarget을 이용하여 동일한 효과를 얻을 수 있다.

![bubbling-capturing](/image/bubbling-capturing13.png)
