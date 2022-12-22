## 조건문 
주어진 조건식의 평가 결과에 따라 코드 블록을 실행한다.



#### if ... else 문
```javascript
var num = 2;
var kind;

if (num > 0)      kind = '양수';
else if (num < 0) kind = '음수';
else              kind = '영';

console.log(kind); // 양수
```

#### switch 문

```javascript
var year = 2000; // 2000년은 윤년으로 2월이 29일이다.
var month = 2;
var days = 0;

switch (month) {
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    days = ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}
console.log(days); // 29
```


<br/>


## 반복문
조건식의 평가 결과가 거짓일 때까지 반복된다.
#### for 문
```javascript
for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]`);
  }
}
```

#### while 문
```javascript
var count = 0;

while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}
```

#### do-while 문
```javascript
var count = 0;

do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```


<br/>


## break
코드블럭을 벗어난다
```javascript
var string = 'Hello World.';
var search = 'l';
var index;
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === search) {
    index = i;
    break; // 반복문을 탈출한다.
  }
}
```

<br/>


## continue
다음 반복으로 넘어간다
```javascript
for (var i = 0; i < string.length; i++) {
  if (string[i] !== search) continue;
  count++;
}
```
