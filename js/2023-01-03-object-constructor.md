## object 생성자 함수
new 연산자와 함께 Object 생성자 함수를 호출하여 빈 객체를 생성한다. 
```js
// 빈 객체의 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(person); // {name: "Lee", sayHello: ƒ}
person.sayHello(); // Hi! My name is Lee
```

<br/>


## 생성자 함수
new 연산자와 함께 호출하여 객체를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를 인스턴스라고 한다. 
new 연산자와 함께 생성자 함수를 호출하지 않으면 일반 함수로 동작한다.

#### 객체 리터럴에 의한 객체는 단 하나의 객체만을 생성하지만, 생성자 함수에 의한 객체는 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.
```js
const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle1.getDiameter()); // 10

const circle2 = {
  radius: 10,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle2.getDiameter()); // 20
```

```js
// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

#### 생성자 함수와 일반 함수의 정의 방법은 같으며 new 연산자와 함께 호출하면 해당 함수는 생생자 함수로 동작하고 않으면 일반 함수로 동작한다. 
```js
// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다.
// 즉, 일반 함수로서 호출된다.
const circle3 = Circle(15);

// 일반 함수로서 호출된 Circle은 반환문이 없으므로 암묵적으로 undefined를 반환한다.
console.log(circle3); // undefined

// 일반 함수로서 호출된 Circle내의 this는 전역 객체를 가리킨다.
console.log(radius); // 15
```

<br/>


### 생성자 함수의 인스턴스 생성 과정 
#### 1. 인스턴스 생성과 this 바인딩
암묵적으로 빈 객체를 생성하는데 이 빈 객체는 생성자 함수가 생성한 인스턴스이다. 그리고 인스턴스는 this에 바인딩된다. 이 처리는 런타임 이전에 실행된다.
> 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 
```js
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Circle {}

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}
```

#### 2. 인스턴스 초기화
성자 함수의 코드가 실행되며 this에 바인딩되어 있는 인스턴스를 초기화한다.
```js
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}
```

#### 3. 인스턴스 반환 
생성자 함수 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this에 암묵적으로 반환된다.
```js
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };

  // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다
}

// 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환한다.
const circle = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
```

this 이외에 객체를 반환하면 return 문에 명시한 객체가 반환된다.
```js
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };

  // 3. 암묵적으로 this를 반환한다.
  // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
  return {};
}

// 인스턴스 생성. Circle 생성자 함수는 명시적으로 반환한 객체를 반환한다.
const circle = new Circle(1);
console.log(circle); // {}
```

원시 값을 반환하면 this가 반환된다. 
```js
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };

  // 3. 암묵적으로 this를 반환한다.
  // 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
  return 100;
}

// 인스턴스 생성. Circle 생성자 함수는 명시적으로 반환한 객체를 반환한다.
const circle = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
```

<br/>


## 내부 메서드 `[[Call]]`과 `[[Construct]]`
함수는 객체이지만 일반 객체와는 다르게 호출할 수 있다. 따라서 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드와 함수로서 동작하기 위해 함수 객체만을 위한 내부 슬롯과 메서드를 추가로 가진다. 
#### 함수가 일반 함수로서 호출하면 `[[Call]]`이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 `[[Construct]]`가 호출된다.
```js
function foo() {}

// 일반적인 함수로서 호출: [[Call]]이 호출된다.
foo();

// 생성자 함수로서 호출: [[Construct]]가 호출된다.
new foo();
```

#### `[[Call]]`을 가지면 callable, `[[Construct]]`을 가지면 constructor, 가지지 않으면 non-constructor라고 한다.
모든 함수는 호출할 수 있으므로 callable이지만 모든 함수 객체가 생성자 함수가 되지는 못한다. 
- constructor : 함수 선언문, 함수 표현식, 클래스
- non-constructor : 메서드, 화살표 함수 
```js
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function () {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수다. 이는 메서드로 인정하지 않는다.
const baz = {
  x: function () {}
};

// 일반 함수로 정의된 함수만이 constructor이다.
new foo();   // -> foo {}
new bar();   // -> bar {}
new baz.x(); // -> x {}

// 화살표 함수 정의
const arrow = () => {};

new arrow(); // TypeError: arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만을 메서드로 인정한다.
const obj = {
  x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor
```

<br/>

## new 연산자
일반 함수와 생성자 함수의 차이는 nwe 연산자와 함께 호출했나의 여부이다.
#### new 연산자 없이 함수를 호출하면 `[[Call]]`이 호출된다. 
```js
// 생성자 함수로서 정의하지 않은 일반 함수
function add(x, y) {
  return x + y;
}

// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
let inst = new add();

// 함수가 객체를 반환하지 않았으므로 반환문이 무시된다. 따라서 빈 객체가 생성되어 반환된다.
console.log(inst); // {}

// 객체를 반환하는 일반 함수
function createUser(name, role) {
  return { name, role };
}

// 일반 함수를 new 연산자와 함께 호출
inst = new createUser('Lee', 'admin');
// 함수가 생성한 객체를 반환한다.
console.log(inst); // {name: "Lee", role: "admin"}
```

#### new 연산자와 함께 호출하면 `[[Construct]]`가 호출된다. 
```js
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출된다.
const circle = Circle(5);
console.log(circle); // undefined

// 일반 함수 내부의 this는 전역 객체 window를 가리킨다.
console.log(radius); // 5
console.log(getDiameter()); // 10

circle.getDiameter();
// TypeError: Cannot read property 'getDiameter' of undefined
```

<br/>

> ### new.target 
>> 생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 ES6에서 지원하는 메타 프로퍼티로 IE에서는 지원하지 않는다. 
```js
// 생성자 함수
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
  if (!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter());  // 10
```

