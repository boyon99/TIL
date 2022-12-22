## 템플릿 리터럴 (template literal)이란?
멀티라인 문자열, 표현식 삽입, 태그드 템플릿 등 편리한 문자열 처리를 제공한다. 템플릿 리터럴은 런타임에서 문자열로 변환되어 처리한다. ``을 사용해 표현한다.
```javascript
var template = `Template literal`;
console.log(template); // Template literal
```


<br/>



#### 일반적인 경우 줄바꿈 등을 사용해야 할 때 - 이스케이프 시퀀스
```javascript
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';
console.log(template);
```
```javascript
<ul>
  <li><a href="#">Home</a></li>
</ul>
```

#### 템플릿 리터널 내에서 사용할 때 - 멀티라인 문자열
```javascript
var template = `<ul>
  <li><a href="#">Home</a></li>
</ul>`;
console.log(template);
```
```javascript
<ul>
  <li><a href="#">Home</a></li>
</ul>
```


<br/>


#### 일반적인 경우 문자열을 연결할 때 - `+`
```javascript
var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.'); // My name is Ung-mo Lee.
```

#### 템플릿 리터널 내에서 연결할 때 - 표현식 삽입 `${}`
```javascript
var first = 'Ung-mo';
var last = 'Lee';

console.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.
console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3


```
