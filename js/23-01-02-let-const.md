### var 키워드로 선언한 변수의 문제점 
#### 변수 중복 선언 허용
```js
var x = 1;
var y = 1;

// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var x = 100;
// 초기화문이 없는 변수 선언문은 무시된다.
var y;

console.log(x); // 100
console.log(y); // 1
```

#### 함수 레벨 스코프로 함수의 코드 블록만 지역 스코프로 인정함
```js
var x = 1;

if (true) {
  // x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
  // 이는 의도치 않게 변수값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10
```

#### 변수 호이스팅에 의해 변수 선언문 이전에 변수를 참조할 수 있다.
```js
var i = 10;

// for문에서 선언한 i는 전역 변수이다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 i 변수의 값이 변경되었다.
console.log(i); // 5
```


<br/>


## let 키워드
#### 변수 중복 선언 금지
```js
var foo = 123;
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var foo = 456;

let bar = 123;
// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```

#### 블록 레벨 스코프로 모든 코드 블록을 지역 스코프로 인정한다.
```js
let foo = 1; // 전역 변수

{
  let foo = 2; // 지역 변수
  let bar = 3; // 지역 변수
}

console.log(foo); // 1
console.log(bar); // ReferenceError: bar is not defined
```

#### 변수 호이스팅이 발생하지 않는 것처럼 동작한다
선언 단계와 초기화 단계가 분리되어 진행한다. 초기화 단계는 변수 선언문에 도달할 때 실행되므로 변수 호이스팅이 발생하지 않는 것처럼 동작한다. 선언단계와 초기화단계 사이를 일시적 사각지대라고 부른다.
```js
// 런타임 이전에 선언 단계가 실행된다. 아직 변수가 초기화되지 않았다.
// 초기화 이전의 일시적 사각 지대에서는 변수를 참조할 수 없다.
console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

<br/>


## const 키워드
상수를 선언하기 위해 사용한다. 대부분 let 키워드와 동일하다.
#### 언과 동시에 초기화해야 한다. 그렇지 않으면 에러가 발생한다. 
```js
const foo = 1;
```

```js
const foo; // SyntaxError: Missing initializer in const declaration
```

#### 재할당이 금지된 변수를 의미하는 상수이다.
```js
const foo = 1;
foo = 2; // TypeError: Assignment to constant variable.
```

#### 일반적으로 상수의 이름은 대문자로 선언해 상수임을 명확히 나타낸다.
```js
// 세율을 의미하는 0.1은 변경할 수 없는 상수로서 사용될 값이다.
// 변수 이름을 대문자로 선언해 상수임을 명확히 나타낸다.
const TAX_RATE = 0.1;

// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

console.log(afterTaxPrice); // 110
```

#### const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.
```js
const person = {
  name: 'Lee'
};

// 객체는 변경 가능한 값이다. 따라서 재할당없이 변경이 가능하다.
person.name = 'Kim';

console.log(person); // {name: "Kim"}
```
