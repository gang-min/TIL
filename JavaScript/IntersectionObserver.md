# IntersectionObserver - Web API

- Intersection Observer API는 타겟 요소와 상위 요소 또는 최상위 document 의 viewport 사이의 intersection 내의 변화를 비동기적으로 관찰하는 방법이다.

* 즉, 우리가 원하는 `요소가 뷰포트나 특정한 영역(이 API에서 이를 root요소 혹은 root로 칭함)에 들어오거나 나갔을 때` 우리의 callback함수를 호출해주는 관찰자이다.

- 사용 방법

1. `intersection observer 생성하기`

   : intersection observer를 생성하기 위해서는 생성자 호출 시 콜백 함수를 제공해야 한다. 이 콜백 함수는 `threshold가 한 방향 혹은 다른 방향으로 교차할 때 실행`된다.

```
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0
}

let observer = new IntersectionObserver(callback, options);
```

> threshold: 1.0 은 대상 요소가 root 에 지정된 요소 내에서 100% 보여질 때 콜백이 호출될 것을 의미한다.

2. `Intersection observer 설정`

   : IntersectionObserver() 생성자에 전달되는 `options 객체는` observer 콜백이 호출되는 상황을 조작할 수 있다.

   - root

     : 대상 객체의 가시성을 확인할 때 사용되는 뷰포트 요소이다. 이는 대상 객체의 조상 요소여야 한다. 기본값은 브라우저 뷰포트이며, root 값이 null 이거나 지정되지 않을때 `기본값(뷰포트)로 설정`이 된다.

   - rootMargin

     : root 가 가진 여백이다. 이 속성의 값은 CSS의 margin 속성과 유사하다. 이것은 root 요소의 각 측면의 bounding box를 수축시키거나 증가시키며, 교차성을 계산하기 전에 적용된다. `기본값은 0이다.`

     : CSS margin과 마찬가지로 상,우,하,좌 다양하게 margin을 줄 수 있다.

     ![intersectionObserver](/image/intersectionObserver6.png)

     > 만약 rootMargin: '100px';을 주었다면 원래의 viewPort보다 100px 더 넓은 영역에서 요소들의 들어오고 나가는 것을 관찰한다. 즉, 사용자에게 보여지기 이전에 viewPort의 바깥 100px부터 callback함수가 실행된다.

   - threshold

     : observer의 콜백이 실행될 대상 요소의 `가시성 퍼센티지(intersection ratio)`를 나타내는 단일 숫자 혹은 숫자 배열이다. 만일 50%만큼 요소가 보여졌을 때를 탐지하고 싶다면, 값을 0.5로 설정하면 된다. 혹은 25% 단위로 요소의 가시성이 변경될 때 마다 callback이 실행되게 하고 싶다면 [0, 0.25, 0.5, 0.75, 1]과 같은 배열을 설정한다. `기본값은 0이다.`

     > 주의 !  
     > threshold를 설정 하게 되면 들어 올 때는 정해진 값이 되고 나갈 떄는 정해진 threshold의 정해진값의 반대이다. 즉, threshold:0.7;로 설정 되어 있다면 요소가 들어올 떄 (Intersecting:true) 요소가 70%만큼 보여야 callback함수가 실행되고, 요소가 나갈 떄 (Intersecting:false) 요소가 30% 나가면 callback함수가 실행된다.

3. `callback 함수`

- callback함수가 호출이 될 때 entries와 observer라는 두 가지 인자가 전달 된다.

```
const callback = function(entries, observer){

};
```

- 실습 예시)

![intersectionObserver](/image/intersectionObserver.png)

- 생성자 함수 IntersectionObserver에 callback이라는 것을 전달해서 새로운 observer 라는 인스턴스(오브젝트)를 만들었고, boxes를 forEach로 돌면서 각각의 box를 observer가 observe(관찰하도록)명령 해 놓은 상태이다.

- observer가 observe(관찰하는) 요소들(boxes)이 화면(뷰포트)에 `들어오거나 나갈 때 우리가 등록한 callback함수를 호출`해 준다.

- callback함수에는 우리가 eventHandler를 등록 해 놓으면 event라는 유용한 정보를 인자로 전달해 주는 것처럼 `여기에는 entries와 observer라는 유용한 정보들을 전달해 준다.`

![intersectionObserver](/image/intersectionObserver2.png)

- 처음에는 20개의 모든 box들이 window에 들어왔기 때문에 총 20개의 요소가 entries에 들어있고 각각의 배열에는 `IntersectionObserverEntry`라는 오브젝트가 들어 있다.

- IntersectionObserverEntry는 화면에 들어온 요소에 대한 정보를 담고 있는데 하나를 열어서 보면 아래와 같다.

![intersectionObserver](/image/intersectionObserver3.png)

- 요소의 `boundingClientRect` 즉, 포지션(x, y)과 너비와 높이를 알 수 있다.

- `intersectionRatio`는 요소가 얼마만큼 뷰포트에 들어와 있는지 확인할 수 있다. 뷰포트안에 요소가 전부 위치했다면 1, 90%만 들어와 있다면 0.9, 20%만 들어와 있다면 0.2 이런식으로 0부터1까지 ratio를 알려준다.

- `intersectionRect`는 boundingClientRect와 비슷하지만 `현재 뷰포트에 들어온 상태`에서의 포지션과 너비와 높이를 알 수 있다.

- `isIntersecting`은 요소가 뷰포트 안에 들어오는 상태라면 true이고 즉, 뷰포트안에 요소가 조금이라도 보인다면 true, 보이지 않는다면 false이다.

- `rootBounds`는 지금 현재 보여지고 있는 root 너비와 높이를 알 수 있다. 위의 예제에서는 option객체를 지정하지 않았기 떄문에 기본값은 뷰포트로 지정되어 있다.

- `target`은 현재 관찰되어지고 있는 요소를 말한다.

![intersectionObserver](/image/intersectionObserver4.png)

- entries는 배열이기 떄문에 forEach로 돌면서 각각의 entry에 대해서 해당하는 작업을 해주면 된다.

> 뷰포트에 요소들이 처음 들어 올떄만 entries에 모든 요소들이 들어가고 이후에는 요소가 들어가고 나가는 것들에만 대해서 entries에 들어간다.

- 위와 같이 if를 이용하여 요소의 isIntersecting가 true, 즉 들어오는 상태라면 로그를 찍고, else 나가는 경우라면 error를 찍도록 해보았다.

![intersectionObserver](/image/intersectionObserver5.png)

- 그래서 이걸 활용하여 들어오는 요소에는 active라는 class를 추가해주고 만약 나가는 요소라면 active class를 제거해줄 수 있게 하는 것으로도 사용할 수 있다.

> 이제 여기서 조금 더 세부적으로 조정하고 싶다면 IntersectionObserver를 만들 때 option을 전달할 수 있다. (let observer = new IntersectionObserver(callback, options);)

![intersectionObserver](/image/intersectionObserver7.png)
