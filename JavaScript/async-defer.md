# Script의 async와 defer 속성

- 웹 브라우저는 html을 랜더링하는 과정에서 css(`<link type='text/css'>`) 또는 js(`<script>`) 를 만나면 해당 내용이 해석되고 실행되기 전에는 뒤에 나오는 내용을 처리하지 않는다.

* 즉, JavaScript는 `parser blocking resource(파서 차단 리소스)`이다.

* 이 부분은 화면의 랜더링 속도에 큰 영향을 줄 수 있다(사용자 경험 측면에서 큰 영향을 주며 SEO와도 관련된다).

- [Browser Critical Rendering Path 참조](https://github.com/gang-min/TIL/blob/main/HTML/Critical_rendering_path.md)

## 1. `<head>` 안에 `<script>`를 속성없이 사용 하였을 때

- 브라우저는 문서를 parsing해서 읽다가 `<script>`를 만나면 진행하고 있었던 parsing을 멈추고 `<script>`를 `fetch -> parsing -> execution`한 후 다시 문서를 parsing하게 된다.

![script](/image/scriptsrc.png)

- 이 경우 스크립트를 fetch, parsing, execution할 떄까지 문서(HTML) parsing이 중단돼 화면 랜딩 시간이 더 소요된다.

## 2. `<head>` 안에 `<script>`를 `async`(attribute) 와 함께 사용 하였을 때

- async 속성을 쓰면 문서를 parsing하는 동안 `<script>`를 만나면 문서 parsing과 함께 `<script>`를 fetch받고 `<script>` fetch가 완료되면 즉시 `<script>`를 execution하게 된다. `<script>`를 execution 하는 동안은 문서 parsing을 멈추고 `<script>`를 execution이 끝난 후 남은 문서를 parsing 한다.

![script](/image/scriptsrc2.png)

- ⚠️`실행의 순서가 다운로드 완료 시점의 결정`되므로 실행 순서가 중요한 스크립트들에 async를 사용할 때는 유의해야 한다(HTML5 spec에 async=false 속성 지정시 호출 순서대로 실행되도록 추가됨(default : true)).
- ⚠️ 중간에 `<script>`가 먼저 실행될 경우 문서(HTML)에서 아직 id나 class를 읽지도 않았는데 `<script>`가 DOM을 참조하고 있으면 오류가 생길 것이다.
- 따라서, `async속성은 DOM을 조작하지 않고, 다른 <script>에 의존성이 없고, 실행 순서가 중요하지 않은 경우에 사용한다.`

## 3. `<head>` 안에 `<script>`를 `defer`(attribute) 와 함께 사용 하였을 때

- defer 속성을 쓰면 문서를 parsing하는 동안 `<script>`를 만나면 `<script>`를 fetch하지만 문서 parsing을 멈추지 않고 끝까지 수행하고 `<script>`는 `</html>`태그를 만났을 떄 실행한다. 즉, DOMContentLoaded 발생 이전에 실행해야 함을 나타내는 불리언 속성이다.

- 따라서, `DOM을 조작하고, 다른 <script>에 의존성이 있고, 실행 순서가 중요한 경우에 사용한다.`
  ![script](/image/scriptsrc3.png)
