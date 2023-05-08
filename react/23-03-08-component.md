# 컴포넌트

컴포넌트를 선언하는 방식

- **함수 컴포넌트** : 클래스형 컴포넌트보다 선언하기가 쉬우며 메모리 자원도 덜 사용한다. 함수 컴포넌트와 훅을 사용하는 방법을 방법을 권장한다.
- **클래스형 컴포넌트** : render 함수가 반드시 있어야 하며 그 안에서 보여줘야 할 JSX를 반환해야 한다.

> **reactjs code snippet** 사용 시 `rsc` 입력 후 tab을 누르면 자동으로 컴포넌트를 생성해준다. 클래스형 컴포넌트의 경우 `rcc`를 입력한다.

<br/>

## Props

props는 properties를 줄인 표현으로 컴포넌트의 속성을 설정할 때 사용하는 요소이다. props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정할 수 있다.

### 함수 컴포넌트에서 props 사용하기

#### JSX 내부에서 props 렌더링 및 props 값 지정하기

```js
// MyComponent.js
const MyComponent = (props) => {
  return <div>나의 새롭고 멋진 {props.name} 컴포넌트</div>;
};
```

```js
// app.js
import MyComponent from "./MyComponent";

function App() {
  return (
    <>
      <MyComponent name="react"></MyComponent>
    </>
  );
}
```

#### props 기본값 설정하기 : defaultProps

```js
// MyComponent.js
const MyComponent = (props) => {
  return <div>나의 새롭고 멋진 {props.name} 컴포넌트</div>;
};

MyComponent.defaultProps = {
  name: "기본 설정 이름",
};

export default MyComponent;
```

```js
// app.js
import MyComponent from "./MyComponent";

function App() {
  return (
    <>
      <MyComponent></MyComponent>
    </>
  );
}
```

#### 태그 사이의 내용을 보여 주는 children

```js
// MyComponent.js
const MyComponent = (props) => {
  return <div>childrend 값은 {props.children}입니다.</div>;
};
```

```js
// app.js
import MyComponent from "./MyComponent";

function App() {
  return (
    <>
      <MyComponent>리액트</MyComponent>
    </>
  );
}
```

#### 비구조화 할당 문법을 통해 props 내부 값 추출하기

props 값을 조회할 때마다 props.name, props.children과 같이 `props.`이라는 키워드를 사용한다. 이러한 작업을 더 편하게 하기 위해 비구조화 할당 문법을 사용하여 내부 값을 바로 추출하도록 한다.

```js
// MyComponent.js
const MyComponent = (props) => {
  const { name, children } = props;
  return (
    <div>
      나의 새롭고 멋진 {name} 컴포넌트. childrend 값은 {children}입니다.
    </div>
  );
};
```

더 쉽게 사용할 수 있다.

```js
const MyComponent = ({ name, children }) => {
  return (
    <div>
      나의 새롭고 멋진 {name} 컴포넌트. childrend 값은 {children}입니다.
    </div>
  );
};
```

#### propTypes를 통한 props 검증

컴포넌트의 필수 props를 지정하거나 타입을 지정하는 경우 propTypes를 사용한다.

```js
// MyComponent.js
import propTypes from "prop-types";

const MyComponent = ({ name, children }) => {
  return <div>나의 새롭고 멋진 {name} 컴포넌트</div>;
};

MyComponent.propTypes = {
  name: propTypes.string,
};
```

```js
function App() {
  return (
    <>
      <MyComponent name={3}></MyComponent>
      {/*인수로 string이 아닌 number의 값을 전달했기 때문에 에러가 발생한다.*/}
    </>
  );
}
```

#### isRequired를 사용하여 필수 propTypes 설정

propTypes를 지정하지 않은 경우 경고메세지를 호출한다.

```js
// MyComponent.js
import propTypes from "prop-types";

const MyComponent = ({ name, children }) => {
  return <div>나의 새롭고 멋진 {name} 컴포넌트</div>;
};

MyComponent.propTypes = {
  name: propTypes.number.isRequired,
};
```

