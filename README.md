# thymeleaf 기본기 다지기
## MVC 2편(1) (김영한)

### 목표
타임리프의 기본기능 이해 및 활용<br><br>

<div align="center">
<img src="https://img.shields.io/badge/thymeleaf-005F0F?style=for-the-badge&logo=thymeleaf&logoColor=white">
</div>

## thymeleaf
* 서버 사이드 랜더링(SSR)
* 네츄럴 템플릿
* 스프링 통합 지원

### 서버 사이드 랜더링(SSR)
타임리프는 백엔드 서버에서 **HTML을 동적으로 렌더링** 하는 용도로 사용된다.

### 네츄럴 템플릿
타임리프는 순수 HTML을 최대한 유지하는 특성

순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 
**네츄럴 템플릿(natural templates)** 이라 한다.

### 스프링 통합 지원
타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 지원한다.

### 타임리프 사용 선언
`<html xmlns:th="http://www.thymeleaf.org">`

### 기본 표현식
* 간단한 표현
  * 변수 표현식: `${...}`
  * 선택 변수 표현식: `*{...}`
  * 메시지 표현식: `#{...}`
  * 링크 URL(경로) 표현식: `@{...}`
  * 조각 표현식: `~{...}`
* 리터럴
  * 텍스트: `'text'`
  * 숫자: `1, 21, 3.11, 4.0`
  * 불린: `true, false`
  * 널: `null`
  * 리터럴 토큰: `one, sometext, main`
* 문자 연산
* 산술 연산
* 불린 연산
* 비교와 동등
* 조건 연산
* 특별한 토큰
