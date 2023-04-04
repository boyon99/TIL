# 메모리 누수

메모리 누수(Memory Leak)란, 더 이상 필요하지 않은 데이터가 해제되지 못하고 메모리를 계속 차지되는 현상입니다.

### 불필요한 전역 변수 사용

```js
window.hello = "Hello world!";
window.heropy = { name: "Heropy", age: 85 };
```

### 분리된 노드 참조

```html
<button>Remove!</button>

<div class="parent">
  <div class="child">1</div>
  <div class="child">2</div>
</div>
```

메모리 누수 예제

```js
const btn = document.querySelector("button");
const parent = document.querySelector(".parent");
btn.addEventListener("click", () => {
  console.log(parent); // <div class="parent">...</div>
  parent.remove();
});
```

메모리 누수 해결

```js
const btn = document.querySelector("button");
btn.addEventListener("click", () => {
  const parent = document.querySelector(".parent");
  console.log(parent); // <div class="parent">...</div>
  parent && parent.remove();
});
```

### 해제하지 않은 타이머

메모리 누수 예제

```js
let a = 0;
setInterval(() => {
  a += 1;
}, 100);
setTimeout(() => {
  console.log(a); // 10
}, 1000);
```

메모리 누수 해결

```js
let a = 0;
const intervalId = setInterval(() => {
  a += 1;
}, 100);
setTimeout(() => {
  console.log(a); // 10
  clearInterval(intervalId); // 타이머 해제!
}, 1000);
```
