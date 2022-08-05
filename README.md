# thymeleaf 기본기 다지기

## MVC 2편(1) (김영한)

### 목표

타임리프의 기본기능 이해 및 활용



[![img](https://camo.githubusercontent.com/f1b9cef5b50e9524115cac99c65a1ec6dcb6119e6da797568c84ec51adaa0ef5/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f7468796d656c6561662d3030354630463f7374796c653d666f722d7468652d6261646765266c6f676f3d7468796d656c656166266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/f1b9cef5b50e9524115cac99c65a1ec6dcb6119e6da797568c84ec51adaa0ef5/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f7468796d656c6561662d3030354630463f7374796c653d666f722d7468652d6261646765266c6f676f3d7468796d656c656166266c6f676f436f6c6f723d7768697465)



## thymeleaf

- 서버 사이드 랜더링(SSR)
- 네츄럴 템플릿
- 스프링 통합 지원

### 서버 사이드 랜더링(SSR)

타임리프는 백엔드 서버에서 **HTML을 동적으로 렌더링** 하는 용도로 사용된다.

### 네츄럴 템플릿

타임리프는 순수 HTML을 최대한 유지하는 특성

순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 **네츄럴 템플릿(natural templates)** 이라 한다.

### 스프링 통합 지원

타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 지원한다.

### 타임리프 사용 선언

```
<html xmlns:th="http://www.thymeleaf.org">
```

### 기본 표현식

참고:  https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#standardexpression-syntax

- **간단한 표현**
  - 변수 표현식:  `${...}`
  - 선택 변수 표현식:  `*{...}`
  - 메시지 표현식:  `#{...}`
  - 링크 URL(경로) 표현식:  `@{...}`
  - 조각 표현식:  `~{...}`
- **리터럴**
  - 텍스트:  `'text'`
  - 숫자:  `1, 21, 3.11, 4.0`
  - 불린:  `true, false`
  - 널:  `null`
  - 리터럴 토큰:  `one, sometext, main`
- **문자 연산**
  - 문자 합치기:  `+`
  - 리터럴 대체:  `|the name is ${name}|`
- **산술 연산**
  - Binalry operators:  `+, -, *, /, % `
  - Minus sign(unary operator):  `-`
- **불린 연산**
  - Binary operators:  `and, or`
  - Boolean negation(unary operator):  `!, not`
- **비교와 동등**
  - 비교:  `>, <, >=, <= (gt, lt, ge, le)`
  - 동등 연산:  `==, !=, (eq, ne)`
- **조건 연산**
  - If- then: `(if) ? (then)`
  - If-then-else: `(if) ? (then) : (else)`
  - Defalut:  `(value) ?: (defaultvalue)`
- **특별한 토큰**
  - No-Operation: `_`



### 텍스트

`th:text`를 사용

**컨텐츠 안에서 직접 출력**하기 `[[${data}]]` 사용

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
 <meta charset="UTF-8">
 <title>Title</title>
</head>
<body>
<h1>컨텐츠에 데이터 출력하기</h1>
<ul>
 <li>th:text 사용 <span th:text="${data}"></span></li>
 <li>컨텐츠 안에서 직접 출력하기 = [[${data}]]</li>
</ul>
</body>
</html>
```



#### Escape

HTML문서는 `<`,` >`같은 특수 문자를 기반으로 정의된다.

따라서 뷰 템플릿으로 HTML화면을 생성할 때는 출력하는 데이터에 이러한 특수 문자가 있는 것을 **주의**해서 사용!



#### HTML 엔티티

브라우저는 `<`를 HTML태그의 시작으로 인식

따라서 `<`를 태그의 시작이 아닌 **문자로 표현할수 있는 방법**이 필요한데, 이것을 **HTML 엔티티**라고 한다.

이렇게 **특수문자를 HTML 엔티티로 변경하는 것을 escape**라고 한다.

**라임리프가 제공**하는 `th:text`, `[[...]]` 는 **기본적으로 escape를 제공**

**escape를 사용하지 않으려면** `th:utext`, `[(...)]`를 사용한다.



HTML에서 제공하는 대표적인 엔티티

| 엔티티 문자 | 엔티티 이름 | 16진수 엔티티 숫자 |       설명        |
| :---------: | :---------: | :----------------: | :---------------: |
|             |  `&nbsp;`   |      `&#160;`      | 줄 바꿈 없는 공백 |
|      <      |   `&lt;`    |      `&#60;`       |     보다 작은     |
|      >      |   `&gt;`    |      `&#62;`       |      보다 큰      |
|      &      |   `&amp;`   |      `&#38;`       |     AND 기호      |
|      "      |  `&quot;`   |      `&#34;`       |     큰따옴표      |
|      '      |  `&apos;`   |      `&#39;`       |    작은따옴표     |



예시

```html
<h1>text vs utext</h1>
<ul>
    <li>th:text = <span th:text="${data}"></span></li>
    <li>th:utext = <span th:utext="${data}"></span></li>
</ul>
<h1><span th:inline="none">[[...]] vs [(...)]</span></h1>
<ul>
    <li><span th:inline="none">[[...]] = </span>[[${data}]]</li>
    <li><span th:inline="none">[(...)] = </span>[(${data})]</li>
</ul>
```





### 변수 - SpringEL

타임리프에서 변수를 사용할 대는 변수 표현식을 사용

변수 표현식: `${...}`



#### object

* `user.username`: `user.getUsername()`과 동일
* `user['username']`: `user.getUsername()`과 동일
* `user.getUsername()`: `user의 getUsername()`을 직접 호출

#### List

* `users[0].username`: List에서 첫 번째 회원을 찾고 username 프로퍼티 접근 -> `list.get(0).getUsername()`
* `users[0]['usern']`: 위와 동일
* `users[0].getUsername()`: List에서 첫 번째 회원을 찾고 메서드 직접 호출

#### Map

* `userMap['userA'].username`: Map에서 userA를 찾고, username 프로퍼티 접근 -> `map.get("userA").getUsername()`
* `userMap['userA']['username']`: 위와 같음
* `userMap['userA'].getUsername()`: Map에서 userA를 찾고 메서드 직접 호출



#### 지역변수

`th:with`를 사용하면 지역변수를 선언해서 사용

선언한 태그 안에서만 사용할 수 있다.

```html
<h1>지역 변수 - (th:with)</h1>
<div th:with="first=${users[0]}">
 	<p>처음 사람의 이름은 <span th:text="${first.username}"></span></p>
</div>
```





### 기본 객체들

타임리프는 기본 객체들을 제공

* `${#request}`
* `${#response}`
* `${#session}`
* `${#servletContext}`
* `${#locale}`



`#request`는 `HttpServletRequest`객체가 그대로 제공되기 때문에, 데이터를 조회하려면 `request.getParameter("data")`처럼 불편하게 접근

이러한 문제를 해결하기 위해 편의 객체를 제공

* **HTTP 요청 파라미터** 접근: `param`
  * `${param.paramData}`
* **HTTP 세션** 접근: `session`
  * `${session.sessionData}`
* **스프링 빈** 접근: `@`
  * `${@helloBean.hello('Spring!')}`





### 유티리티 객체와 날짜

* `#message`:  메시지, 국제화처리
* `#uris`: URI 이스케이프 지원
* `#dates`: java.util.Date 서식 지원
* `#calendars`: java.util.Calendar 서식 지원
* `#temporals`: 자바8 날짜 서식 지원
* `#numbers`: 숫자 서식 지원
* `#strings`: 문자 관련 편의 기능
* `#objects`: 객체 관련 기능 제공
* `#bools`:  boolean 관련 기능 제공
* `#arrays`: 배열 관련 기능 제공
* `#lists`, `#sets`, `#maps`: 컬렉션 관련 기능 제공
* `#ids`: 아이디 처리 관련 기능 제공



유틸리티 객체

* https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#expression-utilityobjects

유틸리티 객체 예시

* https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expressionutility-objects





#### 자바8 날짜

자바8 날짜용 유틸리티 객체

`#temporals`



```html
<span th:text="${#temporals.format(localDateTime, 'yyyy-MM-dd HH:mm:ss')}"></span>
```



#### URI 링크

`@{...}` 문법을 사용



**단순한 URL**

* `@{/hello}`

**쿼리 파라미터**

* `@{/hello(param1=${param1}, param2=${param2})}`
* param1, 2의 값에 따라 `/hello?param1=data1&param2=data2` 같이 처리

**경로 변수**

* `@{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}`
  * `/hello/data1/data2`

**경로 변수 + 쿼리 파라미터**

* `@{/hello/{param1}(param1=${param1}, param2=${param2})}`
  * `/hello/data1?param2=data2`



상대경로, 절대경로, 프로토콜 기준을 표현할 수 도 있다.

* `/hello`: 절대 경로
* `hello`: 상대 경로
* 참고: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#link-urls





### 리터럴(Literals)

리터럴이란 **소스 코드상에 고정된 값**을 말하는 용어

