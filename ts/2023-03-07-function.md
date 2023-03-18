# 함수

## this
함수 내 this는 전역 객체를 참조하거나(sloppy mode), undefined(strict mode)가 되는 등 우리가 원하는 콘텍스트(context)를 잃고 다른 값이 되는 경우들이 있다.
```js
const obj = {
  a: 'Hello',
  b: function () {
    console.log(this.a); // obj.a
    function b() {
      console.log(this.a); // error: global.a
    }
  }
};

obj.b() // Hello
```
이를 해결하기 위한 방법으로

1. bind 메소드를 사용해 this를 직접 연결해 주는 방법
```js
const b = obj.b.bind(obj);
b(); // Hello
```

> 타입스크립트에서 bind, call, apply 메소드는 기본적으로 인수 타입 체크를 하지 않기 때문에 컴파일러 옵션에서 strict: true(혹은 strictBindCallApply: true)를 지정해 줘야 정상적으로 타입 체크를 한다.

2. 화살표 함수를 사용하는 방법
```js
const b = () => obj.b();
b(); // Hello
```

> 화살표 함수는 호출된 곳이 아닌 함수가 생성된 곳에서 this를 포착한다.

<br/>

## 명시적 this
엄격 모드에서 this는 암시적인(implicitly) any 타입이기 때문에 에러가 발생한다. 이 경우 this의 타입을 명시적으로(explicitly) 선언할 수 있다. 다음과 같이 가짜(fake) 매개변수로 this를 선언한다.
```js
interface ICat {
  name: string
}

const cat: ICat = {
  name: 'Lucy'
};

function someFn(this: ICat, greeting: string) {
  console.log(`${greeting} ${this.name}`); // ok
}
someFn.call(cat, 'Hello'); // Hello Lucy
```

<br/>

## 오버로드 (Overloads)
이름은 같지만 매개변수 타입과 반환 타입이 다른 여러 함수를 가질 수 있는 것을 말한다. 함수 오버로드를 통해 다양한 구조의 함수를 생성하고 관리할 수 있다.

#### 함수에서 함수 선언부와 구현부의 매개변수 개수가 같아야 한다. 함수 구현부에 any가 자주 사용된다.
```js
function add(a: string, b: string): string; // 함수 선언
function add(a: number, b: number): number; // 함수 선언
function add(a: any, b: any): any { // 함수 구현
  return a + b;
}

add('hello ', 'world');
add(1, 2);
add('hello ', 2); // Error - No overload matches this call.
```

#### 인터페이스나 타입 별칭 등의 메소드 정의에서 사용가능하다. 타입 단언이나 타입 가드를 통해 함수 선언부의 동적인 매개변수와 반환 값을 정의할 수 있다.
```js
interface IUser {
  name: string;
  age: number;
  getData(x: string): string[];
  getData(x: number): string;
}

let user: IUser = {
  name: "",
  age: 36,
  getData: (data: any) => {
    if (typeof data === "string") {
      return data.split("");
    } else {
      return data.toString();
    }
  }
};

console.log(user.getData('hello')) // [ 'h', 'e', 'l', 'l', 'o' ]
console.log(user.getData(123)) // 123
```



