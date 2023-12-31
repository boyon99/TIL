## 다양한 함수의 형태

### 즉시 실행 함수 (IIFE, Immediately Invoked Function Expression)

함수 정의와 동시에 호출되는 함수를 의미하며 단 한 번만 호출되며 다시 호출할 수 없다. 사용하는 이유는 필요 없는 전역 변수의 생성을 줄일 수 있으며 외부에서 접근 할 수 없는 자체적인 스코프를 가지므로 private한 변수를 만들 수가 있기 때문이다.

```javascript
// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
})();
```

#### 즉시 실행 함수는 반드시 그룹 연산자(...)로 감사야 한다. 그 이외에 연산자를 사용해도 좋다.

```javascript
(function () {
  // ...
})();

(function () {
  // ...
})();

!(function () {
  // ...
})();

+(function () {
  // ...
})();
```

#### 일반 함수처럼 값을 반환할 수 있고 인수를 전달할 수 있다.

```javascript
// 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있다.
var res = (function () {
  var a = 3;
  var b = 5;
  return a * b;
})();

console.log(res); // 15

// 즉시 실행 함수에도 일반 함수처럼 인수를 전달할 수 있다.
res = (function (a, b) {
  return a * b;
})(3, 5);

console.log(res); // 15
```

<br/>

### 재귀함수

자기 자신을 호출하는 함수

```javascript
function countdown(n) {
  if (n < 0) return;
  console.log(n);
  countdown(n - 1); // 재귀 호출
}

countdown(10);
```

#### 함수 내부에서는 함수 이름을 호출해 자기 자신을 호출할 수 있다. 단, 외부에서는 식별자로 호출해야 한다.

```javascript
// 함수 표현식
var factorial = function foo(n) {
  // 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
  if (n <= 1) return 1;
  // 함수를 가리키는 식별자로 자기 자신을 재귀 호출
  return n * factorial(n - 1);
};

console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

<br/>

### 중첩함수

함수 내부에 정의된 함수. 내부 함수라고도 불린다. 중첩함수를 포함하는 함수를 외부함수라고 부른다. 중첩함수는 외부 함수 내부에서만 호출할 수 있다.

```javascript
function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }

  inner();
}

outer();
```

<br/>

### 콜백함수와 고차함수

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백 함수라고 하며 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수라고 한다.

```javascript
// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

<br/>

### 순수함수와 비순수 함수

외부 상태에 의존하지 않고 변경하지도 않는, 즉 부수 효과가 없는 함수를 순수 함수라고 하고 부수 효과가 있는 함수를 비순수 함수라고 한다. 또한 순수함수는 외부 상태를 변경하지 않으나 비순수 함수는 외부 상태를 변경하는 부수 효과가 있다.

```javascript
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
increase(count);
console.log(count); // 0

count = increase(count);
console.log(count); // 1
```

```javascript
var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```
