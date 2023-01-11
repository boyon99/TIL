# 고차 함수
고차 함수는 함수를 인수로 전달받거나 함수를 반환하는 함수를 말한다. 고차 함수는 외부 상태의 변경이나 가변 데이터를 피하고 불변성을 지향한다. 
이를 위해 조건문과 반복문을 제거하여 복잡성을 해결하고 변수의 사용을 억제하여 상태 변경을 피한다. 

#### 메서드
- Array.prototype.forEach
- Array.prototype.map
- Array.prototype.reduce

#### 변환
- Array.prototype.sort
- Array.prototype.flatMap

#### 참과 거짓
- Array.prototype.filter 
- Array.prototype.some 
- Array.prototype.every 
- Array.prototype.find 
- Array.prototype.findIndex 

> filter는 true인 요소를 반환하고 find는 true인 첫 요소를 반환하고 findIndex는 true인 첫 요소 인덱스를 반환한다.



<br/>

### Array.prototype.sort
배열의 요소를 정렬한다. 원본 배열을 직접 변경하며 정렬된 배열을 반환한다. 기본적으로 오름차순으로 요소를 정렬한다. 
```js
const fruits = ['Banana', 'Orange', 'Apple'];
const fruits2 = ['바나나', '오렌지', '사과'];

// 오름차순(ascending) 정렬
fruits.sort();
fruits2.sort();

// sort 메서드는 원본 배열을 직접 변경한다.
console.log(fruits); // ['Apple', 'Banana', 'Orange']
console.log(fruits2); // ['바나나', '사과', '오렌지']
```

#### 내림차순을 하려면 reverse 메서드를 사용한다. 
```js
const fruits = ['Banana', 'Orange', 'Apple'];
// 오름차순(ascending) 정렬
fruits.sort();
console.log(fruits); // ['Apple', 'Banana', 'Orange']

// 내림차순(descending) 정렬
fruits.reverse();
console.log(fruits); // ['Orange', 'Banana', 'Apple']
```

#### 숫자인 경우 유니코드 코드 포인트의 순서를 기준으로 정렬한다.
```js
const points = [40, 100, 1, 5, 2, 25, 10];

points.sort();

// 숫자 요소들로 이루어진 배열은 의도한 대로 정렬되지 않는다.
console.log(points); // [1, 10, 100, 2, 25, 40, 5]
```

#### 따라서 정렬 순서를 정의하는 비교 함수를 인수로 전달해야 한다. 
> 비교 함수는 양수나 음수 또는 0을 반환해야 한다. 비교 함수의 반환값이 0보다 작으면 비교 함수의 첫 번째 인수를 우선 정렬하고 0이면 정렬하지 않으면 0보다 크면 두 번째 인수를 우선하여 정렬한다. 

```js
const points = [40, 100, 1, 5, 2, 25, 10];

// 숫자 배열의 오름차순 정렬. 비교 함수의 반환값이 0보다 작으면 a를 우선하여 정렬한다.
points.sort((a, b) => a - b);
console.log(points); // [1, 2, 5, 10, 25, 40, 100]

// 숫자 배열에서 최소/최대값 취득
console.log(points[0], points[points.length]); // 1

// 숫자 배열의 내림차순 정렬. 비교 함수의 반환값이 0보다 작으면 b를 우선하여 정렬한다.
points.sort((a, b) => b - a);
console.log(points); // [100, 40, 25, 10, 5, 2, 1]

// 숫자 배열에서 최대값 취득
console.log(points[0]); // 100
```

#### 객체를 정렬하는 예제는 다음과 같다.
```js
const todos = [
  { id: 4, content: 'JavaScript' },
  { id: 1, content: 'HTML' },
  { id: 2, content: 'CSS' }
];

// 비교 함수. 매개변수 key는 프로퍼티 키다.
function compare(key) {
  // 프로퍼티 값이 문자열인 경우 - 산술 연산으로 비교하면 NaN이 나오므로 비교 연산을 사용한다.
  // 비교 함수는 양수/음수/0을 반환하면 되므로 - 산술 연산 대신 비교 연산을 사용할 수 있다.
  return (a, b) => (a[key] > b[key] ? 1 : (a[key] < b[key] ? -1 : 0));
}

// id를 기준으로 오름차순 정렬
todos.sort(compare('id'));
console.log(todos);
/*
[
  { id: 1, content: 'HTML' },
  { id: 2, content: 'CSS' },
  { id: 4, content: 'JavaScript' }
]
*/

// content를 기준으로 오름차순 정렬
todos.sort(compare('content'));
console.log(todos);
/*
[
  { id: 2, content: 'CSS' },
  { id: 1, content: 'HTML' },
  { id: 4, content: 'JavaScript' }
]
*/
```

<br/>

