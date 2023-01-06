# 자바스크립트 객체의 분류
- ### 표준 빌트인 객체
  ECMAScript 사양에 정의된 객체를 말하며 애플리케이션 전역의 공통 기능을 제공한다. 자바스크립트 실행 환경과 관계없이 언제나 사용할 수 있으며 전역 객체의 프로퍼티로서 제공된다. 따라서 별도의 선언 없이 전역 변수처럼 언제나 참조할 수 있다.
- ### 호스트 객체
  CMAScript에는 정의되어 있지 않지만 자바스크립트 실행환경에서 추가로 제공되는 객체를 말한다. 브라우저 환경에서는 DOM, BOM, Canvas 등과 같은 클라이언트 사이드 Web API를 호스트 객체로 제공하고 있고 Node.js 환경에서는 Node.js 고유의 API를 호스트 객체로 제공한다.
- ### 사용자 정의 객체
  표준 빌트인 객체와 호스트 객체처럼 기본 제공되는 객체가 아닌 사용자가 직접 정의한 객체를 의미한다.
  
  
<br/>

## 표준 빌트인 객체
`Object` `String` `Math` `Date` `Map` `Function` `JSON` `Error` 등 40여개의 표준 빌트인 객체를 제공한다. `Math` `Reflect` `JSON`을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체이다. 생성자 함수 객체인 표준 빌트인 객체는 프로토타입 메서드와 정적 메서드를 제공하고 생성자 함수 객체가 아닌 표준 빌트인 객체는 정적 메서드만 제공한다.

```js
// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(1.5); // Number {1.5}

// toFixed는 Number.prototype의 프로토타입 메서드다.
// Number.prototype.toFixed는 소수점 자리를 반올림하여 문자열로 반환한다.
console.log(numObj.toFixed()); // 2

// isInteger는 Number의 정적 메서드다.
// Number.isInteger는 인수가 정수(integer)인지 검사하여 그 결과를 Boolean으로 반환한다.
console.log(Number.isInteger(0.5)); // false
```

<br/>

## 원시 값과 래퍼 객체
자열, 숫자, 불리언, 심벌 원시 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 래퍼 객체라고 한다. null과 undefined에 경우 객체처럼 사용하면 에러가 발생한다.
```js
const str = 'hi';

// 원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 변환된다.
console.log(str.length); // 2
console.log(str.toUpperCase()); // HI

// 래퍼 객체로 프로퍼티에 접근하거나 메서드를 호출한 후, 다시 원시값으로 되돌린다.
console.log(typeof str); // string
```


<br/>

## 전역객체
코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며 어떤 객체에도 속하지 않는 최상위 객체이다. 브라우저 환경에서는 window가, Node.js 환경에서는 global이 전역 객체를 가리킨다. 전역 객체는 표준 빌트인 객체, 호스트 객체, var 키워드로 선언한 전역 변수와 전역 함수를 프로퍼티로 갖는다. 
#### 전역객체를 생성할 수 있는 생성자 함수가 제공되지 않으며 프로퍼티 참조 시 window나 global은 생략할 수 있다.
```js
// 문자열 'F'를 16진수로 해석하여 10진수로 변환하여 반환한다.
window.parseInt('F', 16); // -> 15
// window.parseInt는 parseInt로 호출할 수 있다.
parseInt('F', 16); // -> 15

window.parseInt === parseInt; // -> true
```

#### 전역객체는 표준 빌트인 객체를 프로퍼티로 가지고 있으며 var 키워드로 선언한 전역 변수와 선언하지 않은 변수에 암묵적 전역을, 전역 함수는 전역 객체의 프로퍼티가 된다. 
```js
// var 키워드로 선언한 전역 변수
var foo = 1;
console.log(window.foo); // 1

// 선언하지 않은 변수에 값을 암묵적 전역. bar는 전역 변수가 아니라 전역 객체의 프로퍼티다.
bar = 2; // window.bar = 2
console.log(window.bar); // 2

// 전역 함수
function baz() { return 3; }
console.log(window.baz()); // 3
```

#### let, const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 
```js
let foo = 123;
console.log(window.foo); // undefined
```

<br/>

### 빌트인 전역 프로퍼티
전역 객체의 프로퍼티를 의미한다. 애플리케이션 전역에서 사용하는 값을 제공한다.
#### Infinity 프로퍼티는 무한대를 나타내는 숫자값을 갖는다.
```js
// 전역 프로퍼티는 window를 생략하고 참조할 수 있다.
console.log(window.Infinity === Infinity); // true

// 양의 무한대
console.log(3/0);  // Infinity
// 음의 무한대
console.log(-3/0); // -Infinity
// Infinity는 숫자값이다.
console.log(typeof Infinity); // number
```
#### NaN 프로퍼티는 숫자가 아님을 나타내는 숫자값을 갖는다.
```js
console.log(window.NaN); // NaN

console.log(Number('xyz')); // NaN
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number
```