> [더 많은 prop-types 알아보기](https://github.com/facebook/prop-types)

### 클래스형 컴포넌트에서 props 사용하기

클래스형 컴포넌트에서 props를 사용할 경우 render 함수에서 this.props를 조회한다. defaultPorps와 propTypes의 경우 동일한 방식으로 설정할 수 있다.

```js
// MyComponent.js
import propTypes from "prop-types";
import React, { Component } from "react";

class MyComponent extends Component {
  render() {
    const { name, children } = this.props;
    return (
      <div>
        {name} {children}
      </div>
    );
  }
}

MyComponent.defaultProps = {
  name: "기본 설정 이름",
};

MyComponent.propTypes = {
  name: propTypes.number.isRequired,
};

export default MyComponent;
```

다음과 같이 class 내부에서 지정할 수 있다.

```js
import propTypes from "prop-types";
import React, { Component } from "react";

class MyComponent extends Component {
  static defaultProps = {
    name: "기본 설정 이름",
  };
  static propTypes = {
    name: propTypes.number.isRequired,
  };
  render() {
    const { name, children } = this.props;
    return (
      <div>
        {name} {children}
      </div>
    );
  }
}

export default MyComponent;
```

<br/>

## state

컴포넌트 내부에서 바뀔 수 있는 값을 의미한다. 함수 컴포넌트에서 state를 사용하려면 `useState`를 사용해야 한다.

### 함수 컴포넌트에서 useState를 사용하여 state 사용하기

```js
import React, { useState } from "react";

const example = () => {
  const [number, setNumber] = useState(1);
  return (
    <div>
      <h2>{number}</h2>
      <button
        onClick={() => {
          setNumber((number) => number + 1);
        }}
      >
        +1
      </button>
    </div>
  );
};
```

### 클래스형 컴포넌트에서 state 사용하기

```js
// Counter.js
import React, { Component } from "react";

class Counter extends Component {
  // constructor
  // 컴포넌트의 생성자 메서드로 클래스형 컴포넌트에서 constructor를 작성할 때는 반드시 super 키워드를 호출해야 한다.
  constructor(props) {
    super(props); // 이를 통해 생성자 함수를 호출한다.
    // state 초기값을 설정하며 객체 형식이여야 한다.
    this.state = {
      number: 0,
    };
  }

  // render
  // render()함수에서 state를 조회할 경우 this.state로 조회한다.
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            // this.setState를 사용하여 state에 새로운 값을 지정한다.
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

#### state를 constructor에서 꺼내서 초기값을 지정할 수 있다.

```js
class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0,
  };
  render() { ... }
}
```

#### this.setState에 객체 대신 함수 인자 전달하기

```js
// this.setState의 인자로 함수를 넣어줄 때는 다음과 같이 작성한다. 여기서 prevState는 기존 상태이며 porps는 현재 지니고 있는 props를 가리킨다.
this.setState((prevState, props) => {
  return {
    // 업데이트 하고 싶은 내용
  };
});
```

```js
<button
  onClick={() => {
    this.setState((prevState) => {
      return {
        number: prevState.number + 1,
      };
    });
  }}
>
  +1
</button>
```

#### this.setState가 끝난 후 특정작업 시작하기

setState의 두 번째 파라미터로 콜백함수를 등록하여 작업을 처리할 수 있다.

```js
<button
  onClick={() => {
    this.setState({ number: number + 1 }, () => {
      console.log("호출");
    });
  }}
>
  +1
</button>
```

### state 사용할 때 주의 사항

#### 불변성을 지켜야 한다.

클래스형 컴포넌트든 함수 컴포넌트든 state 사용시 state 값을 바꿀 때는 setState 또는 useState를 사용한다. 배열이나 객체의 경우 사본을 만들어 그 사본의 값을 업데이트 한 이후 갱신해서 불변성을 지켜야 한다.

```js
// 객체
const object = { a: 1, b: 2 };
const copyObject = { ...object, b: 1 };

// 배열
const array = [1, 2, 3];
let copyArray = array.concat(4); // 새 항목 추가
```

#### state 변경함수는 async(비동기적)으로 실행된다.

state 변경함수는 비동기적으로 처리되는 함수로, 긴 시간이 소요되는 함수인 경우 남겨두고 다음 코드를 실행한다. 이에 따라 예기치 못한 오류가 생길 수 있다. 이때 `useEffect`을 통해 해결할 수 있다.
