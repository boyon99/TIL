# 인터페이스 Interface

인터페이스(Interface)는 타입스크립트 여러 객체를 정의하는 일종의 규칙이며 구조로 다음과 같이 `interface` 키워드와 함께 사용한다. 타입별칭과는 다르게 중복선언이 가능하며 `extends` 키워드를 사용하여 상속할 수 있다. `사용자 정의 자료형`이라고 할 수 있다.

```ts
interface IUser {
  name: string;
  age: number;
  isAdult: boolean;
}

let user1: IUser = {
  name: "Neo",
  age: 123,
  isAdult: true,
};

// Error - TS2741: Property 'isAdult' is missing in type '{ name: string; age: number; }' but required in type 'IUser'.
let user2: IUser = {
  name: "Evan",
  age: 456,
};
```

#### `:`(colon) `,`(comma) 혹은 기호를 사용하지 않을 수 있다.

```ts
interface IUser {
  name: string;
  age: number;
}
// Or
interface IUser {
  name: string;
  age: number;
}
// Or
interface IUser {
  name: string;
  age: number;
}
```

#### 속성에 `?`를 사용하면 선택적 속성으로 정의할 수 있다.

```ts
interface IUser {
  name: string;
  age: number;
  isAdult?: boolean; // Optional property
}

// `isAdult`를 초기화하지 않아도 에러가 발생하지 않는다.
let user: IUser = {
  name: "Neo",
  age: 123,
};
```

<br/>

## 읽기 전용 속성 Readonly properties

`readonly` 키워드를 사용하면 초기화된 값을 유지해야 하는 읽기 전용 속성을 정의할 수 있다.

```ts
interface IUser {
  readonly name: string;
  age: number;
}

// 초기화
let user: IUser = {
  name: "Neo",
  age: 36,
};

user.age = 85; // Ok
user.name = "Evan"; // Error - TS2540: Cannot assign to 'name' because it is a read-only property.
```

<br/>

## 함수 타입

함수 타입을 인터페이스로 정의하는 경우, 호출 시그니처(Call signature)를 사용한다. 호출 시그니처는 다음과 같이 함수의 매개 변수(parameter)와 반환 타입을 지정한다.

```ts
interface IName {
  (PARAMETER: PARAM_TYPE): RETURN_TYPE; // Call signature
}
```

```ts
interface User {
  name: string;
}
interface GetUser {
  (name: string): User;
}

// 매개 변수 이름이 인터페이스와 일치할 필요가 없다.
const getUser: GetUser = (name) => {
  // ...
  return { name };
};
getUser("Heropy");
```

<br/>

## 클래스 타입

인터페이스로 클래스를 정의하는 경우, `implements` 키워드를 사용한다.

```ts
interface IUser {
  name: string;
  getName(): string;
}

class User implements IUser {
  constructor(public name: string) {}
  getName() {
    return this.name;
  }
}

const neo = new User("Neo");
neo.getName(); // Neo
```

#### 클래스의 경우 구성 시그니처(Construct signature)를 제공한다. 구성 시그니처는 위에서 살펴본 호출 시그니처와 비슷하지만, new 키워드를 사용한다.

```ts
interface IName {
  new (PARAMETER: PARAM_TYPE): RETURN_TYPE; // Construct signature
}
```

```ts
interface ICat {
  name: string;
}
interface ICatConstructor {
  new (name: string): ICat;
}

class Cat implements ICat {
  constructor(public name: string) {}
}

function makeKitten(c: ICatConstructor, n: string) {
  return new c(n); // ok
}
const kitten = makeKitten(Cat, "Lucy");
console.log(kitten);
```

<br/>

## 인덱싱 가능 타입 Indexable types

인덱스 시그니처는 다음 구조와 같이, 인덱싱에 사용할 인덱서(Indexer)의 이름과 타입 그리고 인덱싱 결과의 반환 값을 지정한다. 인덱서의 타입은 string과 number만 지정할 수 있다.

```ts
interface INAME {
  [INDEXER_NAME: INDEXER_TYPE]: RETURN_TYPE; // Index signature
}
```

```ts
interface IItem {
  [itemIndex: number]: string; // Index signature
}
let item: IItem = ["a", "b", "c"]; // Indexable type
console.log(item[0]); // 'a' is string.
console.log(item[1]); // 'b' is string.
console.log(item["0"]); // Error - TS7015: Element implicitly has an 'any' type because index expression is not of type 'number'.
```

#### 인덱싱 결과의 반환 타입으로 유니온을 사용할 수 있다.

```ts
interface IItem {
  [itemIndex: number]: string | boolean | number[];
}
let item: IItem = ["Hello", false, [1, 2, 3]];
console.log(item[0]); // Hello
console.log(item[1]); // false
console.log(item[2]); // [1, 2, 3]
```

#### 문자로 인덱싱할 때 다음과 같이 사용할 수 있다.

```ts
interface IUser {
  [userProp: string]: string | boolean;
}
let user: IUser = {
  name: "Neo",
  email: "thesecon@gmail.com",
  isValid: true,
  0: false,
};
console.log(user["name"]); // 'Neo' is string.
console.log(user["email"]); // 'thesecon@gmail.com' is string.
console.log(user["isValid"]); // true is boolean.
console.log(user[0]); // false is boolean
console.log(user[1]); // undefined
console.log(user["0"]); // false is boolean
```

#### 인덱싱 가능 타입에서 `keyof`를 사용하면 속성 이름을 타입으로 사용할 수 있다. 인덱싱 가능 타입의 속성 이름들이 유니온 타입으로 적용된다.

```ts
interface ICountries {
  KR: "대한민국";
  US: "미국";
  CP: "중국";
}
let country: keyof ICountries; // 'KR' | 'US' | 'CP'
country = "KR"; // ok
country = "RU"; // Error - TS2322: Type '"RU"' is not assignable to type '"KR" | "US" | "CP"'.
```

#### `keyof`를 통한 인덱싱으로 타입의 개별 값에도 접근할 수 있다.

```ts
interface ICountries {
  KR: "대한민국";
  US: "미국";
  CP: "중국";
}
let country: ICountries[keyof ICountries]; // ICountries['KR' | 'US' | 'CP']
country = "대한민국";
country = "러시아"; // Error - TS2322: Type '"러시아"' is not assignable to type '"대한민국" | "미국" | "중국"'.
```

<br/>

## 인터페이스 확장

`extends` 키워드를 활용해 상속할 수 있다.

```ts
interface Animal {
  name: string;
}
interface Cat extends Animal {
  meow(): string;
}

class Cat implements Cat {
  constructor(public name: string) {}
  meow() {
    return "MEOW~";
  }
}
const cat = new Cat("Luxy");
```

#### 같은 이름의 인터페이스를 여러 개 만들 수 있다. 기존에 만들어진 인터페이스에 내용을 추가하는 경우 유용하다.

```js
interface IFullName {
  firstName: string;
  lastName: string;
}
interface IFullName {
  middleName: string;
}

const fullName: IFullName = {
  firstName: "Tomas",
  middleName: "Sean",
  lastName: "Connery",
};
```
