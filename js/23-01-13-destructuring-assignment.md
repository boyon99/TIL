# 디스트럭처링 할당
구조화된 배열과 같은 이터러블 또는 객체를 destructuring하여 1개 이상의 변수에 개별적으로 할당하는 것을 말한다. 배열과 같은 이터러블 또는 객체 리터럴에서 필요한 값만 추출하여 사용할 때 유용하다.

<br/>

## 배열 디스트럭처링 할당
배열 디스트럭처링 할당의 대상은 이터러블이어야 하며 할당 기준은 배열의 인덱스이다. 
```js
const arr = [1, 2, 3];

// ES6 배열 디스트럭처링 할당
// 변수 one, two, three를 선언하고 배열 arr을 디스트럭처링하여 할당한다.
// 이때 할당 기준은 배열의 인덱스다.
const [one, two, three] = arr;

console.log(one, two, three); // 1 2 3
```

#### 할당 연산자 왼쪽에 값을 할당받을 변수를 배열 리터럴 형태로 선언한다. 
```js
const [x, y] = [1, 2];
```
#### 우변에 이터러블을 할당하지 않으면 에러가 발생한다.
```js
const [x, y]; // SyntaxError: Missing initializer in destructuring declaration

const [a, b] = {}; // TypeError: {} is not iterable
```
#### 선언과 할당을 분리할 수 있으나 const 키워드로 변수 선언이 불가능하다.
```js
let x, y;
[x, y] = [1, 2];

const x, y; // SyntaxError: Missing initializer in const declaration
[x, y] = [1, 2];
```
#### 변수의 개수와 이터러블의 요소 개수가 반드시 일치할 필요는 없다.
```js
const [a, b] = [1, 2];
console.log(a, b); // 1 2

const [c, d] = [1];
console.log(c, d); // 1 undefined

const [e, f] = [1, 2, 3];
console.log(e, f); // 1 2

const [g, , h] = [1, 2, 3];
console.log(g, h); // 1 3
```
#### 변수에 기본값을 설정할 수 있으나 할당된 값이 우선된다.
```js
// 기본값
const [a, b, c = 3] = [1, 2];
console.log(a, b, c); // 1 2 3

// 기본값보다 할당된 값이 우선한다.
const [e, f = 10, g = 3] = [1, 2];
console.log(e, f, g); // 1 2 3
```
#### Rest 파라미터와 유사하게 Rest 요소 `...`를 사용할 수 있다. 반드시 마지막에 위치해야 한다.
```js
// Rest 요소
const [x, ...y] = [1, 2, 3];
console.log(x, y); // 1 [ 2, 3 ]
```

<br/>

## 객체 디스트럭처링 할당
객체 디스트럭처링 할당은 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다. 할당의 대상은 객체여야 하며 할당 기준은 프로퍼티 키이다. 즉, 선언된 변수 이름과 프로퍼티 키가 일치하면 할당된다.
```js
const user = { firstName: 'Ungmo', lastName: 'Lee' };

// ES6 객체 디스트럭처링 할당
// 변수 lastName, firstName을 선언하고 user 객체를 디스트럭처링하여 할당한다.
// 이때 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미가 없다.
const { lastName, firstName } = user;

console.log(firstName, lastName); // Ungmo Lee
```

#### 할당받을 변수를 객체 리터럴 형태로 선언한다.
```js
const { lastName, firstName } = { firstName: 'Ungmo', lastName: 'Lee' };
```
#### 우변에 객체 또는 객체로 평가될 수 있는 평가식을 할당해야 한다.
```js
const { lastName, firstName };
// SyntaxError: Missing initializer in destructuring declaration

const { lastName, firstName } = null;
// TypeError: Cannot destructure property 'lastName' of 'null' as it is null.
```
#### 프로퍼티 축약 표현을 통해 변수를 선언한다.
```js
const { lastName, firstName } = user;
// 위와 아래는 동치다.
const { lastName: lastName, firstName: firstName } = user;
```
#### 프로퍼티 키와 다른 변수 이름으로 할당받으려면 다음과 같이 선언한다.
```js
const user = { firstName: 'Ungmo', lastName: 'Lee' };

// 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다.
// 프로퍼티 키가 lastName인 프로퍼티 값을 ln에 할당하고,
// 프로퍼티 키가 firstName인 프로퍼티 값을 fn에 할당한다.
const { lastName: ln, firstName: fn } = user;

console.log(fn, ln); // Ungmo Lee
```
#### 변수에 기본값을 설정할 수 있다.
```js
const { firstName = 'Ungmo', lastName } = { lastName: 'Lee' };
console.log(firstName, lastName); // Ungmo Lee

const { firstName: fn = 'Ungmo', lastName: ln } = { lastName: 'Lee' };
console.log(fn, ln); // Ungmo Lee
```
#### 중첩 객체인 경우 다음과 같이 사용한다.
```js
const user = {
  name: 'Lee',
  address: {
    zipCode: '03068',
    city: 'Seoul'
  }
};

// address 프로퍼티 키로 객체를 추출하고 이 객체의 city 프로퍼티 키로 값을 추출한다.
const { address: { city } } = user;
console.log(city); // 'Seoul'
```
#### Rest 프로퍼티 `...`를 사용할 수 있다. 마지막에 위치해야 한다.
```js
// Rest 프로퍼티
const { x, ...rest } = { x: 1, y: 2, z: 3 };
console.log(x, rest); // 1 { y: 2, z: 3 }
```

<br/>

### 배열 디스트럭처링 할당과 객체 디스트럭처링 할당의 혼용
배열의 요소가 객체인 경우 혼용할 수 있다.
```js
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: false },
  { id: 3, content: 'JS', completed: false }
];

// todos 배열의 두 번째 요소인 객체로부터 id 프로퍼티만 추출한다.
const [, { id }] = todos;
console.log(id); // 2
```
