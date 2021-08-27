# 마크다운(Mark Down)에 대해서

## 마크다운의 장점

---

1. 문법이 쉽다.
2. 관리가 쉽다.
3. 지원 가능한 플랫폼과 프로그램이 다양하다.

## 마크다운의 단점

---

1. 표준이 없어 사용자마다 문법이 상이할 수 있다.
2. 모든 HTML 마크업을 대신하지 못한다.

## 마크다운의 사용

---

- 메모장부터 전용 에디터까지 많은 곳에서 활용할 수 있습니다. 문법이 쉽기 떄문에 꼭 전용 에디터를 사용할 필요는 없지만, 마크다운 코드의 하이라이트 효과를 원한다면 전용 에디터가 좋은 선택이 될 것이다.

## 마크다운 문법(Syntax)

---

# `제목(Header)`

- `<h1>` 부터 `<h6>` 까지 제목을 표현할 수 있습니다.`

```
# 제목 1
## 제목 2
### 제목 3
#### 제목 4
##### 제목 5
###### 제목 6
```

# 제목1

## 제목2

### 제목3

#### 제목4

##### 제목5

###### 제목6

- `제목1(h1)과 제목2(h2)는 다음과 같이 표현할 수 있습니다`

```
제목1
=====
제목2
-----
```

# 제목1

## 제목2

# `강조(Emphasis)`

- 각각 `<em>`, `<strong>`, `<del>` 태그로 변환됩니다.  
  밑줄을 입력하고 싶다면 `<u></u>` 태그를 사용하세요.

```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
```

_single asterisks_  
_single underscores_  
**double asterisks**  
**double underscores**  
~~cancelline~~

# `목록(List)`

- `<ol>`, `<ul>` 목록 태그로 변환됩니다.

```
  1. 순서가 필요한 목록
  1. 순서가 필요한 목록
      - 순서가 필요하지 않은 목록(서브)
      - 순서가 필요하지 않은 목록(서브)
  1. 순서가 필요한 목록
      1. 순서가 필요한 목록(서브)
      1. 순서가 필요한 목록(서브)
  1.순서가 필요한 목록
  - 순서가 필요하지 않은 목록에 사용 가능한 기호
    -대쉬(hyphen)
    *별표(asterisks)
    +더하기(plus sign)
