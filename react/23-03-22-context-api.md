# Context API

리액트에서 전역적으로 사용할 데이터가 있을 때 유용하며 리덕스, 리액트 라우터, styled-components 등의 라이브러리는 Context API를 기반으로 구현되어 있다.

> [상세코드](https://codesandbox.io/s/react-context-api-oro1ix?file=/src/contexts/color.jsx)와 [레포](https://github.com/boyon99/state-management-library/tree/context)에서 구체적인 내용을 확인할 수 있다.

<br/>

## Context API를 사용한 전역 상태 관리 흐름 이해하기

주로 전역적으로 필요한 상태를 관리할 때는 최상위 컴포넌트인 App의 state에 넣어서 관리한다. 그러나 컴포넌트가 많아지는 경우 유지 보수성이 낮아질 수 있다. 이에 따라 Context API를 사용하면 Context를 만들어 한 번에 원하는 값을 받아 사용할 수 있다.

<br/>

## Context API 사용하기

### 새 context 만들기

`createContext()`함수를 사용하여 컨텍스트 객체를 생성한다. 이 객체에는`Provider`와 `consumer`라는 두 가지 주요 컴포넌트가 포함되어 있다.

```js
// contexts/color.js
import { createContext } from "react";

const ColorContext = createContext({ color: "black" });
export default ColorContext;
```

<img src="../img/context-default.png"/>

### Consumer 사용하기

`Context` 안에 있는 `Consumer`라는 컴포넌트를 통해 색상을 조회한다.

> Render Props란 컴포넌트의 children이 있어야 할 자리에 일반 JSX 혹은 문자열이 아닌 함수를 전달하는 것이다.

```js
// components/ColorBox.js
import React from "react";
import ColorContext from "../contexts/color";

const ColorBox = () => {
  return (
    <ColorContext.Consumer>
      {(value) => (
        <div
          style={{
            width: "64px",
            height: "64px",
            background: value.color,
          }}
        />
      )}
    </ColorContext.Consumer>
  );
};

export default ColorBox;
```

### Provider

`Provider`를 통해 `Context`의 vaule를 변경할 수 있다. 전에 createContext({ color: 'black' }); 처럼 기본값을 넣었는데 이는 `Provider`를 사용하지 않은 경우에만 사용한다. `Provider` 사용시 value를 반드시 명시해야 한다.

```js
// App.js
import ColorBox from "./components/ColorBox";
import ColorContext from "./contexts/color";
import React from "react";

const App = () => {
  return (
    <ColorContext.Provider value={{ color: "red" }}>
      <div>
        <ColorBox />
      </div>
    </ColorContext.Provider>
  );
};

export default App;
```

<br/>

## Consumer 대신 useContenxt Hook 사용하기

`useContenxt` 훅을 사용하면 함수 컴포넌트에서 `Context`를 쉽게 사용할 수 있다. 일반적으로 전 컴포넌트에서 공유되어야 하는 값이 있을 때만 사용하며, 각 컴포넌트로 별로만 관리하는 값일 경우 `useState`를 쓰는 것이 더 적절하다.

#### context 생성하기

```js
const UserContext = createContext();
```

#### Provider를 통해 컴포넌트를 감쌀 경우 하위 컴포넌트에서 항상 사용할 수 있다.

```jsx
<UserContext.Provider value={ 여러 컴포넌트에서 사용하고 싶은 값 }>
  <UserList />
</UserContext.Provider>
```

#### useContext를 통해 값을 불러온다.

```jsx
const Context = () => {
  const { color } = useContext(MyContext);

  return (
    <div
      style={{
        width: "64px",
        height: "64px",
        background: color,
      }}
    />
  );
};

export default Context;
```

기존에는 consumer 컴포넌트를 생성해야 했는데 useContext를 사용하면 value의 값을 바로 가져올 수 있다.
