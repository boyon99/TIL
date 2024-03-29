# 클로저

클로저(Closure)는 함수가 선언될 때의 유효범위(렉시컬 범위)를 기억하고 있다가, 함수가 외부에서 호출될 때 그 유효범위의 특정 변수를 참조할 수 있는 개념이다.

```js
function createCount() {
  let a = 0;
  return function () {
    return (a += 1);
  };
}

const count = createCount();

console.log(count()); // 1
console.log(count()); // 2
console.log(count()); // 3
```

## 렉시컬 스코프

자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다. 이를 렉시컬 스코프라고 한다.

```js
const x = 1;

function outer() {
  const x = 10;
  inter();
}

function inter() {
  console.log(x); // 1
}

outer();
```

<br/>

## 함수 객체의 내부 슬롯

함수는 자신의 내부 슬롯 `[[Environment]]`에 자신이 정의된 환경인 상위 스코프의 참조를 저장한다.

<br/>

## 클로저와 렉시컬 환경

외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다. 이러한 중첩 함수를 클로저라고 부른다.

```js
// 3번 시 outer함수는 중첩 함수 inner를 반환하고 생명주기를 마감한다. 이때 변수 x 역시 생명주기를 마감한다. 따라서 2번의 실행 결과 x를 참조할 수 없어 보이지만 4의 결과 10이 출력된다.
const x = 1;

// ①
function outer() {
  const x = 10;
  const inner = function () {
    console.log(x);
  }; // ②
  return inner;
}

// outer 함수를 호출하면 중첩 함수 inner를 반환한다.
// 그리고 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝되어 제거된다.
const innerFunc = outer(); // ③
innerFunc(); // ④ 10
```

<br/>

## 클로저의 활용

클로저는 상태를 안전하게 변경하고 유지하기 위해 사용한다. 즉, 상태가 의도치 않게 변경되지 않도록 상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하기 위해 사용한다.

```js
// 카운트 상태 변수는 전역 변수를 통해 관리되고 있기 때문에 누구나 접근할 수 있고 변경할 수 있다. 즉 좋지 않다.
let num = 0;

// 카운트 상태 변경 함수
const increase = function () {
  // 카운트 상태를 1만큼 증가 시킨다.
  return ++num;
};

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

```js
// 카운트 상태 변경 함수
const increase = (function () {
  // 카운트 상태 변수
  let num = 0;

  // 클로저
  return function () {
    // 카운트 상태를 1만큼 증가 시킨다.
    return ++num;
  };
})();

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

#### 반환된 함수는 자신만의 독립된 렉시컬 환경을 갖는다.

```js
// 함수를 인수로 전달받고 함수를 반환하는 고차 함수
// 이 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저를 반환한다.
function makeCounter(aux) {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;

  // 클로저를 반환
  return function () {
    // 인수로 전달 받은 보조 함수에 상태 변경을 위임한다.
    counter = aux(counter);
    return counter;
  };
}

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 함수로 함수를 생성한다.
// makeCounter 함수는 보조 함수를 인수로 전달받아 함수를 반환한다
const increaser = makeCounter(increase); // ①
console.log(increaser()); // 1
console.log(increaser()); // 2

// increaser 함수와는 별개의 독립된 렉시컬 환경을 갖기 때문에 카운터 상태가 연동하지 않는다.
const decreaser = makeCounter(decrease); // ②
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

<br/>

## 캡슐화와 정보 은닉

캡슐화는 프로퍼티와 메서드를 하나로 묶는 것을 말하며 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라고 한다. 이전까지는 정보 은닉을 완전하게 지원하지는 않으나 `private`필드가 제안되어 있는 상태이다.
