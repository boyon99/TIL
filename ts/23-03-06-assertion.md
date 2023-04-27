
## 타입 단언 Assertions

타입스크립트가 타입 추론을 통해 판단할 수 있는 타입의 범주를 넘는 경우, 더 이상 추론하지 않도록 지시할 수 있다. 이를 ‘타입 단언’이라고 하며, 이는 프로그래머가 타입스크립트보다 타입에 대해 더 잘 이해하고 있는 상황을 의미한다.

```ts
// Error - TS2533: Object is possibly 'null' or 'undefined'.
function fnA(x: number | null | undefined) {
  return x.toFixed(2); // 타입이 null이나 undefined일 수 있으므로 오류 발생
}
```

### Non-null 단언 연산자

`!`를 사용하는 Non-null 단언 연산자(Non-null assertion operator)를 통해 피연산자가 Nullish(`null`이나 `undefined`) 값이 아님을 단언할 수 있는데, 변수나 속성에서 간단하게 사용할 수 있기 때문에 유용하다.

```js
// Non-null assertion operator으로 오류를 해결하는 방법
function fnA(x: number | null | undefined) : number{
  return x!; // 타입이 null이나 undefined일 수 있으므로 오류 발생
}
```

### as 키워드 단언
`as` 키워드로 변수의 특정한 타입으로 단언한다.
```ts
// Type assertion으로 오류를 해결하는 방법
function someFunc(val: string | number, isNumber: boolean) {
  if (isNumber) {
    // true인 경우 val의 타입은 number이다.
    (val as number).toFixed(2); // 숫자임을 확신할 때 타입 단언을 할 수 있다. 
  }
}
```
### 타입 가드
데이터가 참인 경우에만 동작하도록 작성한다.
```ts
// if statement으로 오류를 해결하는 방법
function fnD(x: number | null | undefined) {
  if (x) {
    return x.toFixed(2);
  }
}
```
