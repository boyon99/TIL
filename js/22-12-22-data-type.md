# 원시 타입 primitive type

- 변경 불가능한 값
- 원시 값을 변수에 할당하면 변수(메모리 공간)에는 실제 값이 저장된다
- 다른 변수에 할당하면 원시 값이 복사되는데 이를 `값에 의한 전달`이라고 한다. (다른 메모리 공간에 저장된 별개의 값)

```js
let a = 5;
let b = a;

a = 7;
console.log(a, b); // 5 7
```

<br/>

## 숫자타입

정수, 실수 등을 구분하지 않고 하나의 숫자 타입 만이 존재한다.

#### 모두 숫자 타입이다.

```javascript
var integer = 10; // 정수
var double = 10.12; // 실수
var negative = -20; // 음의 정수
```

#### 2진수, 8진수, 16진수를 표현하기 위한 데이터 타입을 제공하지 않는다.

```javascript
var binary = 0b01000001; // 2진수
var octal = 0o101; // 8진수
var hex = 0x41; // 16진수
```

#### 숫자 타입은 모두 실수로 처리된다.

```javascript
console.log(1 === 1.0); // true
console.log(4 / 2); // 2
console.log(3 / 2); // 1.5
```

#### 숫자 타입은 세 가지 특별한 값을 표현할 수 있다

```javascript
console.log(10 / 0); // Infinity (양의 무한대)
console.log(10 / -0); // -Infinity (음의 무한대)
console.log(1 * "String"); // NaN (Not-A-Number)
```

<br/>

## 문자열 타입

텍스트 데이터를 나타내는데 사용된다. 문자열은 ''또는 ""또는 ``으로 텍스트를 감싼다.

```javascript
var string;
string = "문자열"; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱 (ES6)

string = '작은따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.';
string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.";
```

<br/>

## 불리언 타입

`true`와 `false` 두 가지 값인 논리 데이터이다.

```javascript
var foo = true;
console.log(foo); // true

foo = false;
console.log(foo); // false
```

<br/>

## undefined 타입

'값이 할당되지 않은 상태'를 나타낼 때 사용한다.

```javascript
var foo;
console.log(foo); // undefined
```

<br/>

## null 타입

null은 변수에 값이 없다는 것을 의도적으로 명시 할 때 사용한다. 또한, undefined란 null과는 달리 '타입'이 정해지지 않은 것을 의미한다.

```javascript
var foo = "Lee";
foo = null;
```

<br/>

## symbol 타입

변경 불가능한 원시 타입의 값으로 다른 값과 중복 되지 않는 유일무일하고 외부에 노출되지 않는 값이며 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다.

```javascript
var key = Symbol("key");
```

<br/><br/>

# 객체 타입 object type

6가지 타입 이외에는 모두 객체 타입이다. 객체, 함수, 배열 등이 있다.

- 객체는 변경 가능한 값
- 객체를 변수에 할당하면 변수에는 참조 값이 저장
- 객체의 경우 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달이라고 한다.

```javascript
var dog = { name: "해피", age: 3 }; // 객체의 생성
```
