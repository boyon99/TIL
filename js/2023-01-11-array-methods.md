# 배열 메소드

Array 생성자 함수는 정적 메서드를 제공하며 Array.prototype은 프로토타입 메서드를 제공한다.

#### true false 반환

- [Array.isArray](#isArray)
- [Array.prototype.includes](#includes)

#### 인덱스 반환

- [Array.prototype.indexOf](#indexOf)

#### 제거

- [Array.prototype.pop](#pop)
- [Array.prototype.shift](#shift)
- [Array.prototype.splice](#splice)

#### 추가

- [Array.prototype.push](#push)
- [Array.prototype.unshift](#unshift)
- [Array.prototype.concat](#concat)
- [Array.prototype.splice](#splice)

#### 변환

- [Array.prototype.slice](#slice)
- [Array.prototype.join](#join)
- [Array.prototype.reverse](#reverse)
- [Array.prototype.fill](#fill)
- [Array.prototype.flat](#flat)

<br/>

### <div id="isArray">Array.isArray</div>

전달된 인수가 배열이면 true, 아니면 false를 반환한다.

```js
// true
Array.isArray([]);
Array.isArray([1, 2]);
Array.isArray(new Array());

// false
Array.isArray();
Array.isArray({});
Array.isArray("Array");
Array.isArray({ 0: 1, length: 1 });
```

<br/>

### <div id="indexOf">Array.prototype.indexOf</div>

원본배열에서 인수로 전달된 요소를 검색하여 나온 첫번째 요소의 인덱스를 반환한다. 전달된 요소가 존재하지 않으면 -1을 반환한다. 2번째 인수는 검색을 시작할 인덱스이다.

```js
const arr = [1, 2, 2, 3];

// 배열 arr에서 요소 2를 검색하여 첫 번째로 검색된 요소의 인덱스를 반환한다.
arr.indexOf(2); // -> 1
// 배열 arr에 요소 4가 없으므로 -1을 반환한다.
arr.indexOf(4); // -> -1
// 두 번째 인수는 검색을 시작할 인덱스다. 두 번째 인수를 생략하면 처음부터 검색한다.
arr.indexOf(2, 2); // -> 2
```

<br/>

### Array.prototype.lastIndexOf

원본배열에서 인수로 전달된 요소를 검색하여 나온 마지막 요소의 인덱스를 반환한다.

```js
const arr = [1, 2, 2, 3];

// 배열 arr에서 요소 2를 검색하여 첫 번째로 검색된 요소의 인덱스를 반환한다.
console.log(arr.lastIndexOf(2)); // 2
```

<br/>

### <div id="push">Array.prototype.push</div>

인수로 전달받은 모든 값을 원본 배열의 마지막 요소에 추가하고 변경된 length 값을 반환한다. 원본 배열을 변경한다.

```js
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.push(3, 4);
console.log(result); // 4

// push 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 2, 3, 4]
```

#### 마지막에 추가할 요소가 하나라면 length 프로퍼티로 직접 추가하는 것이 더 빠르다.

```js
const arr = [1, 2];

// arr.push(3)과 동일한 처리를 한다. 이 방법이 push 메서드보다 빠르다.
arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

<br/>

### <div id="pop">Array.prototype.pop</div>

원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다. 빈 배열이면 undefined을 반환한다. 원본 배열을 직접 변경한다.

```js
const arr = [1, 2];

// 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.pop();
console.log(result); // 2

// pop 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

<br/>

### <div id="unshift">Array.prototype.unshift</div>

인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티의 값을 반환한다. 원본 배열을 변경한다.

```js
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.unshift(3, 4);
console.log(result); // 4

// unshift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 4, 1, 2]
```

<br/>

### <div id="shift">Array.prototype.shift</div>

원본 배열에서 첫번째 요소를 제거하고 제거한 요소를 반환한다. 빈 배열이면 undefined를 반환한다. 원본 배열을 변경한다.

```js
const arr = [1, 2];

// 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.shift();
console.log(result); // 1

// shift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [2]
```

<br/>

### <div id="concat">Array.prototype.concat</div>

인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다.

```js
const arr1 = [1, 2];
const arr2 = [3, 4];

// 배열 arr2를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
// 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.
let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

// 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
result = arr1.concat(3);
console.log(result); // [1, 2, 3]

// 배열 arr2와 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
result = arr1.concat(arr2, 5);
console.log(result); // [1, 2, 3, 4, 5]

// 원본 배열은 변경되지 않는다.
console.log(arr1); // [1, 2]
```

#### 인수로 전달받은 값이 배열인 경우 push와 unshift 메서드는 배열을 그대로 추가하지만 concat 메서드는 배열을 해체한 후 배열에 추가한다.

```js
const arr = [3, 4];

// unshift와 push 메서드는 인수로 전달받은 배열을 그대로 원본 배열의 요소로 추가한다
arr.unshift([1, 2]);
arr.push([5, 6]);
console.log(arr); // [[1, 2], 3, 4,[5, 6]]

// concat 메서드는 인수로 전달받은 배열을 해체하여 새로운 배열의 요소로 추가한다
let result = [1, 2].concat([3, 4]);
result = result.concat([5, 6]);

console.log(result); // [1, 2, 3, 4, 5, 6]
```

<br/>

### <div id="splice">Array.prototype.splice</div>

원본 배열의 중간에 요소를 추가하거나 제거하는 경우 사용한다. 3개의 매개변수가 있다. 원본 배열을 변경하며 제거된 값이 반환된다.

- start는 원본 배열의 요소를 제거하기 시작할 인덱스로 start만 있으면 start 인덱스부터 모든 요소를 제거한다. 음수인 경우 배열 끝에서의 인덱스이다.
- deleteCount는 start부터 제거할 요소의 개수이다. 0인 경우 아무런 요소도 제거되지 않는다.
- items는 제거할 위치에 삽입할 요소들의 목록이다.

```js
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
const result = arr.splice(1, 2, 20, 30);

// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3]
// splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 20, 30, 4]
```

<br/>

### <div id="slice">Array.prototype.slice</div>

인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다. 원본 배열은 변경하지 않는다. 2개의 매개변수를 가지며 복사를 시작 인덱스와 복사를 종료 인덱스로 종료 인덱스의 요소는 복사되지 않는다. 종료 인덱스는 생략 가능하며 기본값은 length 프로퍼티 값이다.

```js
const arr = [1, 2, 3];

// arr[0]부터 arr[1] 이전(arr[1] 미포함)까지 복사하여 반환한다.
arr.slice(0, 1); // -> [1]

// arr[1]부터 arr[2] 이전(arr[2] 미포함)까지 복사하여 반환한다.
arr.slice(1, 2); // -> [2]

// 원본은 변경되지 않는다.
console.log(arr); // [1, 2, 3]
```

#### 시작 인덱스가 음수인 경우 배열의 끝에서부터 요소를 복사하여 배열로 반환한다.

```js
const arr = [1, 2, 3];

// 배열의 끝에서부터 요소를 한 개 복사하여 반환한다.
arr.slice(-1); // -> [3]

// 배열의 끝에서부터 요소를 두 개 복사하여 반환한다.
arr.slice(-2); // -> [2, 3]
```

#### 인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.

```js
const arr = [1, 2, 3];

// 인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.
const copy = arr.slice();
console.log(copy); // [1, 2, 3]
console.log(copy === arr); // false
```

#### 이때 생성된 복사본은 얕은 복사이다.

```js
const todos = [
  { id: 1, content: "HTML", completed: false },
  { id: 2, content: "CSS", completed: true },
  { id: 3, content: "Javascript", completed: false },
];

// 얕은 복사(shallow copy)
const _todos = todos.slice();
// const _todos = [...todos];

// _todos와 todos는 참조값이 다른 별개의 객체다.
console.log(_todos === todos); // false

// 배열 요소의 참조값이 같다. 즉, 얕은 복사되었다.
console.log(_todos[0] === todos[0]); // true
```

<br/>

### <div id="join">Array.prototype.join</div>

원본 배열의 모든 요소를 문자열로 변환한 후 구분자로 연결한 문자열을 반환한다. 기본 구분자는 콤바(,)이다.

```js
const arr = [1, 2, 3, 4];

// 기본 구분자는 ','이다.
// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 기본 구분자 ','로 연결한 문자열을 반환한다.
arr.join(); // -> '1,2,3,4';

// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 빈문자열로 연결한 문자열을 반환한다.
arr.join(""); // -> '1234'

// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 구분자 ':'로 연결한 문자열을 반환한다.
arr.join(":"); // -> '1:2:3:4'
```

<br/>

### <div id="reverse">Array.prototype.reverse</div>

원본 배열의 순서를 반대로 뒤집는다. 원본 배열이 변경되며 반환값은 변경된 배열이다.

```js
const arr = [1, 2, 3];
const result = arr.reverse();

// reverse 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 2, 1]
// 반환값은 변경된 배열이다.
console.log(result); // [3, 2, 1]
```

<br/>

### <div id="fill">Array.prototype.fill</div>

인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 원본 배열은 변경된다.

```js
const arr = [1, 2, 3];

// 인수로 전달 받은 값 0을 배열의 처음부터 끝까지 요소로 채운다.
arr.fill(0);

// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [0, 0, 0]
```

두 번째 인수로 요소 채우기를 시작할 인덱스를 전달할 수 있다.

```js
const arr = [1, 2, 3];

// 인수로 전달받은 값 0을 배열의 인덱스 1부터 끝까지 요소로 채운다.
arr.fill(0, 1);

// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 0, 0]
```

세 번째 인수로 요소 채우기를 멈출 인덱스를 전달할 수 있다.

```js
const arr = [1, 2, 3, 4, 5];

// 인수로 전달받은 값 0을 배열의 인덱스 1부터 3 이전(인덱스 3 미포함)까지 요소로 채운다.
arr.fill(0, 1, 3);

// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 0, 0, 4, 5]
```

<br/>

### <div id="includes">Array.prototype.includes</div>

배열 내에 특정 요소가 있는지 확인하여 true나 false를 반환한다. 첫 번째 인수로 검색할 대상을 지정한다.

```js
const arr = [1, 2, 3];

// 배열에 요소 2가 포함되어 있는지 확인한다.
arr.includes(2); // -> true

// 배열에 요소 100이 포함되어 있는지 확인한다.
arr.includes(100); // -> false
```

두번째 인수로 검색을 시작할 인덱스를 전달할 수 있다. 생략 시 0이다. 음수를 전달하면 length 프로퍼티와 음수 인덱스를 합산하여 검색 시작 인덱스로 설정한다.

```js
const arr = [1, 2, 3];

// 배열에 요소 1이 포함되어 있는지 인덱스 1부터 확인한다.
arr.includes(1, 1); // -> false

// 배열에 요소 3이 포함되어 있는지 인덱스 2(arr.length - 1)부터 확인한다.
arr.includes(3, -1); // -> true
```

<br/>

### <div id="flat">Array.prototype.flat</div>

인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.

```js
[1, [2, 3, 4, 5]].flat(); // -> [1, 2, 3, 4, 5]
```

#### 중첩 배열을 평탄화할 깊이를 인수로 전달할 수 있다. 기본값은 1이다. Infinity를 전달하면 모두 평탄화한다.

```js
// 중첩 배열을 평탄화하기 위한 깊이 값의 기본값은 1이다.
[1, [2, [3, [4]]]].flat(); // -> [1, 2, [3, [4]]]
[1, [2, [3, [4]]]].flat(1); // -> [1, 2, [3, [4]]]

// 중첩 배열을 평탄화하기 위한 깊이 값을 2로 지정하여 2단계 깊이까지 평탄화한다.
[1, [2, [3, [4]]]].flat(2); // -> [1, 2, 3, [4]]
// 2번 평탄화한 것과 동일하다.
[1, [2, [3, [4]]]].flat().flat(); // -> [1, 2, 3, [4]]

// 중첩 배열을 평탄화하기 위한 깊이 값을 Infinity로 지정하여 중첩 배열 모두를 평탄화한다.
[1, [2, [3, [4]]]].flat(Infinity); // -> [1, 2, 3, 4]
```

<br/>
