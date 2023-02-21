# promise
자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다. 하지만 전통적인 콜백 패턴은 명백한 한계가 존재하므로 ES6에서는 비동기 처리를 위한 또 다른 패턴으로 프로미스를 도입하였다. 즉 프로미스는 비동기 콜백 함수이다.

```js
// 콜백 함수를 사용한 전통적인 콜백 패턴
function call2(){
  console.log("3: call2") // 3번 실행
}

function call(){
  console.log("2: call") // 2번 실행
  call2()
}

console.log("1: outer") // 1번 실행
call()
```

<br/>

## 비동기 처리를 위한 콜백 패턴의 단점
- 콜백 헬을 발생시킨다.

  비동기 함수란 함수 내부에 비동기로 동작하는 코드를 포함한 함수를 말한다. 비동기 함수를 호춯하면 함수 내부에 비동기로 동작하는 코드가 완료하지 않아도 즉시 종료된다. 따라서 비동기로 작동하는 코드는 비동기 함수가 종료된 이후에 완료된다. 이는 원하는 대로 동작하지 않는 현상을 발생시킨다. 따라서 원하는 대로 하기 위해서 콜백 함수 호출이 중첩되도록 구현하면 복잡도가 높아지는 콜백 헬이 발생한다.

- 비동기 처리 결과를 외부에 반환하거나 상위 스코프 변수에 할당할 수도 없다.
- 에러 처리가 곤란하다는 것이다.

<br/>

## 프로미스의 생성
프로미스 생성자 함수를 new 연산자와 함께 호출하여 생성할 수 있으며 비동기 처리를 수행할 콜백 함수를 인수로 전달받는데 이 콜백 함수는 resolve와 reject 함수를 인수로 전달받는다.

#### 프로미스는 비동기 처리가 어떻게 진행되고 있는지 나타내는 상태 정보를 갖는다.
- pendung : 비동기 처리가 아직 수행되지 않은 상태
- fulfilled : 비동기 처리가 수행된 상태(성공)으로 resolve 함수를 호출한다.
- rejected : 비동기 처리가 수행된 상태(실패)로 reject 함수를 호출한다.

```js
// 프로미스 생성
const promise = new Promise((resolve, reject) => {
  // Promise 함수의 콜백 함수 내부에서 비동기 처리를 수행한다.
  if (/* 비동기 처리 성공 */) {
    resolve('result');
  } else { /* 비동기 처리 실패 */
    reject('failure reason');
  }
});
```

#### GET 요청을 위한 비동기 함수
```js
const promiseGet = url => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.send();

    xhr.onload = () => {
      if (xhr.status === 200) {
        // 성공적으로 응답을 전달받으면 resolve 함수를 호출한다.
        resolve(JSON.parse(xhr.response));
      } else {
        // 에러 처리를 위해 reject 함수를 호출한다.
        reject(new Error(xhr.status));
      }
    };
  });
};

// promiseGet 함수는 프로미스를 반환한다.
promiseGet('https://jsonplaceholder.typicode.com/posts/1');
```

<br/>

### 프로미스의 후속 처리 메서드
프로미스의 비동기 처리 상태가 변화하면 이에 따른 후속 처리를 해야 한다. 이를 위해 프로미스는 후속 메서드 `then` `catch` `finally`를 제공한다. 그리고 프로미스의 비동기 처리 상태가 변화하면 후속 처리 메서드에 인수로 전달한 콜백 함수가 선택적으로 호출된다.


#### Promise.then
2개의 콜백 함수를 인수로 전달받는다.
- 첫 번째 콜백 함수는 프로미스가 fulfilled 상태가 되면 호출한다.
- 두 번째 콜백 함수는 프로미스가 rejected 상태가 되면 호출한다.

```js
// fulfilled
new Promise(resolve => resolve('fulfilled'))
  .then(v => console.log(v), e => console.error(e)); // fulfilled

// rejected
new Promise((_, reject) => reject(new Error('rejected')))
  .then(v => console.log(v), e => console.error(e)); // Error: rejected
```

#### Promise.catch
프로미스가 rejected인 상태에서만 호출된다.
```js
// rejected
new Promise((_, reject) => reject(new Error('rejected')))
  .catch(e => console.log(e)); // Error: rejected
```

#### Promise.finally
finally 메서드는 한 개의 콜백 함수를 인수로 전달받으며 성공 여부와 상관없이 무조건 한 번 호출된다.

```js
new Promise(() => {})
  .finally(() => console.log('finally')); // finally
```

