---
layout: post
title: 코드잇 스프린트 6기 FE 위클리 페이퍼 4주차
subtitle: CodeIt Sprint Weekly Paper 4th Week
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: ["#코드잇스프린트", "#스프린트프론트엔드6기", "#취업까지달린다" ]
author: Jongwook Lee
---

# 4주차 위클리 과제 안내

<br>

{: .box-note}
**아래 두 가지 주제에 대해서 각자 조사해서 답변을 제출해 주세요.**<br>
**자바스크립트에서 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)에 대해 설명해 주세요.**<br>
**var, let, const 를 중복 선언 허용, 스코프, 호이스팅 관점에서 서로 비교해 주세요.**<br>
**제출은 위클리 페이퍼 답안 제출 설문에 일요일 23시 59분까지 해주시면 됩니다.**<br>



<br>

## 조사 내용

#### 1. 자바스크립트에서 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)에 대해 설명해 주세요.
- 먼저 얕은 복사와 깊은 복사를 이해하기 위해서는 자바스크립트 자료형의 개념을 알아야 한다.
	- 자바스크립트 내에서는 원시 값과 참조 값, 두 가지의 데이터의 값이 존재한다.
		- 원시 값은 새로운 메모리 공간에 독립적인 값을 저장하므로, 깊은 복사가 수행된다.
		- 참조 값은 얕은 복사로 수행된다. 
		- 원시 값과 참조 값의 큰 차이점은 원본이 바뀌면 참조 값은 복사본도 같이 변경되나, 원시 값은 변경되지 않는다.
		
		```
		// 원시 타입의 깊은 복사
		let a = '원본 데이터';
		let b = a;

		a = '수정 데이터';

		console.log(a); // '수정 데이터'
		console.log(b); // '원본 데이터'
		
		// 참조 타입의 얕은 복사
		let a = {name:'원본 데이터'};
		let b = a;
		
		a.name = '수정 데이터';
		
		console.log(a); // '수정 데이터'
		console.log(b); // '수정 데이터'
		```
		
- 얕은 복사 : 복사본의 속성이 복사본이 만들어진 원본 객체와 같은 참조를 공유하는 복사이다.
	- 원본이나 복사본을 변경하면, 다른 객체 또한 변경이 가능하다.
	- 원본과 복사본이 완전히 독립적인 깊은 복사의 동작과 대조적이다.
	- 다음 명제의 조건에서는 얕은 복사가 성립된다.
		- 두 객체가 같은 객체가 아니면서 속성은 같은 이름과 순서를 가지고 있다. 그리고 두 객체의 속성 값이 동일하다.
		**- 두 객체의 프로토타입 체인이 동일하다.**
	- 속성 값이 모두 원시 값인 객체 복사는 깊은 복사/얕은 복사 둘 다 해당된다.
		- 중첩된 속성이 없기 때문에 복사의 깊이와는 연관이 없다.
		- 주로 중첩된 속성을 변경하는 흐름에서 깊은 복사 여부를 비교한다.
	**-	얕은 복사는 중첩된 객체의 값이 아닌 최상위 속성만 복사한다.**
		- 복사본의 최상위 속성에 값을 재할당하여도 원본 객체에는 영향이 없다.
		- 복사본의 중첩 객체 속성을 재할당하면 원본 객체에 영향이 있다.
	- 자바스크립트 내에서 모든 표준 내장 객체의 복사 작업은 깊은 복사가 아닌 얕은 복사본을 생성한다.
		- Array.prototype.concat()
		- Array.prototype.slice()
		
		```
		const original = ['a',2,true,4,"hi"];
		const copy = original.slice();
		
		console.log(JSON.stringify(original) === JSON.stringify(copy)); // true
		
		copy.push(10);
		
		console.log(JSON.stringify(original) === JSON.stringify(copy)); // false
		
		console.log(original); // [ 'a', 2, true, 4, 'hi' ]
		console.log(copy); // [ 'a', 2, true, 4, 'hi', 10 ]
		```
		
		- Spread Syntax (전개 구문)
		
		```
		const obj = { a: 1 };
		const newObj = Object.assign({}, obj);
		
		newObj.a = 2;
		
		console.log(obj); // { a: 1 }
		console.log(obj === newObj); // false
		```
		
		- Array.From()
		- Object.assign()
		
		```
		const obj = { a: 1 };
		const newObj = Object.assign({}, obj);
		
		newObj.a = 2;
		
		console.log(obj); // { a: 1 }
		console.log(obj === newObj); // false
		```
		
		- Object.create()
		
