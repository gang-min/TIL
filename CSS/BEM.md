# [CSS 방법론] BEM 방식

- 방법론 쉽게 풀어쓰면 html에서 클래스 이름을 작성할 때 너무너무 복잡하고 유지 보수 하기가 힘들기 때문에 어떻게 하면 클래스 이름을 작성할 때 잘 작성할 수 있을지에 대해서` 클래스 이름을 작성하는 방법에 대해서 정의한 규칙`이다.

- 방법론에는 여러 가지가 있지만, 요즘에 많은 분들이 사용하고 있는 BEM에 대해서 알아보자.

* 나중에 프로젝트를 조금 더 모듈화해서 만들고 PostCSS 같은 아이들을 이용하게 되면 BEM은 필요가 없지만, 모듈화를 하지 않고 간단하게 프로젝트를 만든다면 BEM을 이용해서 만들면 조금 더 쉽게 클래스 이름을 만들 수가 있다.

## `BEM이란 무엇인가`

- BEM은 Block Element Modifier 이다.

- 즉 block과 element, modifier으로 나누어서 이름을 작성하는 것을 말한다.

* 예를들면, 만약 우리가 카드를 만든다고 한다면 바로 `Block은 이 카드 자체가 된다.` 즉, 카드 하나가 우리가 만들고자 하는 컴포넌트이기 때문에 Block이다.

  ![BEM-Block](/image/BEMBlock.png)

* 여기서 카드(block)안에 들어 있는 `이미지나 타이틀이나 버튼들은 다 Element이다.` 즉, 한가지, 더이상 분리될 수 없는 Element 자체인거다.

![BEM-Element](/image/BEMElement.png)

```
BEM 이름 작성 방법 아래와 같다.

Block__Element--Modifier
```

```
앞의 카드를 BEM 방식으로 적어보면 아래와 같이 적어볼 수 있다.

.card

.card__img

.card__title

.card__description

.card__button
```

- 여기서 만약에 카드가 다른 색상의 카드가 존재한다면, 즉, 다른 버전의 카드가 존재할 떄 Modifier를 쓰면 된다.

![BEM-Modifier](/image/BEMModifier.png)

> 그리고 여기서 버튼이 과연 카드(Block)안에 속해 있는 컴포넌트인지 아닌지를 조금 고민할 필요가 있다. 만약 버튼이 카드(Block)안에서 뿐만 아니라 다른 컴포넌트(Block)에도 공통적으로 쓰인다면 `이 버튼은 카드(Block)안에 속해있을 필요가 없다.` 그래서 `.card__button`이라고 하기 보다 버튼은 버튼 자체로 컴포넌트이기 때문에 이렇게 `.button(Block)`으로 정해 따로 작성하는 것이 좋다.

![BEM](/image/컴포넌트.png)

- 또, 민약 이 card가 여러가지가 묶여있는 cards라는 container안에 들어있다면 아래와 같이 작성해야 할까?

![BEM](/image/뱀.png)

> 많은 사람들이 다른 방식으로 다양하게 얘기할 수 있지만, BEM은 nesting 될수록 hierarchy(체계)대로 이름을 일일이 다 작성하는것은 아니라고 본다. BEM은 컴포넌트 단위로 Block으로 이름을 작성하는거기 때문에 card는 card 자체로 하나의 컴포넌트이다. cards는 이런 card를 묶어 놓는 container일뿐이다.

- 그래서 cards는 cards대로 만들고 card는 card 자체로 만드는 것이 좋다.

![BEM](/image/뱀2.png)

- 이렇게 작성하게 되면 card라는 Block은 cards라는 container안에 들어갈 수도 있고 또 다른 부분에서도 쉽게 쓰여질 수 있다.

* 그래서 이런식으로 작성하는 것이 조금 더 코드 양을 줄일 수도 있고 앞에서 본 방식대로 작성하게 되면 타이핑하는게 너무 많다. 그래서 가능하면 깔끔하게 이 방식대로 작성하는걸 추천한다.

* [참고하면 좋은 사이트 - BEM](https://nykim.work/15)
