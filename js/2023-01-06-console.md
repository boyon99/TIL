# console 메서드
`console.log(console)`을 출력하면 다음과 같이 나타난다. 이를 통해 console 메서드를 확인해볼 수 있다. 
```node
Object [console] {
  log: [Function: log],
  warn: [Function: warn],
  dir: [Function: dir],
  time: [Function: time],
  timeEnd: [Function: timeEnd],
  timeLog: [Function: timeLog],
  trace: [Function: trace],
  assert: [Function: assert],
  clear: [Function: clear],
  count: [Function: count],
  countReset: [Function: countReset],
  group: [Function: group],
  groupEnd: [Function: groupEnd],
  table: [Function: table],
  debug: [Function: debug],
  info: [Function: info],
  dirxml: [Function: dirxml],
  error: [Function: error],
  groupCollapsed: [Function: groupCollapsed],
  Console: [Function: Console],
  profile: [Function: profile],
  profileEnd: [Function: profileEnd],
  timeStamp: [Function: timeStamp],
  context: [Function: context]
}
```

<br/>


### `console.log`
```js
const person = {name:'lee', age:24, lang:['java', 'js', 'html', 'css']}

console.log(person) 
```
웹 콘솔에 메시지를 출력한다.
```console
{ name: 'lee', age: 24, lang: [ 'java', 'js', 'html', 'css' ] }
```

<br/>


### `console.dir`
```js
const person = {name:'lee', age:24, lang:['java', 'js', 'html', 'css']}

console.dir(person)
```
지정된 JavaScript 개체의 속성에 대한 대화형 목록을 표시한다.
```console
{ name: 'lee', age: 24, lang: [ 'java', 'js', 'html', 'css' ] }
```

<br/>

### `console.assert`
```js
const person = {name:'lee', age:24, lang:['java', 'js', 'html', 'css']}

console.assert(person.lang.find(lang => lang === 'node'), 'please learn node')
```
false인 경우 오류 메시지를 콘솔에 기록한다. 참이면 아무 일도 일어나지 않는다.
```console
Assertion failed: please learn node
```

<br/>

### `console.count`
```js
const person = {name:'lee', age:24, lang:['java', 'js', 'html', 'css']}

person.lang.forEach(lang => console.count('lang'))
```
특정 호출이 호출된 횟수를 기록한다.
```console
lang: 1
lang: 2
lang: 3
lang: 4
```

<br/>

### `console.table`
```js
const person = {name:'lee', age:24, lang:['java', 'js', 'html', 'css']}

console.table(person)
```
 테이블 형식 데이터를 테이블로 표시한다.
```console
┌─────────┬────────┬──────┬────────┬───────┬────────┐
│ (index) │   0    │  1   │   2    │   3   │ Values │
├─────────┼────────┼──────┼────────┼───────┼────────┤
│  name   │        │      │        │       │ 'lee'  │
│   age   │        │      │        │       │   24   │
│  lang   │ 'java' │ 'js' │ 'html' │ 'css' │        │
└─────────┴────────┴──────┴────────┴───────┴────────┘
```

<br/>

### `console.time()` `console.timeLog()` `console.timeEnd()`
```js
console.time()
console.timeLog() 
console.timeEnd() 
```
console.time()메서드는 작업 소요 시간을 추적하는 데 사용할 수 있는 타이머를 시작하며, console.timeLog()메서드는 이전에 호출하여 시작된 타이머의 현재 값을 기록하며, console.timeEnd()이전에 호출하여 시작된 타이머를 중지한다.
```console
default: 0.045ms
 default: 0.16ms
```

<br/>

### `console.trace`
```js
const parentFunc =  () => {
  const nestedFunc = () => {
    console.trace('How did i get here?')
  }
  nestedFunc()
}

parentFunc()
```
console.trace() 에 스택 추적을 출력한다.
```console
How did i get here?
  nestedFunc @ VM42:3
  parentFunc @ VM42:5
  (anonymous) @ VM42:8
```

<br/>

### `console.group` `console.groupEnd`
```js
console.group('parnet group')
        console.log('message1')
        console.log('message2')
        console.group('message3')
            console.log('message3-1')
            console.log('message3-2')
        console.groupEnd()
console.groupEnd()
```
console.group()는 로그에 새 인라인 그룹을 생성하여 console.groupEnd()가 호출 될 때까지 모든 후속 콘솔 메시지가 추가 수준으로 들여쓰기되도록 한다.
```console
parnet group
  message1
  message2
  message3
    message3-1
    message3-2
```

<br/>

## Reference
더 자세한 사항은 [mozilla console](https://developer.mozilla.org/ko/docs/Web/API/console)에서 확인할 수 있다.
