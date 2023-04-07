# Optional
`?` 키워드를 사용하는 여러 선택적(Optional) 개념

<br/>

### 1. 매개 변수(Parameters)
타입을 선언할 때 선택적 매개 변수(Optional Parameter)를 지정할 수 있다.
```js
function add(x: number, y?: number): number {
  return x + (y || 0);
}
const sum = add(2);
console.log(sum);
```

#### ? 키워드 사용은 | undefined를 추가하는 것과 같다.
```js
function add(x: number, y: number | undefined): number {
  return x + (y || 0);
}
const sum = add(2, undefined);
console.log(sum);
```

<br/>

### 2. 속성(Properties)과 메소드(Methods) 타입 선언
```js
interface IUser {
  name: string,
  age: number,
  isAdult?: boolean
}

let user2: IUser = {
  name: 'Evan',
  age: 456
};
```
#### Type이나 Class에서도 사용할 수 있다.

```js
interface IUser {
  isAdult?: boolean,
  validate?(): boolean
}
type TUser = {
  isAdult?: boolean,
  validate?(): boolean
}
abstract class CUser {
  abstract isAdult?: boolean;
  abstract validate?(): boolean;
}
```

<br/>

### 3. 페이닝 (Chaining)
```js
// Error - TS2532: Object is possibly 'undefined'.
function toString(str: string | undefined) {
  return str.toString();
}

// Type Assertion
function toString(str: string | undefined) {
  return (str as string).toString();
}

// Optional Chaining
function toString(str: string | undefined) {
  return str?.toString();
}
```

#### `&&` 연산자를 사용해 Nullish 체크(null이나 undefined를 확인)할 때 유용하다.
```js
// Before
if (foo && foo.bar && foo.bar.baz) {}

// After-ish
if (foo?.bar?.baz) {}
```

<br/>

### 4. Nullish 병합 연산자
```js
const foo = null ?? 'Hello nullish.';
console.log(foo); // Hello nullish.

const bar = false ?? true;
console.log(bar); // false

const baz = 0 ?? 12;
console.log(baz); // 0
```
