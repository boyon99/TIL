# 타입 변환
개발자의 의도적에 따라 값의 타입을 변환하는 것을 **명시적 타입 변환** 또는 **타입 캐스팅**이라고 하며, 자바스크립트 엔진에 의해 암묵적으로 타입이 변환되는 것을 **암묵적 타입 변환** 또는 **타입 강제 변환**이라고 한다.


<br/>


## 암묵적 타입 변환 
자바스크립트 엔진에 의해 암묵적으로 타입이 변환되는 것을 의미하며 문자열 타입, 숫자 타입, 불리언 타입으로 변환할 수 있다.


<br/>


### 문자열 타입으로 변환
#### `+` 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작함.
```javascript
// 숫자 타입
0 + ''         // -> "0"
-0 + ''        // -> "0"
Infinity + ''  // -> "Infinity"
-Infinity + '' // -> "-Infinity"

// 불리언 타입
true + ''  // -> "true"
false + '' // -> "false"

// null 타입
null + '' // -> "null"

// undefined 타입
undefined + '' // -> "undefined"

// 심벌 타입
(Symbol()) + '' // -> TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''           // -> "[object Object]"
Math + ''           // -> "[object Math]"
[] + ''             // -> ""
[10, 20] + ''       // -> "10,20"
(function(){}) + '' // -> "function(){}"
Array + ''          // -> "function Array() { [native code] }"
```


<br/>


### 숫자 타입으로 변환 
반환할 수 없을 경우 NaN 값이 나타나며 `빈 문자열('')` `빈 배열([])` `null` `false`은 0으로 `true`는 1로 변환된다. 객체와 빈 배열이 아닌 배열, undefined는 변환되지 않아 NaN이 된다. 
#### 산술 연산자의 역할은 숫자 값을 만드는 것이므로 암묵적 타입 변환
```javascript
1 - '1'   // -> 0
1 * '10'  // -> 10
1 / 'one' // -> NaN (반환할 수 없을 경우 NaN을 반환한다.)
```
#### 비교 연산자의 경우 피연산자의 크기를 비교해야 하므로 암묵적 타입 변환
```javascript
'1' > 0  // -> true
```
#### + 단항 연산자의 경우 숫자 타입의 값으로 암묵적 타입 변환을 실행
```javascript
// 문자열 타입
+''       // -> 0
+'1'      // -> 1
+'string' // -> NaN (반환할 수 없을 경우 NaN을 반환한다.)

// 불리언 타입
+true     // -> 1
+false    // -> 0

// null 타입
+null     // -> 0

// undefined 타입
+undefined // -> NaN 

// 심벌 타입
+Symbol() // -> TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}             // -> NaN
+[]             // -> 0
+[10, 20]       // -> NaN
+(function(){}) // -> NaN
```


<br/>



### 불리언 타입으로 변환
불리언 값으로 평가되어야 할 문맥에서 truthy값은 true로 falsy값은 false 값으로 암묵적 타입 변환된다. falsy값으로는 `false` `undefined` `null` `0` `-0` `NaN` `''(빈 문자열)`
이 있다.
#### 제어문 또는 삼항 조건 연산자의 조걱식은 참과 거짓으로 표현해야 하므로 암묵적 타입 변환
```javascript
if (!false)     console.log(false + ' is falsy value');
if (!undefined) console.log(undefined + ' is falsy value');
if (!null)      console.log(null + ' is falsy value');
if (!0)         console.log(0 + ' is falsy value');
if (!NaN)       console.log(NaN + ' is falsy value');
if (!'')        console.log('' + ' is falsy value');
```


<br/>


## 명시적 타입 변환
개발자의 의도에 따라 타입을 변경하는 방법으로 문자열 타입, 숫자 타입, 불리언 타입으로 변환할 수 있다. 


<br/>


### 문자열 타입으로 변환
생성자 함수를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법, 암묵적 타입 변환을 이용하는 방법이 있다.
#### String 생성자 함수를 new 연산자 없이 호출하는 방법
```javascript
// 숫자 타입 => 문자열 타입
String(1);        // -> "1"
String(NaN);      // -> "NaN"
String(Infinity); // -> "Infinity"

// 불리언 타입 => 문자열 타입
String(true);     // -> "true"
String(false);    // -> "false"
```

#### Object.prototype.toString 메서드를 사용하는 방법
```javascript
// 숫자 타입 => 문자열 타입
(1).toString();        // -> "1"
(NaN).toString();      // -> "NaN"
(Infinity).toString(); // -> "Infinity"

// 불리언 타입 => 문자열 타입
(true).toString();     // -> "true"
(false).toString();    // -> "false"
```

#### 문자열 연결 연산자를 이용하는 방법
```javascript
// 숫자 타입 => 문자열 타입
1 + '';        // -> "1"
NaN + '';      // -> "NaN"
Infinity + ''; // -> "Infinity"

// 불리언 타입 => 문자열 타입
true + '';     // -> "true"
false + '';    // -> "false"
```


<br/>


### 숫자 타입으로 변환
생성자 함수를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법, 암묵적 타입 변환을 이용하는 방법이 있다.

#### Number 생성자 함수를 new 연산자 없이 호출하는 방법
```javascript
// 문자열 타입 => 숫자 타입
Number('0');     // -> 0
Number('10.53'); // -> 10.53

// 불리언 타입 => 숫자 타입
Number(true);    // -> 1
Number(false);   // -> 0
```
#### parseInt, parseFloat 함수를 사용하는 방법 (문자열만 변환 가능)
```javascript
// 문자열 타입 => 숫자 타입
parseInt('0');       // -> 0
parseFloat('10.53'); // -> 10.53
```
#### + 단항 산술 연산자를 이용하는 방법
```javascript
// 문자열 타입 => 숫자 타입
+'-1';    // -> -1
+'10.53'; // -> 10.53

// 불리언 타입 => 숫자 타입
+true;    // -> 1
+false;   // -> 0
```

#### * 산술 연산자를 이용하는 방법
```javascript
// 문자열 타입 => 숫자 타입
'0' * 1;     // -> 0
'10.53' * 1; // -> 10.53

// 불리언 타입 => 숫자 타입
true * 1;    // -> 1
false * 1;   // -> 0
```


<br/>


### 불리언 타입으로 변환
false 값으로는 `false` `undefined` `null` `0` `-0` `NaN` `''(빈 문자열)`이 있다.
#### Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
```javascript 
// 문자열 타입 => 불리언 타입
Boolean('x');       // -> true
Boolean('');        // -> false
Boolean('false');   // -> true (빈 문자열이 아니므로)

// 숫자 타입 => 불리언 타입
Boolean(0);         // -> false
Boolean(1);         // -> true
Boolean(NaN);       // -> false
Boolean(Infinity);  // -> true

// null 타입 => 불리언 타입
Boolean(null);      // -> false

// undefined 타입 => 불리언 타입
Boolean(undefined); // -> false

// 객체 타입 => 불리언 타입
Boolean({});        // -> true
Boolean([]);        // -> true
```

#### ! 부정 논리 연산자를 두번 사용하는 방법
```javascript
!!'x';       // -> true
!!'';        // -> false
```



