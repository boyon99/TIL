# TS 유틸리티 타입

타입스크립트에서 제공하는 여러 전역 유틸리티 타입이 있다.

> 타입 변수 `T`는 타입(Type), `U`는 또 다른 타입, `K`는 속성(key)을 의미하는 약어이다. 이해하기 쉽게 타입 변수를 `T`는 `TYPE` 또는 `TYPE1`, `U`는 `TYPE2`, `K`는 `KEY`로 명시했다.

| 유틸리티 이름           | 설명 (대표 타입)                                                                       | 타입 변수        |
| ----------------------- | -------------------------------------------------------------------------------------- | ---------------- |
| `Partial`               | `TYPE`의 모든 속성을 선택적으로 변경한 새로운 타입 반환 (인터페이스)                   | `<TYPE>`         |
| `Required`              | `TYPE`의 모든 속성을 필수로 변경한 새로운 타입 반환 (인터페이스)                       | `<TYPE>`         |
| `Readonly`              | `TYPE`의 모든 속성을 읽기 전용으로 변경한 새로운 타입 반환 (인터페이스)                | `<TYPE>`         |
| `ReadonlyArray`         |                                                                                        | `<TYPE>`         |
| `Record`                | `KEY`를 속성으로, `TYPE`를 그 속성값의 타입으로 지정하는 새로운 타입 반환 (인터페이스) | `<KEY, TYPE>`    |
| `Pick`                  | `TYPE`에서 `KEY`로 속성을 선택한 새로운 타입 반환 (인터페이스)                         | `<TYPE, KEY>`    |
| `Omit`                  | `TYPE`에서 `KEY`로 속성을 생략하고 나머지를 선택한 새로운 타입 반환 (인터페이스)       | `<TYPE, KEY>`    |
| `Exclude`               | `TYPE1`에서 `TYPE2`를 제외한 새로운 타입 반환 (유니언)                                 | `<TYPE1, TYPE2>` |
| `Extract`               | `TYPE1`에서 `TYPE2`를 추출한 새로운 타입 반환 (유니언)                                 | `<TYPE1, TYPE2>` |
| `NonNullable`           | `TYPE`에서 `null`과 `undefined`를 제외한 새로운 타입 반환 (유니언)                     | `<TYPE>`         |
| `Parameters`            | `TYPE`의 매개변수 타입을 새로운 튜플 타입으로 반환 (함수, 튜플)                        | `<TYPE>`         |
| `ConstructorParameters` | `TYPE`의 매개변수 타입을 새로운 튜플 타입으로 반환 (클래스, 튜플)                      | `<TYPE>`         |
| `ReturnType`            | `TYPE`의 반환 타입을 새로운 타입으로 반환 (함수)                                       | `<TYPE>`         |
| `InstanceType`          | `TYPE`의 인스턴스 타입을 반환 (클래스)                                                 | `<TYPE>`         |
| `ThisParameterType`     | `TYPE`의 명시적 `this` 매개변수 타입을 새로운 타입으로 반환 (함수)                     | `<TYPE>`         |
| `OmitThisParameter`     | `TYPE`의 명시적 `this` 매개변수를 제거한 새로운 타입을 반환 (함수)                     | `<TYPE>`         |
| `ThisType`              | `TYPE`의 `this` 컨텍스트(Context)를 명시, 별도 반환 없음! (인터페이스)                 | `<TYPE>`         |

### Partial

`TYPE`의 모든 속성을 선택적(`?`)으로 변경한 새로운 타입을 반환한다.

```typescript
Partial<TYPE>;
```

```typescript
interface User {
  name: string
  age: number
}

const userA: User = { Error!
  name: 'A'
}
const userB: Partial<User> = {
  name: 'B'
}
```

다음과 같이 이해할 수 있다.

```typescript
interface NewType {
  name?: string;
  age?: number;
}
```

### Required

`TYPE`의 모든 속성을 필수로 변경한 새로운 타입을 반환한다.

```typescript
Required<TYPE>;
```

```typescript
interface User {
  name?: string
  age?: number
}

const userA: User = {
  name: 'A'
}
const userB: Required<User> = { Error!
  name: 'B'
}
```

다음과 같이 이해할 수 있다.

