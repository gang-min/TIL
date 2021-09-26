# Template Literal

## 1. template literal

```
Syntax

`문자열`

또는

`문자열 ${표현식} 문자열`

또는

tag `문자열 ${표현식} 문자열`
```

- template literal

  - 문자열 처리를 위한 리터럴

  - 표현식을 포함할 수 있음.

- backtick( ` ) 안에 표현식 작성

  - 표현식을 ${표현식} 형태로 작성

```
console.log(`ABC`)  // ABC
```

- 백틱 안에 문자열을 작성하였다.

- 문자열이 그대로 문자열로 출력된다.

```
const one = 1, two = 2;

const result = `1 + 2는 ${one + two}이 된다`;

console.log(result);  // 1 + 2는 3이 된다
```

- ${one + two} 템플릿에 표현식을 작성하였다.

- one에 one 변숫값 1을, two에 two 변숫값 2를 설정하고

- one의 값과 two의 값을 더해표현식 위치에 설정한다.

- 템플릿 리터럴은 모든 공백이 그대로 반영된다.

> template literal은 문자열과 표현식을 하나로 연결하여 문자열을 처리하는 것이다.

> '' 와 "" / template literal 의 큰 차이점은 표현식을 사용할 수 있다는 것이다.

> 또한 `줄바꿈`과 `공백`도 그대로 반영이 된다.
