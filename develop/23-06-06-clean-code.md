## clean code

원하는 로직을 빠르게 찾을 수 있는 코드, 모든 팀원이 이해하기 쉽도록 작성된 코드라고 정의할 수 있다. 많은 개발자들이 클린코드를 위해 명확학 이름, 중복 줄이기, 가독성 높이기 등을 실천하고 있다.

#### 1. 검색이 가능한 이름을 써라.

```js
// bad code
setInterval(hour, 24);
// 클린 코드
const HOUR = 24;
setInterval(hour, HOUR);
```

#### 2. 함수명은 동사로 사용하라.

함수는 단 하나의 역할만 하는 것이 좋다. (단 한가지 액션만 수행하기)

```js
// bad code
function userData() {}
// clean code
function loadUserData() {}
```

#### 3. 인수를 많이 사용하지 마라. 3개 이하로 사용하는 것을 권장한다.

만일 많이 사용하게 된다면 configuration object로 보내도록 하자.

```js
// bad code
function makePayment(price, productId, size, quantity, userId) {}
makePayment(24, 5, "xl", 2, "noco");
// clean code
function makePayment({ price, productId, size, quantity, userId }) {}
makePayemnt({
  price: 35,
  product: 5,
  size: "xl",
  quantity: 2,
  userId: "nico",
});
```

#### 4. boolean 값을 인수로 함수에 보내는 것을 최대한 방지하자.

#### 5. 짧은 변수명이나 축약어를 사용하는 것을 지양하라.

```js
// bad code
allUser.forEach((u, i) => {});
// clean code
allUser.forEach((user, currentNumber) => {});
```
