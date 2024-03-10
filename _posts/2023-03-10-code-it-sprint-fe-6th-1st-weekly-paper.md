---
layout: post
title: 코드잇 스프린트 6기 FE 위클리 페이퍼 1주차
subtitle: CodeIt Sprint Weekly Paper 1st Week
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [books, test]
author: Jongwook Lee
---

---

# 1주차 위클리 과제 안내

{: .box-note}
**아래 한 가지 주제에 대해서 각자 조사해서 답변을 제출해 주세요.**
**CSS의 Cascading에 대해 설명해 주세요.**
** 제출은 위클리 페이퍼 답안 제출 설문에 일요일 23시 59분까지 해주시면 됩니다.**

---

<br>

## 조사 내용

### CSS와 CSS의 Cascading은 무엇인가?

- CSS란, Cascading Style Sheets의 약어로 HTML이나 XML로 작성된 문서의 표시 방법을 기술하기 위한 스타일 시트 언어입니다.
- 주로 웹 페이지의 디자인과 레이아웃을 정의하여 사용자들에게 시각적인 디자인을 제공하기 위해 필수적입니다.
- 스타일이 제대로 적용되지 않는 이유는 Cascading의 영향일 확률이 높습니다.
- CSS에서의 Cascading은 '위에서 아래로 흐르는' 혹은 '상속 또는 종속하는'의 의미처럼 스타일 규칙이 계단식으로 적용되는 방식을 말합니다.
- 일반적으로 여러 개의 스타일 규칙이 같은 HTML 요소에 적용될 수 있는데, 이 때 어떤 규칙이 우선 순위가 높은지 판단해야 합니다.
  - Cascading에서 규칙이 더 구체적일수록 우선 순위가 높아집니다.
- MDN 혹은 W3 문서에서는 User-Agent가 다양한 출처에서 오는 속성 값을 어떻게 결합하는 지 정의하는 알고리즘이라고 알려주고 있습니다.
  - User-Agent는 우리가 사용하는 웹 브라우저 속에 숨겨진 중요한 기능 중의 하나로써 사용자의 OS, 버전, 웹 브라우저, 디바이스 등의 정보를 가지고 있습니다.
  - 과거에는 웹 브라우저마다 자체 엔진을 사용했는데 브라우저마다 기능에 대한 지원 범위, 호환성이 다르기 때문에 어떤 브라우저에서는 어떤 문제가 발생하는 지를 기록했습니다.
    - 즉 여러 웹 브라우저에서 호환성을 유지하기 위해 사용합니다.
    - 하지만 현재에는 대부분의 브라우저들이 크롬 기반의 블링크 엔진을 사용하므로 그럴 필요성이 적어졌습니다.
    - 최근에는 접속한 기기의 정보나 OS를 구분하는 데에 많이 사용하고 있습니다.
- 결론적으로, CSS는 여러 곳에서 중복으로 작성할 수 있기 때문에 실제로 어떤 스타일이 적용되는지는 우선 순위에 따라 결정될 수 있습니다.
  <br>

### CSS에서의 우선 순위 결정 기준