```

1. 순서가 필요한 목록
1. 순서가 필요한 목록
   - 순서가 필요하지 않은 목록(서브)
   - 순서가 필요하지 않은 목록(서브)
1. 순서가 필요한 목록
   1. 순서가 필요한 목록(서브)
   1. 순서가 필요한 목록(서브)
1. 순서가 필요한 목록

- 순서가 필요하지 않은 목록에 사용 가능한 기호

  - 대쉬(hyphen)

  * 별표(asterisks)

  - 더하기(plus sign)

# `링크(Links)`

- `<a>`로 변환됩니다.

```
[GOOGLE](https://google.com)

[NAVER](https://naver.com "링크 설명(title)을 작성하세요.")

[상대적 참조](../users/login)

[Dribbble][Dribbble link]

[GitHub][1]

문서 안에서 [참조 링크]를 그대로 사용할 수도 있습니다.

다음과 같이 문서 내 일반 URL이나 꺾쇠 괄호(`< >`, Angle Brackets)안의 URL은 자동으로 링크를 사용합니다.
구글 홈페이지: https://google.com
네이버 홈페이지: <https://naver.com>

[Dribbble link]: https://dribbble.com
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"
```

[GOOGLE](https://google.com)

[NAVER](https://naver.com "링크 설명(title)을 작성하세요.")

[상대적 참조](../users/login)

[Dribbble][dribbble link]

[GitHub][1]

문서 안에서 [참조 링크]를 그대로 사용할 수도 있습니다.

다음과 같이 문서 내 일반 URL이나 꺾쇠 괄호(`< >`, Angle Brackets)안의 URL은 자동으로 링크를 사용합니다.
구글 홈페이지: https://google.com
네이버 홈페이지: <https://naver.com>

[dribbble link]: https://dribbble.com
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"

# `이미지(Images)`

- `<img>`로 변환됩니다.  
  링크와 비슷하지만 앞에 ! 가 붙습니다.

```
![대체 텍스트(alternative text)를 입력하세요!](http://www.gstatic.com/webp/gallery/5.jpg "링크 설명(title)을 작성하세요.")

![Kayak][logo]

[logo]: http://www.gstatic.com/webp/gallery/2.jpg "To go kayaking."
```

![대체 텍스트(alternative text)를 입력하세요!](http://www.gstatic.com/webp/gallery/5.jpg "링크 설명(title)을 작성하세요.")

![Kayak][logo]

![logo]: http://www.gstatic.com/webp/gallery/2.jpg "To go kayaking."

# `코드(code) 강조`

`<pre>`, `<code>`로 변환됩니다.  
숫자 1번키 왼쪽에 있는 ` (Grave)를 입력하세요.

- 인라인(Inline) 코드 강조

```
`background`혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.
```

`background`혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.

- 블록(Block) 코드 강조  
  ` 를 3번 이상 입력하고 코드 종류도 적습니다.

```html
<a href="https://www.google.co.kr/" target="_blank">GOOGLE</a>
```

```css
.list > li {
  position: absolute;
  top: 40px;
}
```

```javascript
function func() {
  var a = "AAA";
  return a;
}
```

```bash
$ vim ./~zshrc
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting.
But let's throw in a tag.
```

# `표(Table)`

- `<table>` 태그로 변환됩니다.
  헤더 셀을 구분할 때 3개 이상의 -(hyphen/dash) 기호가 필요합니다.
  헤더 셀을 구분하면서 :(Colons) 기호로 셀(열/칸) 안에 내용을 정렬할 수 있습니다.
  가장 좌측과 가장 우측에 있는 |(vertical bar) 기호는 생략 가능합니다.

```
| 값 | 의미 | 기본값 |
|---|:---:|---:|
| `static` | 유형(기준) 없음 / 배치 불가능 | `static` |
| `relative` | 요소 자신을 기준으로 배치 |  |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |  |
| `fixed` | 브라우저 창을 기준으로 배치 |  |

값 | 의미 | 기본값
---|:---:|---:
`static` | 유형(기준) 없음 / 배치 불가능 | `static`
`relative` | 요소 **자신**을 기준으로 배치 |
`absolute` | 위치 상 **_부모_(조상)요소**를 기준으로 배치 |
`fixed` | **브라우저 창**을 기준으로 배치 |
```

| 값         |                  의미                  |   기본값 |
| ---------- | :------------------------------------: | -------: |
| `static`   |     유형(기준) 없음 / 배치 불가능      | `static` |
| `relative` |       요소 자신을 기준으로 배치        |          |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |          |
| `fixed`    |      브라우저 창을 기준으로 배치       |          |

| 값         |                     의미                     |   기본값 |
| ---------- | :------------------------------------------: | -------: |
| `static`   |        유형(기준) 없음 / 배치 불가능         | `static` |
| `relative` |        요소 **자신**을 기준으로 배치         |
| `absolute` | 위치 상 **_부모_(조상)요소**를 기준으로 배치 |
| `fixed`    |       **브라우저 창**을 기준으로 배치        |

# `인용문(BlockQuote)`

- `<blockquote>` 태그로 변환됩니다.

```
인용문(blockQuote)

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.
> _(네이버 국어 사전)_

BREAK!

> 인용문을 작성하세요!
>> 중첩된 인용문(nested blockquote)을 만들 수 있습니다.
>>> 중중첩된 인용문 1
>>> 중중첩된 인용문 2
>>> 중중첩된 인용문 3
```

인용문(blockQuote)

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.
> _(네이버 국어 사전)_

BREAK!

> 인용문을 작성하세요!
>
> > 중첩된 인용문(nested blockquote)을 만들 수 있습니다.
> >
> > > 중중첩된 인용문 1
> > > 중중첩된 인용문 2
> > > 중중첩된 인용문 3

# `원시 HTML(Raw HTML)`

- 마크다운 문법이 아닌 원시 HTML 문법을 사용할 수 있습니다.

```
<u>마크다운에서 지원하지 않는 기능</u>을 사용할 때 유용하며 대부분 잘 동작합니다.

<img width="150" src="http://www.gstatic.com/webp/gallery/4.jpg" alt="Prunus" title="A Wild Cherry (Prunus avium) in flower">

![Prunus](http://www.gstatic.com/webp/gallery/4.jpg)
```

<u>마크다운에서 지원하지 않는 기능</u>을 사용할 때 유용하며 대부분 잘 동작합니다.

<img width="150" src="http://www.gstatic.com/webp/gallery/4.jpg" alt="Prunus" title="A Wild Cherry (Prunus avium) in flower">

![Prunus](http://www.gstatic.com/webp/gallery/4.jpg)

# `수평선(Horizontal Rule)`

- 각 기호를 3개 이상 입력하세요.

```
---
(Hyphens)

***
(Asterisks)

___
(Underscores)
```

---

(Hyphens)

---

(Asterisks)

---

(Underscores)

# `줄바꿈(Line Breaks)`

```
동해물과 백두산이 마르고 닳도록
하느님이 보우하사 우리나라 만세   <!--띄어쓰기 2번-->
무궁화 삼천리 화려 강산<br>
대한 사람 대한으로 길이 보전하세
```

동해물과 백두산이 마르고 닳도록
하느님이 보우하사 우리나라 만세  
무궁화 삼천리 화려 강산<br>
대한 사람 대한으로 길이 보전하세