### Array.prototype.forEach
자신의 내부에서 반복문을 실행하는 고차 함수로서 내부에서 자신이 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다. 
```js
const numbers = [1, 2, 3];
let pows = [];

// forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
numbers.forEach(item => pows.push(item ** 2));
console.log(pows); // [1, 4, 9]
```
#### 콜백 함수는 호출한 배열의 요소값과 인덱스, 호출한 배열인 this을 순차적으로 전달받을 수 있다. 
```js
// forEach 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
[1, 2, 3].forEach((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
});
/*
요소값: 1, 인덱스: 0, this: [1,2,3]
요소값: 2, 인덱스: 1, this: [1,2,3]
요소값: 3, 인덱스: 2, this: [1,2,3]
*/
```
#### 원본 배열을 변경하지는 않지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.
```js
const numbers = [1, 2, 3];

// forEach 메서드는 원본 배열을 변경하지 않지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.
// 콜백 함수의 세 번째 매개변수 arr은 원본 배열 numbers를 가리킨다.
// 따라서 콜백 함수의 세 번째 매개변수 arr을 직접 변경하면 원본 배열 numbers가 변경된다.
numbers.forEach((item, index, arr) => { arr[index] = item ** 2; });
console.log(numbers); // [1, 4, 9]
```
#### 반환값은 언제나 undefined이다.
```js
const result = [1, 2, 3].forEach(console.log);
console.log(result); // undefined
```
#### this로 사용할 객체를 전달할 수 있다.
```js
class Numbers {
  numberArray = [];

  multiply(arr) {
    // 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다.
    arr.forEach(item => this.numberArray.push(item * item));
  }
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
console.log(numbers.numberArray); // [1, 4, 9]
```
#### break나 continue를 사용할 수 없다. 
```js
[1, 2, 3].forEach(item => {
  console.log(item);
  if (item > 1) break; // SyntaxError: Illegal break statement
});

[1, 2, 3].forEach(item => {
  console.log(item);
  if (item > 1) continue;
  // SyntaxError: Illegal continue statement: no surrounding iteration statement
});
```
#### 희소배열의 경우 존재하지 않는 요소는 순회 대상에서 제외된다.
```js
// 희소 배열
const arr = [1, , 3];

// for 문으로 희소 배열을 순회
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); // 1, undefined, 3
}

// forEach 메서드는 희소 배열의 존재하지 않는 요소를 순회 대상에서 제외한다.
arr.forEach(v => console.log(v)); // 1, 3
```

<br/>

### Array.prototype.map
자신이 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 콜백 함수의 반환값으로 구성된 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다. 새로운 배열의 length 프로퍼티 값은 호출한 배열의 값과 반드시 일치한다.
```js
const numbers = [1, 4, 9];

// map 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
// 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.
const roots = numbers.map(item => Math.sqrt(item));

// 위 코드는 다음과 같다.
// const roots = numbers.map(Math.sqrt);

// map 메서드는 새로운 배열을 반환한다
console.log(roots);   // [ 1, 2, 3 ]
// map 메서드는 원본 배열을 변경하지 않는다
console.log(numbers); // [ 1, 4, 9 ]
```
#### 호출한 배열의 요소값과 인덱스, 호출한 배열 자체인 this을 순차적으로 전달받을 수 있다.
```js
// map 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
[1, 2, 3].map((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
  return item;
});
/*
요소값: 1, 인덱스: 0, this: [1,2,3]
요소값: 2, 인덱스: 1, this: [1,2,3]
요소값: 3, 인덱스: 2, this: [1,2,3]
*/
```
#### 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다. 
```js
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  add(arr) {
    // 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다.
    return arr.map(item => this.prefix + item);
  }
}

const prefixer = new Prefixer('-webkit-');
console.log(prefixer.add(['transition', 'user-select']));
// ['-webkit-transition', '-webkit-user-select']
```

<br/>


### Array.prototype.filter
자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다. 
```js
const numbers = [1, 2, 3, 4, 5];

// filter 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
// 그리고 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.
// 다음의 경우 numbers 배열에서 홀수인 요소만을 필터링한다(1은 true로 평가된다).
const odds = numbers.filter(item => item % 2);
console.log(odds); // [1, 3, 5]
```
#### 호출한 배열의 요소값과 인덱스, 호출한 배열 자체인 this을 순차적으로 전달받을 수 있다. 
```js
// filter 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
[1, 2, 3].filter((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
  return item % 2;
});
/*
요소값: 1, 인덱스: 0, this: [1,2,3]
요소값: 2, 인덱스: 1, this: [1,2,3]
요소값: 3, 인덱스: 2, this: [1,2,3]
*/
```
#### 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다.
```js
class Users {
  constructor() {
    this.users = [
      { id: 1, name: 'Lee' },
      { id: 2, name: 'Kim' }
    ];
  }

  // 요소 추출
  findById(id) {
    // id가 일치하는 사용자만 반환한다.
    return this.users.filter(user => user.id === id);
  }

  // 요소 제거
  remove(id) {
    // id가 일치하지 않는 사용자를 제거한다.
    this.users = this.users.filter(user => user.id !== id);
  }
}

const users = new Users();

let user = users.findById(1);
console.log(user); // [{ id: 1, name: 'Lee' }]

// id가 1인 사용자를 제거한다.
users.remove(1);

user = users.findById(1);
console.log(user); // []
```