- 깊은 복사 : 배열을 포함한 객체의 복사본의 속성이 복사본이 만들어진 원본 객체와 같은 참조를 공유하지 않는 복사
	- 따라서, 원본이나 복사본을 변경할 때, 다른 객체가 변경되지 않는 것을 보장 가능하다.
	- 원본이나 복사본의 중첩된 속성을 변경하면 다른 객체도 변경될 수 있는 얕은 복사와 대조적이다.
	- 다음 명제의 조건에서는 구조적으로 동일한 객체로 평가한다.
		- 두 객체의 속성은 같은 이름과 순서를 가지면서, 속성값이 구조적으로 동일하다.
		**- 두 객체의 프로토타입 체인은 구조적으로 동일하다. 즉, Object.protype에서 상속된다.**
	- 동일한 객체일 때, 다음 명제 조건에선 깊은 복사가 성립된다.
		- 두 객체가 같은 객체가 아니면서, 속성이 같은 이름과 순서를 갖는다.
		**- 두 객체의 속성 값이 서로의 깊은 복사 값이면서, 두 객체의 프로토타입 체인이 구조적으로 동일하다.**
	- 깊은 복사는 프로토 타입 체인을 복사할 수도 있으며 아닐 수도 있다.
		- 구조적으로 동일하지 않은 프로토아입 체인을 가진 두 객체는 서로의 복사본이 아니다.
	- 깊은 복사를 수행하는 방법은 직렬화로, JSON.stringify()를 사용하여 객체를 JSON 문자열로 변환하고, JSON.parse()를 통해 문자열을 완전히 새로운 객체로 만드는 방법이 있다.
		- 또 다른 방법으로는 객체의 깊이만큼 얕은 복사를 수행하면 된다. 
		- 많은 Javascript 객체는 직렬화가 불가능한 경우도 존재한다. 대표적으로 함수(클로저 포함), 심볼, HTML DOM API 내 HTML 요소를 나타내는 객체, 재귀 데이터 등이 존재한다.
		
		```
		const obj = {
			a: 1,
			b: {
				c: 2,
			},
		};
		
		const newObj = JSON.parse(JSON.stringify(obj));
		
		newObj.b.c = 3;
		
		console.log(obj); // { a: 1, b: { c: 2 } }
		console.log(obj.b.c === newObj.b.c); // false
		```
		
	- 깊은 복사는 원본 객체와 참조를 공유하지 않기 때문에 깊은 복사본에 어떠한 변경이 있더라도 원본 객체에 영향을 주지 않는다.		
	- Web API 중 structuredClone()를 통해 깊은 복사본을 만든 후, 원본에서 전송가능한 객체를 복사하는 대신 새로운 복사본으로 전송할 수 있다.
		- Error와 같은 더 많은 데이터 타입의 처리를 할 수 있다.
		- 해당 기능은 자바스크립트 고유의 기능이 아니다.
		- 직렬화와 동일하게 직렬화할 수 없는 객체는 깊은 복사를 수행할 수 없다.
	- 커스텀 재귀 함수를 통해 직접적으로 DFS 알고리즘을 활용하여 깊은 복사를 수행할 수 있다.
		
		```
		function deepCopy(obj) {
			if (obj === null || typeof obj !== "object") {
				return obj;
			}
			
			let copy = {};
			for (let key in obj) {
				copy[key] = deepCopy(obj[key]);
			}
			return copy;
		}
		
		const obj = {
		a: 1,
		b: {
			c: 2,
		},
		func: function () {
			return this.a;
		},
		};
		
		const newObj = deepCopy(obj);
		
		newObj.b.c = 3;
		console.log(obj); // { a: 1, b: { c: 2 }, func: [Function: func] }
		console.log(obj.b.c === newObj.b.c); // false
		```
		
	- Lodash 라이브러리의 cloneDeep 메소드와 같이 라이브러리를 활용하여 안전하게 깊은 복사를 할 수 있다.
		- 설치를 해야한다는 단점은 가지고 있으나, 실무에서는 Lodash를 사용하여 깊은 복사를 많이 수행한다.
		
		```
		// & npm i lodash 으로 설치
		const lodash = require("lodash");
		
		const obj = {
		a: 1,
		b: {
			c: 2,
		},
		func: function () {
			return this.a;
		},
		};
		
		const newObj = lodash.cloneDeep(obj);
		
		newObj.b.c = 3;
		console.log(obj); // { a: 1, b: { c: 2 }, func: [Function: func] }
		console.log(obj.b.c === newObj.b.c); // false
		```
		
