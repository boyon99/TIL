## 변수 호이스팅이란?
변수 선언 경우, 실행 시점은 소스코드가 한 줄씩 순차적으로 실행되는 시점인 런타임이 아니라 그 이전 단계에서 실행된다. 다시 말해 자바스크립트 엔진은 먼저 모든 선언문을 소스코드에서 찾아내 실행한 후 다른 소스코드를 순차적으로 실행한다. 
이러한 자바스크립트 엔진의 특징을 변수 호이스팅이라고 한다.


<br/>


#### 변수 선언은 런타임 이전에 실행된다.
```javascript
console.log(score); // undefined
var score; // 변수 선언
```

#### 변수 선언만 런타임 이전에 실행되며 값의 할당은 순차적으로 실행된다.
```javascript
console.log(food); // undefined
var food = "apple"; 
console.log(food); // apple
```

#### 값을 이전에 선언해도 정상적으로 순차적 실행된다.
```javascript
console.log(number); // undefined
number = 8;
var number;
console.log(number); // 8
```

