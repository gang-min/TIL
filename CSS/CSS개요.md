# CSS 개요

> Contents
>
> 1. CSS소개
> 2. CSS는 어떻게 생겼을까
> 3. CSS 적용하는 방법
> 4. 캐스캐이딩 원칙

## `1. CSS소개`

- CSS (Cascading Style Sheets) 는 HTML, XHTML, XML 같은 문서의 스타일을 꾸밀 때 사용하는 스타일 시트 언어이다.

## `2. CSS는 어떻게 생겼을까`

- CSS는 룰 기반(Rule-based)의 언어이다.

- CSS를 통해 특정 요소, 혹은 특정 요소들의 집합의 스타일 규칙을 정의할 수 있다.

  ![cssrule](/image/cssrule.png)

> 1. 선택자(Selector) : 스타일을 지정할 HTML 요소 선택
>
> 2. 선언 블록(Declaration block) : 중괄호 {} 내부의 여러 선언들을 작성
>
> 3. 선언(Declaration) : property(속성) : value(값); (프로퍼티와 값으로 이루어진 쌍)
>
> 4. 선택자 { 하나이상의 선언; } 의 형태로 이루어진 하나의 Rule (혹은 Rule Set)

## `3. CSS 적용하는 방법`

> 1. 내부 스타일 (Embedded)
>
> 2. 인라인 스타일 (Inline)
>
> 3. 외부 스타일 (External)

### 1. 내부 스타일 (Embedded)

- `<head>` 태그에 `<Style>` 태그를 작성하는 방법  
  ![embedded](/image/styleembedded.png)

### 2. 인라인 스타일 (Inline)

- `<body>` 태그안의 특정 요소에 `style 속성(attribute)`으로 사용하는 방법

* 인라인 스타일은 사용을 지양하는 것이 좋다.  
  ![embedded](/image/styleinline.png)

### 3. 외부 스타일 (External)

- 외부에 CSS파일을 별도로 만든 뒤 `<link>` 태그로 연결하는 방법

* 가장 권장하는 방법  
  ![embedded](/image/stylelink.png)

## ` 4. 캐스캐이딩 원칙`

- 아래 따로 정리한 Cascading 참조  
  [Cascading](https://github.com/gang-min/TIL/blob/main/CSS/Cascading.md)

* `스타일 상속(inherited)`

  - 부모 요소에 있는 스타일 속성(property)들이 자식 요소로 전달(상속)된다.

    - 자식 요소에서 재정의 할 경우, 부모의 스타일을 덮어쓴다.

  - 상속이 되지 않는 속성도 있다.(예: 배경 이미지, 배경 색, box-model 등..)
    ![inherited](/image/inherited.png)
    > color는 상속되는 property로서 자식 요소는 물론 자손 요소까지 적용된다. 하지만 `<button>`처럼 요소에 따라 상속 받지 않는 경우도 존재한다.
    >
    > 또한 border, padding과 같은 상속되지 않는 요소도 존재한다.
    >
    > W3C가 제공하는 `Full property table의 inherited? 가 yes인 property만 상속된다.

  * 상속되지 않는 경우(상속받지 않는 요소 또는 상속되지 않는 프로퍼티), `inherit` value를 사용하여 명시적으로 상속받게 할 수 있다.
    ![inherited](/image/inherited2.png)
