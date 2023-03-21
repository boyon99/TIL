## 단축 평가
논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는 것을 의미한다. 또한 단축 평가는 표현식을 평가하는 도중 평가 결과가 확정된 경우 나머지 과정을 생략한다.


<br/>


### 논리 연산자를 사용한 단축 평가
#### 논리곱 연산자는 두 개의 피연산자가 모두 true 일 때 true을 반환한다. 마지막으로 평가되는 true 값이 출력된다.
```javascript
'Cat' && 'Dog' // -> "Dog"
```

#### 논리합 연산자는 두 개의 피연산자 중 하나만 true여도 평가된다. 첫 번째 true 값을 반환한다.

```javascript
'Cat' || 'Dog' // -> "Cat"
```


<br/>


### 단축 평가를 사용하는 경우
#### 객체가 가리키기를 기대하는 변수가 null 또는 undefined 가 아닌지 확인하고 프로퍼티를 참조할 때 
```javascript
var elem = null;

// elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가되고
// elem이 Truthy 값이면 elem.value로 평가된다.
var value = elem && elem.value; // -> null
```
#### 함수 매개변수에 기본값을 설정할 때
```javascript
// 단축 평가를 사용한 매개변수의 기본값 설정
let obj;
obj = obj + 1 || 1
obj = obj + 1 || 1

console.log(obj) // 2
```


<br/>
<br/>


## 옵셔널 체이닝 연산자 `?.` 
`?.`는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티를 참조한다. `&&`는 false로 평가되는 값이면 좌항 피연산자를 그대로
반환하지만 옵셔널 체이닝 연산자는 null이나 undefined의 경우에만 그대로 반환한다.
```javascript
var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined
```


<br/>


## null 병합 연산자 `??`
`??`은 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 그렇지 않으면 좌항의 피연산자를 반환한다. `||`는 falsy 값으로 평가되는 값을 false로
반환하지만 `??`은 null 또는 undefined인 경우에만 반환한다.
```javascript
// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
var foo = null ?? 'default string';
console.log(foo); // "default string"
```