<br/>

### Array.prototype.reduce
자신을 호출한 배열의 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출한다. 
콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 하나의 결과값을 만들어 반환한다. 원본 배열은 변경되지 않는다. 
첫번째 인수로 콜백 함수, 두 번째 인수로 초기값을 전달받는다. 콜백 함수에는 4개의 인수로 초기값 또는 콜백 함수의 이전 반환값, reduce 메서드를 호출한 배열의 요소값과 인덱스, 호출한 배열 자체인 this가 전달된다. 
```js
// [1, 2, 3, 4]의 모든 요소의 누적을 구한다.
const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);

console.log(sum); // 10
```

#### 초기값을 생략할 수 있다. 
```js
// reduce 메서드의 두 번째 인수, 즉 초기값을 생략했다.
const sum = [1, 2, 3, 4].reduce((acc, cur) => acc + cur);
console.log(sum); // 10
```
#### 초기값을 전달하는 것이 안전하다.
```js
const sum = [].reduce((acc, cur) => acc + cur);
// TypeError: Reduce of empty array with no initial value
```

<br/>

### Array.prototype.some
자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 콜백 함수의 반환값이 단 한번이라도 참이면 true, 모두 거짓이면 false를 반환한다. 빈 배열이면 false를 반환한다. 콜백 함수는 호출한 배열의 요소값과 인덱스, 배열 자체인 this을 순차적으로 전달받을 수 있다.
```js
// 배열의 요소 중에 10보다 큰 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(item => item > 10); // -> true

// 배열의 요소 중에 0보다 작은 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(item => item < 0); // -> false

// 배열의 요소 중에 'banana'가 1개 이상 존재하는지 확인
['apple', 'banana', 'mango'].some(item => item === 'banana'); // -> true

// some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환한다.
[].some(item => item > 3); // -> false
```

<br/>

### Array.prototype.every
자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 콜백 함수의 반환값이 모두 참이면 true, 하나라도 거짓이면 false를 반환한다. 빈 배열이면 true를 반환한다. 콜백 함수는 호출한 배열의 요소값과 인덱스, 배열 자체인 this을 순차적으로 전달받을 수 있다/
```js
// 배열의 모든 요소가 3보다 큰지 확인
[5, 10, 15].every(item => item > 3); // -> true

// 배열의 모든 요소가 10보다 큰지 확인
[5, 10, 15].every(item => item > 10); // -> false

// every 메서드를 호출한 배열이 빈 배열인 경우 언제나 true를 반환한다.
[].every(item => item > 3); // -> true
```

<br/>

### Array.prototype.find
ES6에서 도입된 find 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫번째 요소를 반환한다. 존재하지 않으면 undefined를 반환한다. 콜백 함수는 호출한 배열의 요소값과 인덱스, 배열 자체인 this을 순차적으로 전달받을 수 있다.
```js
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// id가 2인 첫 번째 요소를 반환한다. find 메서드는 배열이 아니라 요소를 반환한다.
users.find(user => user.id === 2); // -> {id: 2, name: 'Kim'}
```
#### filter 메서드는 배열을 반환하고 find 메서드는 요소를 반환한다.
```js
// Array#filter는 배열을 반환한다.
[1, 2, 2, 3].filter(item => item === 2); // -> [2, 2]

// Array#find는 요소를 반환한다.
[1, 2, 2, 3].find(item => item === 2); // -> 2
```

<br/>


### Array.prototype.findIndex
자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫번째 요소의 인덱스를 반환한다. 존재하지 않으면 -1을 반환한다. 콜백 함수는 호출한 배열의 요소값과 인덱스, 배열 자체인 this을 순차적으로 전달받을 수 있다. 
```js
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// id가 2인 요소의 인덱스를 구한다.
users.findIndex(user => user.id === 2); // -> 1

// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(user => user.name === 'Park'); // -> 3

// 위와 같이 프로퍼티 키와 프로퍼티 값으로 요소의 인덱스를 구하는 경우
// 다음과 같이 콜백 함수를 추상화할 수 있다.
function predicate(key, value) {
  // key와 value를 기억하는 클로저를 반환
  return item => item[key] === value;
}

// id가 2인 요소의 인덱스를 구한다.
users.findIndex(predicate('id', 2)); // -> 1

// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(predicate('name', 'Park')); // -> 3
```

<br/>

### Array.prototype.flatMap
ES10에서 도입된 flatMap 메서드는 map 메서드를 통해 생성된 새로운 배열을 평탄화한다. 즉 map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.
```js
const arr = ['hello', 'world'];

// map과 flat을 순차적으로 실행
arr.map(x => x.split('')).flat();
// -> ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']

// flatMap은 map을 통해 생성된 새로운 배열을 평탄화한다.
arr.flatMap(x => x.split(''));
// -> ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
```
