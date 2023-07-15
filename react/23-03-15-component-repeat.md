# 컴포넌트 반복

컴포넌트 반복시 `map()`함수를 사용하고 데이터를 추가할 경우에는 기존 배열을 변경하는 `push()`대신 새로운 배열을 생성하는 `concat()`함수를 사용한다. 데이터 제거 시에는 `filter()`함수를 사용한다.

### map() 함수

map()함수를 통해 반복된 컴포넌트를 쉽게 처리한다.

```js
import React from "react";

const IterationSample = () => {
  const names = [1, 2, 3, 4];
  const nameList = names.map((i) => <li>{i}</li>);
  return (
    <div>
      <ul>{nameList}</ul>
    </div>
  );
};

export default IterationSample;
```

이와 같이 변환할 수 있다. 그러나 이와 같은 경우 `key` prop가 없다는 경고가 나타난다.

<br/>

### key

리액트에서 key는 컴포넌트 배열을 렌더링했을 시 어떤 원소에 변동이 있는지를 알아내기 위해서 사용한다. key의 값은 언제나 유일해야 한다.

```js
const IterationSample = () => {
  {...}
  const nameList = names.map((i, index) => <li key={index}>{i}</li>);
  return (<></>);
};
```

> index 값을 key로 사용하면 리렌더링이 비효율적이다.

이에 따라 고유 id를 위한 state를 생성하였다.

```js
import React, { useState } from "react";

const IterationSample = () => {
  const [names, setNames] = useState([
    { id: 1, text: "눈사람" },
    { id: 2, text: "얼음" },
    { id: 3, text: "눈" },
    { id: 4, text: "바람" },
  ]);
  const [inputText, setInputText] = useState("");
  const [nextId, setNextId] = useState(5);

  const nameList = names.map((name) => <li key={name.id}>{name.text}</li>);
  return <ul>{nameList}</ul>;
};

export default IterationSample;
```

<br/>

### concat 함수

concat()함수를 통해 데이터를 추가하는 함수를 구현한다.

```js
const IterationSample = () => {
  {...}
  const onChange = e => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({
      id: nextId,
      text: inputText,
    });
    setNextId(nextId + 1);
    setNames(nextNames);
    setInputText('');
  };

  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{nameList}</ul>
    </>
  )
}
```

> 리액트에서 상태를 업데이트할 때는 기존 상태를 그대로 두면서 새로운 값을 상태로 설정해야 하는데 이러한 개념을 불변성 유지라고 한다.

<br/>

### filter 함수

filter()함수를 통해 제거하는 기능을 추가한다.

```js
const IterationSample = () => {
  {...}
    const onRemove = id => {
    const nextNames = names.filter(name => name.id !== id);
    setNames(nextNames);
  };
  const nameList = names.map(name => (
    <li key={name.id} onDoubleClick={() => onRemove(name.id)}>
      {name.text}
    </li>
  ));
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{nameList}</ul>
    </>
  );
}
```