#### undefined 프로퍼티는 원시 타입 undefined를 값으로 갖는다.
```js
console.log(window.undefined); // undefined

var foo;
console.log(foo); // undefined
console.log(typeof undefined); // undefined
```

<br/>

### 빌트인 전역 함수
애플리케이션 전역에서 호출할 수 있는 빌트인 함수로서 전역 객체의 메서드이다.

#### eval
자바스크립트 코드를 나타내는 문자열을 인수로 전달받는다. 표현식이라면 런타임에 평가하여 값을 생성하고 표현식이 아닌 문이라면 런타임에 실행한다.
```js
// 표현식인 문
eval('1 + 2;'); // -> 3
// 표현식이 아닌 문
eval('var x = 5;'); // -> undefined

// eval 함수에 의해 런타임에 변수 선언문이 실행되어 x 변수가 선언되었다.
console.log(x); // 5

// 객체 리터럴은 반드시 괄호로 둘러싼다.
const o = eval('({ a: 1 })');
console.log(o); // {a: 1}

// 함수 리터럴은 반드시 괄호로 둘러싼다.
const f = eval('(function() { return 1; })');
console.log(f()); // 1
```
여러 문인 경우 모든 문을 실행한 후 마지막 결과값을 반환한다.
```js
console.log(eval('1 + 2; 3 + 4;')); // 7
```
자신이 호출된 위치에 해당하는 기존의 스코프를 런타임에 동적으로 수정한다. 그리고 그 위치에 존재하던 코드처럼 동작한다.
```js
const x = 1;

function foo() {
  // eval 함수는 런타임에 foo 함수의 스코프를 동적으로 수정한다.
  eval('var x = 2;');
  console.log(x); // 2
}

foo();
console.log(x); // 1
```
단 엄격모드에서는 자체적인 스코프를 생성한다. 
```js
const x = 1;

function foo() {
  'use strict';

  // strict mode에서 eval 함수는 기존의 스코프를 수정하지 않고 eval 함수 자신의 자체적인 스코프를 생성한다.
  eval('var x = 2; console.log(x);'); // 2
  console.log(x); // 1
}

foo();
console.log(x); // 1
```
또한 let, const 키워드를 사용한 변수 선언문이면 암묵적으로 엄격모드가 적용된다.
```js
const x = 1;

function foo() {
  eval('var x = 2; console.log(x);'); // 2
  // let, const 키워드를 사용한 변수 선언문은 strict mode가 적용된다.
  eval('const x = 3; console.log(x);'); // 3
  console.log(x); // 2
}

foo();
console.log(x); // 1
```

> 최적화가 수행되지 않기 때문에 처리 속도가 느리다. eval 함수의 사용을 금지해야 한다.

#### isFinite
전달받은 인수가 유한수이면 true을 무한수이면 false를 반환한다. 숫자가 아니면 숫자로 변환한 후 검사를 수행한다. 인수가 NaN으로 평가받는 값이라면 false를 반환한다.
```js
// 인수가 유한수이면 true를 반환한다.
isFinite(0);    // -> true
isFinite(2e64); // -> true
isFinite('10'); // -> true: '10' → 10
isFinite(null); // -> true: null → 0

// 인수가 무한수 또는 NaN으로 평가되는 값이라면 false를 반환한다.
isFinite(Infinity);  // -> false
isFinite(-Infinity); // -> false

// 인수가 NaN으로 평가되는 값이라면 false를 반환한다.
isFinite(NaN);     // -> false
isFinite('Hello'); // -> false
isFinite('2005/12/12'); // -> false
```

#### isNaN
NaN이면 true을 반환한다.
```js
// 숫자
isNaN(NaN); // -> true
isNaN(10);  // -> false

// 문자열
isNaN('blabla'); // -> true: 'blabla' => NaN
isNaN('10');     // -> false: '10' => 10
isNaN('10.12');  // -> false: '10.12' => 10.12
isNaN('');       // -> false: '' => 0
isNaN(' ');      // -> false: ' ' => 0

// 불리언
isNaN(true); // -> false: true → 1
isNaN(null); // -> false: null → 0

// undefined
isNaN(undefined); // -> true: undefined => NaN

// 객체
isNaN({}); // -> true: {} => NaN

// date
isNaN(new Date());            // -> false: new Date() => Number
isNaN(new Date().toString()); // -> true:  String => NaN
```

#### parseFloat
전달받은 문자열 인수를 실수로 해석하여 반환한다. 
```js
// 문자열을 실수로 해석하여 반환한다.
parseFloat('3.14');  // -> 3.14
parseFloat('10.00'); // -> 10

// 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
parseFloat('34 45 66'); // -> 34
parseFloat('40 years'); // -> 40

// 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
parseFloat('He was 40'); // -> NaN

// 앞뒤 공백은 무시된다.
parseFloat(' 60 '); // -> 60
```