- 깊은 복사와 얕은 복사를 선택하는 기준
	- 객체가 내부에 객체를 소유하는 경우에 깊은 복사를 선택한다.
	- 객체가 내부에 객체를 소유하지 않고 단순한 값들의 집합인 경우 얕은 복사를 선택한다.
	- 객체에 대한 소유권 개념이 필요한 경우, 깊은 복사를 선택한다.
	
- 깊은 복사와 얕은 복사의 장단점
	- 깊은 복사는 안전하고 독립적인 복사를 제공하지만, 메모리 사용량이 더 많아진다.
	- 얕은 복사는 메모리 사용량이 적으나, 객체의 복사가 어려울 수 있으며, 의도치 않은 결과를 유발할 수 있다.
	
<br>	

#### 2. var, let, const 를 중복 선언 허용, 스코프, 호이스팅 관점에서 서로 비교해 주세요
- 먼저 var, let, const를 이해하기 위해서는 변수의 각 단계에 대해 알아야 한다.
	- 변수는 선언 단계, 초기화 단계, 할당 단계라는 3가지 단계를 거쳐 생성된다.
	    - 선언 단계는 변수의 이름을 선언하는 단계이다.
		- 초기화 단계는 undefined를 할당하는 단계이다.
		- 할당 단계는 값을 변수에 넣는 단계이다.
	- var는 선언과 초기화가 동시에 진행된다.
		- 할당 전 호출하는 경우, 오류 대신 undefined를 반환한다.
	- let은 선언 단계, 초기화 단계, 할당 단계로 진행된다.
		- 초기화 단계는 실제 코드에 도달했을 때 진행되기 때문에 참조 에러가 발생된다.
	- const는 선언, 초기화, 할당 단계가 동시에 진행된다.	

- var, let, const를 중복 선언 허용, 스코프, 호이스팅 관점에서 바라본 결과를 표로 정리하면 아래와 같다.

  | 브랜치명       |   중복 선언   |   재할당    |   스코프     |   호이스팅    |   선언 및 초기화 |
  | :------------ | :-----------| :-----------| :-----------| :-----------| :--------------|
  | `var` | O | O | 함수 범위 스코프 | O | 별도로 가능 |
  | `let` | X | O |  지역 범위 스코프 | O (블록 내 발생) | 별도로 가능하나 TDZ가 존재 |
  | `const` | X | X | 지역 범위 스코프 | O (블록 내 발생) | 한 문장 내에서 전부 이뤄져야 함 |
  