- CSS에서 우선 순위를 결정하는 기준은 하기와 같습니다.

  - Origin 우선 순위

    - Origin은 어떤 원천으로부터 적용되었는지, CSS 규칙이 어디서 왔는지를 말합니다. (쉽게 말하면, CSS 스타일 제공 주체)
      1.  User-Agent Stylesheet
      - 사용자 에이전트나 브라우저에 기본적으로 내장된 스타일시트를 의미합니다.
      - 브라우저마다 기본 스타일이 조금씩 다르므로, 퍼블리싱을 할 때 noramlize.css나 reset.css처럼 공통 속성을 재정의하는 CSS를 작성합니다.
      - 예시로 <h1> 태그는 기본적으로 크고 굵게 표시되는 것을 예시로 들 수 있습니다.

    2. Author Stylesheet
       - 가장 일반적인 유형의 CSS로 웹 개발자가 작성한 스타일 시트를 의미합니다.
       - link로 import하여 사용하거나, <style> 블록에서 사용하거나, 인라인 스타일로 작성된 스타일시트를 모두 포함합니다.
       - 개발자가 웹사이트에서 <h1>태그에 color:blue 속성을 지정해놓았다면 해당 사이트에서 <h1>태그의 색상은 파란색으로 표시됩니다.
    3. User Stylesheet
       - 개발자가 아닌 웹사이트 사용자가 설정하는 스타일시트를 의미합니다.
       - 일부 사용자는 시각적 불편을 줄이기 위한 목적 등으로 자신만의 스타일시트를 브라우저에 적용할 수 있습니다.

  - Origin에 따른 일반적인 CSS 우선 순위는 하기와 같습니다.
    - Author Stylesheet > User Stylesheet > User Agent Stylesheet (왼쪽 기준으로 우선 순위가 높음)
  - 만일 !important가 포함된 속성이라면 우선 순위는 하기와 같아집니다.

    - User Agent Stylesheet > User Stylesheet > Author Stylesheet (왼쪽 기준으로 우선 순위가 높음)
    - 참조 이미지
      ![](img_01.png)
      ![](img_02.png)

  - Author Style 우선 순위

    - Author Stylesheet에서 작성할 수 있는 종류는 하기와 같습니다.
      1. 인라인 스타일(inline 스타일)
      - HTML 요소 내에 직접 적용된 스타일을 의미합니다.
        {% highlight javascript linenos %}
        <div style="color: red;">This is an inline style.</div>
        {% endhighlight %}
      2. 내부 스타일(internal/embedded style)
      - HTML 문서 내 `<head>` 섹션의 `<style>` 태그 내에 정의된 스타일을 의미합니다.
        {% highlight javascript linenos %}
        <style> .example { color: blue; } </style>
        {% endhighlight %}
      3. 외부 스타일(external style)
      - 외부 CSS 파일에 정의된 스타일을 의미합니다.
      - HTML 문서에서는 `<link>` 태그를 사용하여 외부 스타일 시트를 사용가능합니다.
        {% highlight javascript linenos %}
        <link rel="stylesheet" href="styles.css">
        {% endhighlight %}
      - Author Style 적용 방식에서의 우선 순위는 하기와 같습니다.
      - 인라인 스타일 > 내부 스타일 > 외부 스타일 (왼쪽 기준으로 우선 순위가 높음)

  - Specificity 우선순위

    - CSS 선택자의 특정성에 따라 결정됩니다.

      1. id 카테고리
         - id 선택자 (#id)
      2. class 카테고리
         - class 선택자 (.class)
         - 속성 선택자 ([type="text"], [title|="first"])
         - 의사 클래스 (:hover, checked, :nth-child(2n))
      3. type 카테고리
         - HTML 요소 선택자 (p, h1, span)
         - 의사요소 (::before, ::placeholder)
      4. 우선 순위에 영향을 미치지 않는 것들
         - 하기 선택자들은 스타일에 적용되지만 Casading 우선 순위에는 영향을 미치지 않습니다.
           - 전체 선택자 (\* : Asterisk)
           - :where() 의사 클래스

    - Specificity 우선 순위는 하기와 같습니다.
    - id 카테고리 > class 카테고리 > type 카테고리 (왼쪽 기준으로 우선 순위가 높음)
    - 위의 카테고리에 의거하여 최종 우선 순위는 카테고리별 점수가 결합하여 결정됩니다.
    - MDN 문서의 설명에는 0-0-0와 같은 형식으로 점수를 부여합니다.

    {% highlight javascript linenos %}
    #id {
     color: blue; /* category 1. 1-0-0 */
    }
    .class {
    	color: yellow; /* category 2. 0-1-0 */
    }
    p {
    	color: red; /* category 3. 0-0-1 */
    }
    * {
    	color: gray; /* category 4. 0-0-0 */
    }
    {% endhighlight %}

    {% highlight javascript linenos %}
    <p id="id" class="class">👋 Hello World!</p>
    {% endhighlight %}

  - 작성 순서에 따른 우선 순위 - 아래에 있을수록 우선 순위는 높아집니다.
    {% highlight javascript linenos %}
    .class {
      font-size: 12px;
      font-weight: 700;
      font-family: Pretendard;
      color: blue;
      color: red; /* 나중에 작성된 red color가 적용됨 */
    }
    {% endhighlight %}
    <br>

  ### 결론

  - 결과적으로 CSS는 스타일을 적용하는 과정에서 Casading 알고리즘을 사용하여 스타일 규칙의 우선 순위를 결정합니다.
  - 우선 순위를 판단하는 기준은 Origin, Specification, 스타일 적용 방법 등을 고려하여 우선 순위를 결정합니다.

  - 캐스캐이딩의 과정은 하기와 같은 진행됩니다.
    1.  스타일 규칙과 요소가 매치되었는지를 검사하여 해당 요소와 관련된 스타일 속성만 선별합니다.
    2.  Origin 및 !import 속성에 따른 우선 순위를 비교합니다.
    - User Agent vs. Author vs. User Stylesheet 간 우선 순위를 판단합니다. (이 때, Important 속성 사용 여부에 따라 우선 순위가 달라질 수 있습니다.)
    3.  Author Style 우선 순위에 따른 우선 순위를 비교합니다.
    - 인라인 -> 내부 -> 외부 간의 우선 순위를 판단합니다.
    4.  Specification 우선 순위
    - #id -> .class -> type 카테고리 순으로 우선 순위를 판단합니다.
    - 작성 순서에 따라 판단합니다.
    - 같은 요소에 동일한 속성이 선언되었을 경우, 나중에 선언된 스타일이 최종적으로 적용됩니다.
  - !important 속성이 적용된 스타일은 가장 우선 순위가 높습니다.
  - 이 때, !important 속성은 우선 순위를 최상위로 변경하므로 많이 사용할수록 디버깅을 복잡하게 만들어 코드의 유지보수를 어렵게 할 수 있으므로 지양하는 것을 권장합니다.

  {% highlight javascript linenos %}
  #hello {
    color: blue;
    font-size: 50px;
  }
  p.contents {
    color: gray;
    font-size: 20px;
    background-color: pink;
  }

  .highlight {
    background-color: yellow;
  }
  {% endhighlight %}

  {% highlight javascript linenos %}
  <p class="contents" id="hello">hello</p>
  <p class="contents"> this is css</p>
  <p class="contents">my awesome css</p>
  <p class="contents">lets go</p>
  {% endhighlight %}

### W3에서의 정의 내용

- CSS Cascade란 다른 소스들로부터 발생될 수 있는 적절한 값을 User-Agent (브라우저)가 혼합할 지 알려주는 알고리즘입니다.
  - Cascade는 순서 없이 주어진 HTML 요소나 주어진 속성들이 선언된 값들을 특정한 조건과 Cascade된 값을 통해 우선 순위를 결정하여 정렬합니다.

# 참조

| Features      | Links          |
| :------------ | :------------- |
| W3 공식 문서  | [:link:][ref1] |
| 참조 블로그 1 | [:link:][ref2] |
| 참조 블로그 2 | [:link:][ref3] |

[ref1](https://www.w3.org/TR/css-cascade-5/#cascading)
[ref2](https://makinghome.tistory.com/67)
[ref3](https://ttaerrim.tistory.com/60)
