
## 타입 추론 Inference

명시적으로 타입 선언이 되어있지 않은 경우, 타입스크립트는 타입을 추론해 제공한다.

#### 타입스크립트가 타입을 추론하는 경우는 다음과 같다.
- 초기화된 변수
- 기본값이 설정된 매개변수
- 반환 값이 있는 경우

```ts
// 초기화된 변수 `num`
let num = 12;
num = 'Hello type!'; // TS2322: Type '"Hello type!"' is not assignable to type 'number'.


// 기본값이 설정된 매개 변수 `b`
function add(a: number, b: number = 2): number {
  // 반환 값(`a + b`)이 있는 함수
  return a + b;
}
```