- var
	- variable의 약어로써 ES6가 등장하기 이전까지 사용하던 변수 선언 키워드 중 하나이다.
	- var는 한번 선언된 변수를 재선언할 수 있다.
	
	```
	var name = 'Mike';
	console.log(name);
	var name = 'Jane';
	console.log(name);
	```
	
	- var는 선언되기 전에 사용할 수 있다.
		- var가 선언되기 전에 사용가능한 이유는 호이스팅으로 인한 변수로 이동으로 가능하다.
		- undefined가 출력되는 이유는 선언만 호이스팅이 되기 때문이다.
		- 자바스크립트는 바로 아래의 코드를 다음 아래의 코드 형태로 해석한다.
		
			```
			console.log(name); // undefined
			var name = 'Mike';
			```
			```
			var greeter;
			console.log(greeter); // greeter is undefined
			greeter = "say hello"
			```
			
	- var는 전역 범위 혹은 함수 범위로 지정된다.
		- var가 함수 외부에서 선언될 때의 범위는 전역이다.
		- 함수 블록 외부에서 var를 사용하면 선언된 모든 변수를 전체 브라우저 상에서 사용할 수 있다.
		- var가 함수 내부에 선언될 때는 함수 범위로 지정된다.
			- 해당 함수 내에서만 사용하고 접근만 가능하다.
	- var가 가진 문제점은 재정의로 인해 값의 충돌이 발생되어 예상 외의 결과 값이 출력될 수 있다.
		- 특히 함수 외에 값은 모두 전역 범위로 취급하므로, 코드 양이 많아지면 값의 변경을 추적하기도 어려워진다.	
			

- let
  - let은 var 선언에 따른 값 변경 추적 문제를 해결할 수 있다.
  - let은 var와 다르게 블록 범위로 바인딩된다.
	- 여기서 블록은 {} (중괄호)로 묶인 것들을 의미한다.
  - let으로 선언된 변수는 해당 블록 내에서만 유효하다.
	- 그렇기 때문에 값이 변경되는 경우, 예상 외의 결과 값의 출력도 막을 수 있다.
  - let은 값의 재할당은 가능하나, 재선언은 불가능하다.
	- 같은 블록 내 재선언 시, 에러가 발생되므로, 값의 변경 추적도 용이하다.	
  - let도 호이스팅이 가능하다.
	  - var와 동일하게 선언이 맨 위로 이동되지만 초기화는 발생되지 않는다.
	  - 또한, 선언 이전에 사용하는 경우, 아래와 같이 Reference Error가 발생된다.
	  
	  ```
	   console.log(name); // Error 발생
	   let name = 'Mike'; 
	  ```
	  
	  - let에서 호이스팅이 가능하지만, var와 다르게 오류가 발생되는 이유는 TDZ(Temporary Dead Zone)으로 인해 할당되지 전까지 사용할 수 없기 때문이다.
		- TDZ는 코드를 예측 가능하도록 만듦에 따라 잠재적인 버그를 줄이는 데 도움을 준다.

- const
  - const는 constant의 약어로, const로 선언된 변수는 일정한 상수 값을 유지한다.
  - const는 let과 유사한 점이 존재한다.
	- let과 같이 블록 범위로 동작한다.
	- let과 같이 재선언도 불가능하다.
  - const와 let이 다른 점은 하기와 같다.
	- let과 다르게 재할당이 불가능하다.
	- const는 선언과 동시에 초기화가 진행되어야 한다.
	- 단 const로 선언된 객체의 내부 값은 변경할 수 있다.
  - const도 호이스팅이 가능하다.
	- let과 동일하게 선언이 맨 위로 올려지나, 초기화가 되지는 않는다.
	
	```
	console.log(name); // Temporal Dead Zone
	const name = 'Mike';
	console.log(name);
	```
	
<br>	

#### 3. 참조

  | Features      | Links                                                  |
  | :------------ | :----------------------------------------------------- |
  | MDN 공식 문서  | [링크로 이동](https://developer.mozilla.org/ko/docs/Glossary/Deep_copy)|
  | 벨로그 | [링크로 이동](https://velog.io/@y_jem/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%99%80-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC) |
  | 프리 코드 캠프 | [링크로 이동](https://www.freecodecamp.org/korean/news/var-let-constyi-caijeomeun/) |
  