```typescript
interface User {
  name: string;
  age: number;
}
```

### Readonly

`TYPE`의 모든 속성을 읽기 전용(`readonly`)으로 변경한 새로운 타입을 반환한다.

```typescript
Readonly<TYPE>;
```

```typescript
interface User {
  name: string;
  age: number;
}

const userA: User = {
  name: "A",
  age: 12,
};
userA.name = "AA";

const userB: Readonly<User> = {
  name: "B",
  age: 13,
};
userB.name = "BB"; // Error!
```

다음과 같이 이해할 수 있습니다.

```typescript
interface NewType {
  readonly name: string;
  readonly age: number;
}
```

### Record

`KEY`를 속성(Key)으로, `TYPE`를 그 속성값의 타입(Type)으로 지정하는 새로운 타입을 반환한다.

```typescript
Record<KEY, TYPE>;
```

```typescript
type Names = "neo" | "lewis";

const developers: Record<Names, number> = {
  neo: 12,
  lewis: 13,
};
```

다음과 같이 이해할 수 있다.

```typescript
interface NewType {
  neo: number;
  lewis: number;
}
```

### Pick

`TYPE`에서 `KEY`로 속성을 선택한 새로운 타입을 반환한다. `TYPE`은 속성을 가지는 인터페이스나 객체 타입이어야 한다.

```typescript
Pick<TYPE, KEY>;
```

```typescript
interface User {
  name: string;
  age: number;
  email: string;
  isValid: boolean;
}
type Keys = "name" | "email";

const user: Pick<User, Keys> = {
  name: "Neo",
  email: "thesecon@gmail.com",
  age: 22, // Error!
};
```

다음과 같이 이해할 수 있다.

```typescript
interface NewType {
  name: string;
  email: string;
}
```

### Omit

`Pick`과 반대로, `TYPE`에서 `KEY`로 속성을 생략하고 나머지를 선택한 새로운 타입을 반환한다. `TYPE`은 속성을 가지는 인터페이스나 객체 타입이어야 한다.

```typescript
Omit<TYPE, KEY>;
```

```typescript
interface User {
  name: string;
  age: number;
  email: string;
  isValid: boolean;
}
type Keys = "name" | "email";

const user: Omit<User, Keys> = {
  age: 22,
  isValid: true,
  name: "Neo", // Error!
};
```

다음과 같이 이해할 수 있다.

```typescript
interface NewType {
  // name: string
  age: number;
  // email: string
  isValid: boolean;
}
```

### Exclude

유니언 `TYPE1`에서 유니언 `TYPE2`를 제외한 새로운 타입을 반환한다.

```typescript
Exclude<TYPE1, TYPE2>;
```

```typescript
type T = string | number;

const a: Exclude<T, number> = "Only string";
const b: Exclude<T, number> = 1234; // Error!
```

### Extract

유니언 `TYPE1`에서 유니언 `TYPE2`를 추출한 새로운 타입을 반환한다.

```typescript
Extract<TYPE1, TYPE2>;
```

```typescript
type T = string | number;
type U = number | boolean;

const a: Extract<T, U> = 123;
const b: Extract<T, U> = "Only number"; // Error!
```

### NonNullable

유니언 `TYPE`에서 `null`과 `undefined`를 제외한 새로운 타입을 반환한다.

```typescript
NonNullable<TYPE>;
```

```typescript
type T = string | number | undefined;

const a: T = undefined;
const b: NonNullable<T> = null; // Error!
```

### Parameters

함수 `TYPE`의 매개변수 타입을 새로운 튜플(Tuple) 타입으로 반환한다.

```typescript
Parameters<TYPE>;
```

```typescript
function fn(a: string | number, b: boolean) {
  return `[${a}, ${b}]`;
}

const a: Parameters<typeof fn> = ["Hello", 123]; // Error! - Type 'number' is not assignable to type 'boolean'.
```

위 예제의 `Parameters<typeof fn>`은 다음과 같이 이해할 수 있다.

```typescript
[string | number, boolean];
```

### ConstructorParameters

클래스 `TYPE`의 매개변수 타입을 새로운 튜플 타입으로 반환한다.

```typescript
ConstructorParameters<TYPE>;
```