프로미스를 구현한 비동기 함수 get를 사용해 후속 처리를 구현해보자
```js
const promiseGet = url => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.send();

    xhr.onload = () => {
      if (xhr.status === 200) {
        // 성공적으로 응답을 전달받으면 resolve 함수를 호출한다.
        resolve(JSON.parse(xhr.response));
      } else {
        // 에러 처리를 위해 reject 함수를 호출한다.
        reject(new Error(xhr.status));
      }
    };
  });
};

// promiseGet 함수는 프로미스를 반환한다.
promiseGet('https://jsonplaceholder.typicode.com/posts/1')
  .then(res => console.log(res))
  .catch(err => console.error(err))
  .finally(() => console.log('Bye!'));
```

<br/>

### 프로미스의 에러 처리
비동기 처리에서 발생한 에러는 `catch`를 사용하거나 `then` 메서드의 두 번째 콜백 함수를 통해 처리할 수 있다. `catch`를 사용하는 것이 바람직하다.
```js
const wrongUrl = 'https://jsonplaceholder.typicode.com/XXX/1';

// 부적절한 URL이 지정되었기 때문에 에러가 발생한다.
promiseGet(wrongUrl)
  .then(res => console.log(res))
  .catch(err => console.error(err)); // Error: 404
```

<br/>

### 프로미스 체이닝
`then` `catch` `finally` 후속 처리 메서드는 언제나 프로미스를 반환하므로 연속적으로 호출할 수 있다. 이를 프로미스 체이닝이라고 한다. 

<br/>

### 프로미스의 정적 메서드
프로미스는 5가지의 정적 메서드를 제공한다.

#### Promise.resolve/reject
```js
// 배열을 resolve하는 프로미스를 생성
const resolvedPromise = Promise.resolve([1, 2, 3]); // new Promise(resolve => resolve([1, 2, 3]));와 동일하다.
resolvedPromise.then(console.log); // [1, 2, 3]
```
```js
// 에러 객체를 reject하는 프로미스를 생성
const rejectedPromise = Promise.reject(new Error('Error!')); // new Promise((_, reject) => reject(new Error('Error!')));와 동일하다.
rejectedPromise.catch(console.log); // Error: Error!
```

#### Promise.all
여러 개의 비동기 처리를 모두 병렬로 처리할 때 사용된다. 인수로 전달받은 배열의 모든 프로미스가 모두 fullfilled 상태가 되면 종료한다. 하나라도 rejected 상태가 되면 나머지 프로미스를 기다리지 않고 즉시 종료된 후 rejected된 에러가 전달된다.
```js
const requestData1 = () => new Promise(resolve => setTimeout(() => resolve(1), 3000));
const requestData2 = () => new Promise(resolve => setTimeout(() => resolve(2), 2000));
const requestData3 = () => new Promise(resolve => setTimeout(() => resolve(3), 1000));

Promise.all([requestData1(), requestData2(), requestData3()])
  .then(console.log) // [ 1, 2, 3 ] ⇒ 약 3초 소요
  .catch(console.error);
```

#### Promise.race
Promise.all과 비슷하게 프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 받는다. 다만 Promise.all과 다르게 모든 프로미스가 fulfilled 상태가 되도록 기다리지 않고 가장 먼저 fulfilled된 프로미스의 처리결과를 반환한다. 하나라도 rejected 되면 그 즉시 에러를 반환한다.
```js
Promise.race([
  new Promise(resolve => setTimeout(() => resolve(1), 1000)), // 1
  new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
  new Promise(resolve => setTimeout(() => resolve(3), 3000)) // 3
])
  .then(console.log) // 1
  .catch(console.log);
```

#### Promise.allSettled
프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 전달받는다. 그리고 전부 settled(완료 또는 실패)상태가 되면 처리 결과를 배열로 반환한다.

```js
Promise.allSettled([
  new Promise(resolve => setTimeout(() => resolve(1), 2000)),
  new Promise((_, reject) => setTimeout(() => reject(new Error('Error!')), 1000))
]).then(console.log);
/*
[
  {status: "fulfilled", value: 1},
  {status: "rejected", reason: Error: Error! at <anonymous>:3:54}
]
*/
```

<br/>

### 마이크로태스크 큐
```js
setTimeout(() => console.log(1), 0);

Promise.resolve()
  .then(() => console.log(2))
  .then(() => console.log(3));
```
다음은 2,3,1순으로 처리된다. 이는 프로미스의 후속 처리 메서드의 콜백 함수는 태스크 큐가 아니라 마이크로태스크 큐에 저장되기 때문이다. 그리고 마이크로태스크 큐는 태스크 큐보다 우선순위가 높다.

