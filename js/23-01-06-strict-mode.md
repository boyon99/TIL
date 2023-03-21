# strict mode

### 암묵적 전역
```js
function foo() {
  x = 5;
}

foo();
console.log(x); // 10 
// 암묵적으로 전역 객체에 x 프로퍼티를 동적 생성하여 전역 변수처럼 사용할 수 있는데 이를 암묵적 전역이라고 한다. 이러한 예방을 하기 위해 엄격 모드가 도입되었다.
console.log(y); // ReferenceError: y is not defined
```

### 엄격 모드 
```js
"use strict"; // 선두에 위치시켜야 함

function foo() {
  x = 5;
}

foo();
console.log(x); // ReferenceError: x is not defined
console.log(y); // ReferenceError: y is not defined
```

<br/>

## strict mode가 발생시키는 에러
### 암묵적 전역
선언하지 않은 변수를 참조하면 reference error가 발생한다.
```js
(function () {
  'use strict';

  x = 1;
  console.log(x); // ReferenceError: x is not defined
}());
```

### 변수, 함수, 매개변수의 삭제 
delete 연산자로 변수, 함수, 매개변수를 삭제하면 syntaxerror가 발생한다.
```js
(function () {
  'use strict';

  var x = 1;
  delete x;
  // SyntaxError: Delete of an unqualified identifier in strict mode.

  function foo(a) {
    delete a;
    // SyntaxError: Delete of an unqualified identifier in strict mode.
  }
  delete foo;
  // SyntaxError: Delete of an unqualified identifier in strict mode.
}());
```

### 매개변수 이름의 중복
중복된 매개변수 이름을 사용하면 syntaxerror가 발생한다.
```js
(function () {
  'use strict';

  //SyntaxError: Duplicate parameter name not allowed in this context
  function foo(x, x) {
    return x + x;
  }
  console.log(foo(1, 2));
}());
```

### with 문의 사용
with 문 사용 시 syntaxerror가 발생한다.
```js
(function () {
  'use strict';

  // SyntaxError: Strict mode code may not include a with statement
  with({ x: 1 }) {
    console.log(x);
  }
}());
```

<br/>

## strict mode 적용에 의한 변화
### 일반 함수의 this
strict mode에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다.
```js
(function () {
  'use strict';

  function foo() {
    console.log(this); // undefined
  }
  foo();

  function Foo() {
    console.log(this); // Foo
  }
  new Foo();
}());
```

### arguments 객체
strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.
```js
(function (a) {
  'use strict';
  // 매개변수에 전달된 인수를 재할당하여 변경
  a = 2;

  // 변경된 인수가 arguments 객체에 반영되지 않는다.
  console.log(arguments); // { 0: 1, length: 1 }
}(1));
```
