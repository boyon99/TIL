# 제네릭
Generic은 재사용을 목적으로 함수나 클래스의 선언 시점이 아닌, **사용 시점에 타입을 선언**할 수 있는 방법을 제공한다. 함수 이름 우측에 `<T>`를 작성해서 시작하며 `T`는 타입 변수(Type variable)로 사용자가 제공한 타입으로 변환될 식별자이다. 타입 변수는 매개 변수처럼 원하는 이름으로 지정할 수 있다.

```js
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray<number>(1, 2);
toArray<string>('1', '2');
toArray<string | number>(1, '2');
toArray<number>(1, '2'); // Error
```

#### 타입 추론을 활용해, 사용 시점에 타입을 제공하지 않을 수 있다.
```js
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray(1, 2);
toArray('1', '2');
toArray(1, '2'); // Error
```

<br/>

## 제약 조건 (Constraints)
인터페이스나 타입 별칭을 사용하는 제네릭을 작성할 수 있다. 다음 예제는 별도의 제약 조건(Constraints)이 없어서 모든 타입이 허용된다.

```js
interface MyType<T> {
  name: string,
  value: T
}

const dataA: MyType<string> = {
  name: 'Data A',
  value: 'Hello world'
};
const dataD: MyType<number[]> = {
  name: 'Data D',
  value: [1, 2, 3, 4]
};
```

#### extends 키워드를 사용하는 제약 조건을 추가할 수 있다.
```js
T extends U
```
```js
interface MyType<T extends string | number> {
  name: string,
  value: T
}

const dataA: MyType<string> = {
  name: 'Data A',
  value: 'Hello world'
};
const dataD: MyType<number[]> = { // TS2344: Type 'number[]' does not satisfy the constraint 'string | number'.
  name: 'Data D',
  value: [1, 2, 3, 4]
};
```

#### type과 interface 키워드를 사용하는 타입 선언은 다음 예제와 같이 = 기호를 기준으로 ‘식별자’와 ‘타입 구현’으로 구분할 수 있다.
```js
type U = string | number | boolean;

// type 식별자 = 타입 구현
type MyType<T extends U> = string | T;

// interface 식별자 { 타입 구현 }
interface IUser<T extends U> {
  name: string,
  age: T
}

let user : IUser<string> = {
  name: "",
  age: ""
}
```

<br/>

## 클래스와 제네릭
```js
class User<P> {
  public payload: P
  constructor(payload: P) {
    this.payload = payload
  }
  getPayload() {
    return this.payload
  }
}

interface UserA {
  name: string
  age: number
  isValid: boolean
}
interface UserB {
  name: string
  age: number
  emails: string[]
}

const heropy = new User<UserA>({
  name: 'Heropy',
  age: 85,
  isValid: true,
  emails: [] // Error!
})
const neo = new User<UserB>({
  name: 'Neo',
  emails: ['neo@gmail.com']
  // Error! - 'age' 속성이 'UserB' 형식에서 필수입니다.(2345)
})
```

<br/>

## 조건부 타입 (Conditional Types)
제약 조건과 다르게 ‘타입 구현’ 영역에서 사용하는 extends는 삼항 연산자(Conditional ternary operator)를 사용할 수 있으며, 이를 조건부 타입(Conditional Types)이라고 하며 다음과 같은 문법을 가진다.
```js
T extends U ? X : Y
```

```js
type U = string | number | boolean;

// type 식별자 = 타입 구현
type MyType<T> = T extends U ? string : never;

// interface 식별자 { 타입 구현 }
interface IUser<T> {
  name: string,
  age: T extends U ? number : never
}
```
```js
// `T`는 `boolean` 타입으로 제한.
interface IUser<T extends boolean> {
  name: string,
  age: T extends true ? string : number, // `T`의 타입이 `true`인 경우 `string` 반환, 아닌 경우 `number` 반환.
  isString: T
}

const str: IUser<true> = {
  name: 'Neo',
  age: '12', // String
  isString: true
}
const num: IUser<false> = {
  name: 'Lewis',
  age: 12, // Number
  isString: false
}
```

#### 삼항 연산자를 연속해서 사용할 수도 있다
```js
type MyType<T> =
  T extends string ? 'Str' :
  T extends number ? 'Num' :
  T extends boolean ? 'Boo' :
  T extends undefined ? 'Und' :
  T extends null ? 'Nul' :
  'Obj';
```

<br/>

### inter
#### `infer` 키워드를 사용해 타입 변수의 타입 추론(Inference) 여부를 확인할 수 있다.

```js
T extends infer U ? X : Y // U가 추론 가능한 타입이면 참, 아니면 거짓
```

```js
type MyType<T> = T extends infer R ? R : null;
const a: MyType<number> = 123;
```

#### 배열의 아이템 타입을 반환하는 타입

```ts
type ArrayItemType<T> = T extends (infer I)[] ? I : never

// 추론에 성공한 경우,
const array = [1, 2, 3]
type A = ArrayItemType<typeof array>
const a: A = 123 // const a: number

// 추론에 실패한 경우,
type B = ArrayItemType<boolean>
const b: B = 123 // const b: never
```

#### 함수의 두 번째 인수 타입을 반환하는 타입

```ts
type SecondArgumentType<T> = T extends (f: any, s: infer S) => any ? S : never

function hello(a: string, b: number) {}
type A = SecondArgumentType<typeof hello>
const a: A = 123 // const a: number
```

#### 함수의 반환 결과 타입을 반환하는 타입

`ReturnType`은 내장된 유틸리티 타입이다.

```ts
// type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any

function fn(x: string) {
  return x
}
type A = ReturnType<typeof fn>
const a: A = 'Hello' // const a: string
```

#### Promise 인스턴스의 이행된 결과 타입을 반환하는 타입

`Awaited`는 내장된 유틸리티 타입이다.

```ts
// loadImage.ts
function loadImage(src: string): Promise<HTMLImageElement> {
  return new Promise(resolve => {
    const img = document.createElement('img')
    img.src = src
    img.addEventListener('load', () => resolve(img))
  })
}

// main.ts
type PromiseReturnType<T> = T extends Promise<infer R> ? R : never

const promise = loadImage('https://example.com/image.png')
type A = PromiseReturnType<typeof promise>
// type A = Awaited<typeof promise> // 유틸리티 타입! >= @4.5
const a: A = document.querySelector('img')! // 이미지 요소로 단언!
```

#### 타입 변수 캐싱

infer 키워드로 추론하는 타입(`U`)을 캐싱할 수 있다.

```ts
type AtoB<T> = T extends 'A' ? 'B' : never
type BtoC<T> = T extends 'B' ? 'C' : never
type AtoC<T> = AtoB<T> extends infer U // 캐싱!
  ? U extends 'B' ? BtoC<U> : never
  : never

type C = AtoC<'A'> // 'C'
```

infer 키워드를 사용하지 않으면, 두 번 계산해야 힌다.

```ts
type AtoB<T> = T extends 'A' ? 'B' : never
type BtoC<T> = T extends 'B' ? 'C' : never
type AtoC<T> = AtoB<T> extends 'B' 
  ? BtoC<AtoB<T>> 
  : never

type C = AtoC<'A'> // 'C'
```