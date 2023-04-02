## 불변성과 가변성

**불변성**(Immutability)은 생성된 데이터가 메모리에서 변경되지 않고, **가변성**(Mutability)은 생성된 데이터가 메모리에서 변경될 수 있음을 의미한다. 자바스크립트 원시형(string, number, boolean, null, undefined, symbol 등)은 불변성을 가지고 있고, 참조형(array, object, function)은 가변성을 가지고 있다.

#### 원시형

```js
let a = 1;
let b = a;
b = 2;
console.log(b); // 2
console.log(a); // 1
```

#### 참조형

```js
// 객체
let a = { x: 1 };
let b = a;
b.x = 2;
console.log(b.x); // 2
console.log(a.x); // 2

// 배열
let a = [1, 2, 3];
let b = a;
b[0] = 4;
console.log(b); // [4, 2, 3]
console.log(a); // [4, 2, 3]

// 함수
let a = () => 1;
let b = a;
b.x = 2;
console.log(b.x); // 2
console.log(a.x); // 2
```
