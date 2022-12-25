# **미리 정의된 전역 함수 (predefined functions)**

## eval()


문자열로 표현된 자바스크립트 코드를 실행하는 함수 `eval("문자열");`

```jsx
var x = 10, y = 20;
var a = eval("x + y"); // 30
var b = eval("y * 3"); // 60
```

<br/>


## isFinite()


전달된 값이 유한한 수인지를 검사하여 그 결과를 참과 거짓으로 반환. 만약 인수로 전달된 값이 숫자가 아니라면, 숫자로 변환하여 검사 `isFinite(검사할값);`


<br/>


## isNaN()


함수는 전달된 값이 NaN(Not-A-Number)인지를 검사하여 그 결과를 참과 거짓으로 반환. 만약 인수로 전달된 값이 숫자가 아니라면, 숫자로 강제 변환하여 검사. typeof 연산자 또는 Number.isNaN() 메소드를 대신 사용할 수도 있다. `isNaN(검사할값);`



<br/>


## parseFloat()


문자열을 파싱하여 부동 소수점 수(floating point number)로 반환 `parseFloat("문자열");`

```jsx
parseFloat("123");       // 123
parseFloat("123.000");   // 123
parseFloat("123.456");   // 123.456
parseFloat("12 34 56");  // 12
parseFloat(" 123 ");     // 123
parseFloat("123 초콜릿"); // 123
parseFloat("초콜릿 123"); // NaN
```



<br/>



## parseInt()


문자열을 파싱하여 정수로 반환 `parseInt("문자열");` 전달받은 문자열의 시작이 "0x"로 시작하면, parseInt() 함수는 해당 문자열을 16진수로 인식. 또한 "0"로 시작하면, 해당 문자열을 8진수로 인식했으나 더 이상 이 문법을 지원하지 않음.

```jsx
parseInt("123");        // 123
parseInt("123.000");    // 123
parseInt("123.456");    // 123
parseInt("12 34 56");   // 12
parseInt(" 123 ");      // 123
parseInt("123 초콜릿"); // 123
parseInt("초콜릿 123"); // NaN
parseInt("10", 10);     // 10
parseInt("10", 8);      // 8
parseInt("10", 16);     // 16
parseInt("0x10");       // 16
```



<br/>


## encodeURI()와 encodeURIComponent()


`encodeURI()`함수는 URI에서 주소를 표시하는 특수문자를 제외하고, 모든 문자를 이스케이프 시퀀스(escape sequences) 처리하여 부호화한다. `encodeURIComponent()`함수는 URI에서 `encodeURI()` 함수에서 부호화하지 않은 모든 문자까지 포함하여 이스케이프 시퀀스 처리한다.

`encodeURI(부호화할URI);`

`encodeURIComponent(부호화할URI);` 

```jsx
*var* uri = "http://google.com/search.php?name=홍길동&city=서울";
var enc1 = encodeURI(uri); // http://google.com/search.php?name=%ED%99%8D%EA%B8%B8%EB%8F%99&city=%EC%84%9C%EC%9A%B8
var enc2 = encodeURIComponent(uri); // http%3A%2F%2Fgoogle.com%2Fsearch.php%3Fname%3D%ED%99%8D%EA%B8%B8%EB%8F%99%26city%3D%EC%84%9C%EC%9A%B8
```


<br/>



## decodeURI()와 decodeURIComponent()


decodeURI() 함수는 encodeURI() 함수나 다른 방법으로 만들어진 URI(Uniform Resource Identifier)를 해독. decodeURIComponent() 함수는 encodeURIComponent() 함수나 다른 방법으로 만들어진 URI 컴포넌트를 해독.

`decodeURI(해독할URI);`

`decodeURIComponent(해독할URI);`

```jsx
*var* uri = "http://google.com/search.php?name=홍길동&city=서울";
var enc1 = encodeURI(uri);
var enc2 = encodeURIComponent(uri);

var dec1 = decodeURI(enc1); // http://google.com/search.php?name=홍길동&city=서울
var dec2 = decodeURIComponent(enc2); // http://google.com/search.php?name=홍길동&city=서울
```


<br/>


## escape()와 unescape()


escape() 함수는 전달받은 문자열에서 특정 문자들을 16진법 이스케이프 시퀀스 문자로 변환한다. unescape() 함수는 전달받은 문자열에서 escape() 함수나 다른 방법으로 만들어진 16진법 이스케이프 시퀀스 문자를 원래의 문자로 변환한다. 더 이상 지원하지 않으므로 encodeURI() 함수나encodeURIComponent() 함수를 대신 사용해야 한다.

`escape("변환할문자열");`

`unescape("원래대로변환할문자열");`

```jsx
*var* str = "Hello! World ?#$";
var esc = escape(str); // Hello%21%09World%20%3F%23%24
var une = unescape(esc); // Hello! World ?#$
```


<br/>



## Number()


Number() 함수는 전달받은 객체의 값을 숫자로 반환 `Number(객체);`

```jsx
Number("123");        // 123
Number("123.000");    // 123
Number("123.456");    // 123.456
Number("12 34 56");   // NaN
Number("123 초콜릿"); // NaN
Number(true);         // 1
Number(false);        // 0
Number(new Date());   // 현재 날짜에 해당하는 숫자를 반환함.
Number(null);         // 0
```


<br/>


## String()


String() 함수는 전달받은 객체의 값을 문자열로 반환 `String(객체);`