#### parseInt
전달받은 문자열 인수를 정수로 해석하여 반환한다. 
```js
// 문자열을 정수로 해석하여 반환한다.
parseInt('10');     // -> 10
parseInt('10.123'); // -> 10
```

2번째 인수로 진법을 나타내는 기수를 전달할 수 있다. 이때 반환값은 10진수이다.
```js
// 10'을 10진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10'); // -> 10
// '10'을 2진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 2); // -> 2
// '10'을 8진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 8); // -> 8
// '10'을 16진수로 해석하고 그 결과를 10진수 정수로 반환한다
parseInt('10', 16); // -> 16
```
0x 0X로 시작하는 16진수 리터럴이면 16진수로 해석하여 10진수 정수로 반환하지만 2진수와 8진수 리터럴은 제대로 해석하지 못한다. 
```js
// 16진수 리터럴 '0xf'를 16진수로 해석하고 10진수 정수로 그 결과를 반환한다.
parseInt('0xf'); // -> 15
// 위 코드와 같다.
parseInt('f', 16); // -> 15
// 2진수 리터럴(0b로 시작)은 제대로 해석하지 못한다. 0 이후가 무시된다.
parseInt('0b10'); // -> 0
// 8진수 리터럴(ES6에서 도입. 0o로 시작)은 제대로 해석하지 못한다. 0 이후가 무시된다.
parseInt('0o10'); // -> 0
```
첫번째 문자가 해당 지수의 숫자로 반환할 수 없다면 NaN을 반환하지만 2번째 문자부터 숫자가 아니면 전부 무시되며 해석된 정수값만 반환한다.
```js
// 'A'는 10진수로 해석할 수 없다.
parseInt('A0'); // -> NaN
// '2'는 2진수로 해석할 수 없다.
parseInt('20', 2); // -> NaN
// 10진수로 해석할 수 없는 'A' 이후의 문자는 모두 무시된다.
parseInt('1A0'); // -> 1
// 2진수로 해석할 수 없는 '2' 이후의 문자는 모두 무시된다.
parseInt('102', 2); // -> 2
// 8진수로 해석할 수 없는 '8' 이후의 문자는 모두 무시된다.
parseInt('58', 8); // -> 5
// 16진수로 해석할 수 없는 'G' 이후의 문자는 모두 무시된다.
parseInt('FG', 16); // -> 15
```
앞뒤 공백은 무시하여 첫번째 문자열만 해석하여 반환한다.
```js
// 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
parseInt('34 45 66'); // -> 34
parseInt('40 years'); // -> 40
// 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
parseInt('He was 40'); // -> NaN
// 앞뒤 공백은 무시된다.
parseInt(' 60 '); // -> 60
```

#### encodeURL decodeURL
완전한 url을 문자열로 전달받아 이스케이프 처리를 위해 인코딩한다. url의 경우 아스키 문자 셋으로만 구성되어야 하므로 한글이나 특수문자의 경우 URL에 포함될 수 없다. 
```js
const uri = 'http://example.com?name=이웅모&job=programmer&teacher';

// encodeURI 함수는 완전한 URI를 전달받아 이스케이프 처리를 위해 인코딩한다.
const enc = encodeURI(uri);
console.log(enc);
// http://example.com?name=%EC%9D%B4%EC%9B%85%EB%AA%A8&job=programmer&teacher

// decodeURI 함수는 인코딩된 완전한 URI를 전달받아 이스케이프 처리 이전으로 디코딩한다.
const dec = decodeURI(enc);
console.log(dec);
// http://example.com?name=이웅모&job=programmer&teacher
```

#### encodeURLComponent decodeURLComponent
URL 구성요소를 인수로 전달받아 인코딩하거나 디코딩한다. 인코딩이란 URl의 문자들을 이스케이프 처리하는 것을 의미한다.
```js
// URI의 쿼리 스트링
const uriComp = 'name=이웅모&job=programmer&teacher';

// encodeURIComponent 함수는 인수로 전달받은 문자열을 URI의 구성요소인 쿼리 스트링의 일부로 간주한다.
// 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &까지 인코딩한다.
let enc = encodeURIComponent(uriComp);
console.log(enc);
// name%3D%EC%9D%B4%EC%9B%85%EB%AA%A8%26job%3Dprogrammer%26teacher

let dec = decodeURIComponent(enc);
console.log(dec);
// 이웅모&job=programmer&teacher

// encodeURI 함수는 인수로 전달받은 문자열을 완전한 URI로 간주한다.
// 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &를 인코딩하지 않는다.
enc = encodeURI(uriComp);
console.log(enc);
// name=%EC%9D%B4%EC%9B%85%EB%AA%A8&job=programmer&teacher

dec = decodeURI(enc);
console.log(dec);
// name=이웅모&job=programmer&teacher
```


