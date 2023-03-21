# 타입별칭 Type Aliases
`type` 키워드를 사용해 새로운 타입 조합을 만들 수 있다. 하나 이상의 타입을 조합해 별칭을 부여하며, 일반적인 경우 둘 이상의 조합으로 구성하기 위해 유니온을 많이 사용한다.

```ts
// 작명 시 대문자로 시작하는 것을 규칙으로 한다.
type MyType = string;
type YourType = string | number | boolean;

type TUser = {
  name: string,
  age: number,
  isValid: boolean
} | [string, number, boolean];

let userA: TUser = {
  name: 'Neo',
  age: 85,
  isValid: true
};
let userB: TUser = ['Evan', 36, false];
```

#### 함수와 메서드에서 타입별칭을 사용할 수 있다.
```js
type functionType = (a:string) => number;

let func : functionType = function (a){
  return 10
}
```