```typescript
class User {
  constructor(public name: string, private age: number) {}
}

const neo = new User("Neo", 12);
const a: ConstructorParameters<typeof User> = ["Neo", 12];
const b: ConstructorParameters<typeof User> = ["Lewis"]; // Error!
```

다음과 같이 이해할 수 있다.

```typescript
[string, number];
```

### ReturnType

함수 `TYPE`의 반환(Return) 타입을 새로운 타입으로 반환한다.

```typescript
ReturnType<TYPE>;
```

```typescript
function fn(str: string) {
  return str;
}

const a: ReturnType<typeof fn> = "Only string";
const b: ReturnType<typeof fn> = 1234; // Error! - TS2322: Type '123' is not assignable to type 'string'.
```

### InstanceType

클래스 `TYPE`의 인스턴스 타입을 반환한다.

```typescript
InstanceType<TYPE>;
```

```typescript
class User {
  constructor(public name: string) {}
}

const neo: InstanceType<typeof User> = new User("Neo");
```

### ThisParameterType

함수 `TYPE`의 명시적 `this` 매개변수 타입을 새로운 타입으로 반환한다. 함수 `TYPE`에 명시적 `this` 매개변수가 없는 경우 알 수 없는 타입(Unknown)을 반환한다.

```typescript
ThisParameterType<TYPE>;
```

```typescript
function toHex(this: number) {
  return this.toString(16); // 16진수 문자로 변환!
}
function numberToString(n: ThisParameterType<typeof toHex>) {
  return toHex.call(n);
}

console.log(numberToString(9)); // '9'
console.log(numberToString(10)); // 'a'
console.log(numberToString(11)); // 'b'
console.log(numberToString(12)); // 'c'
```

위 예제에서 함수 `toHex`의 명시적 `this` 타입은 `Number`이고,  
그 타입을 참고해서 함수 `numberToString`의 매개변수 `n`의 타입을 선언한다. 따라서 `toHex`에 다른 타입의 `this`가 바인딩 되는 것을 방지할 수 있다.

### OmitThisParameter

함수 `TYPE`의 명시적 `this` 매개변수를 제거한 새로운 타입을 반환한다.

```typescript
OmitThisParameter<TYPE>;
```

```typescript
function getAge(this: typeof cat) {
  return this.age;
}

// 기존 데이터
const cat = {
  age: 12, // Number
};
getAge.call(cat); // 12

// 새로운 데이터
const dog = {
  age: "13", // String
};
getAge.call(dog); // Error!
```

위 예제에서 데이터 `cat`을 기준으로 설계한 함수 `getAge`는 일부 다른 타입을 가지는 새로운 데이터 `dog`를 `this`로 사용할 수 없다. 하지만 `OmitThisParameter`를 통해 명시적 `this`를 제거한 새로운 타입의 함수를 만들 수 있기 때문에, `getAge`를 직접 수정하지 않고 데이터 `dog`를 사용할 수 있다.

```typescript
const getAgeForDog: OmitThisParameter<typeof getAge> = getAge;
getAgeForDog.call(dog); // '13'
```

> `this.age`에는 이제 어떤 값도 들어갈 수 있음을 주의

### ThisType

`TYPE`의 `this` 컨텍스트(Context)를 명시하고 별도의 타입을 반환하지 않는다.

```typescript
ThisType<TYPE>;
```

```typescript
interface User {
  name: string;
  getName: () => string;
}

function makeNeo(methods: ThisType<User>) {
  return { name: "Neo", ...methods } as IUser;
}
const neo = makeNeo({
  getName() {
    return this.name;
  },
});

neo.getName(); // Neo
```

함수 `makeNeo`의 인수로 사용되는 메소드 `getName`은 내부에서 `this.name`을 사용하고 있기 때문에 `ThisType`을 통해 명시적으로 `this` 컨텍스트를 설정해 준다. 단, `ThisType`은 별도의 타입을 반환하지 않기 때문에 `makeNeo` 반환 값(`{ name: 'Neo', ...methods }`)에 대한 타입이 정상적으로 추론(Inference)되지 않는다. 따라서 `as User`와 같이 따로 타입을 단언(Assertions)해야 `neo.getName`을 정상적으로 호출할 수 있다.
