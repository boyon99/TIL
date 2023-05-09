# 이벤트 헨들링

> [상세코드](../src/4/ValidationSample.js)에서 확인할 수 있다.

## 이벤트를 사용할 때 주의사항

- 이벤트 이름은 카멜 표기법으로 작성한다. `onClick` `onKeyUp`
- 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라 함수 형태의 값을 전달한다.
- DOM 요소에만 이벤트를 설정할 수 있고 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다.
- 리액트에서는 이벤트 핸들러를 root 태그에 할당해놓고 이벤트 위임에 대한 형태로 이벤트 함수를 실행시킨다.

<br/>

## 이벤트 버블링

하나의 요소에 이벤트가 발생하면, 해당 요소의 이벤트 핸들러 (함수) 가 작동하고, 이어서 그 부모 요소의 이벤트 핸들러가 작동하고, 그렇게 최상단의 요소까지 각 요소에 할당된 핸들러가 작동한다.

```js
import React from 'react';

function Bubble() {
  return (
    <div onClick={() => alert('나는 div')}>
      div입니다.
      <p onClick={() => alert('나는 p')}>p입니다.</p>
    </div>
  );
}

export default Bubble;
```

이러한 버블링으로 인해 `event.target` 과 `event.currentTarget`이 다르게 나타난다.

```js
import React from 'react';

function Bubble() {
  const onClick = (e) => {
    console.log(e.target, e.currentTarget);
    // <p>하위</p>
    // <div><p>하위</p></div>
  };

  return (
    <div onClick={onClick}>
      div입니다.
      <p onClick={onClick}>p입니다.</p>
    </div>
  );
}

export default Bubble;
```

즉 `event.target`은 이벤트 버블링이 발생하는 동안 변하지 않는 최초의 이벤트가 발생한 요소이고, `event.currentTarget`은 이벤트 버블링으로 인해 이벤트가 발생하고 있는 현재의 요소를 가리킨다. (이벤트 핸들러가 중첩되어있을 때만 존재함)

### 버블링 중단하기

이벤트 버블링을 중단할 때는 `e.stopPropagation`을 사용한다. 이런 경우 이벤트 버블링이 발생하지 않고 1번만 발생한다.

```js
const Test = () => {
  const onClick = (e) => {
    e.stopPropagation();
    console.log('onclick');
  };
  return (
    <div>
      <div onClick={onClick}>
        <p onClick={onClick}>하위</p>
      </div>
    </div>
  );
};
```

### 이벤트 위임

이벤트 위임이란 동일한 방식으로 여러 요소를 다뤄야 할 때 사용할 수 있다. 이때 이벤트 위임 방식으로 코드를 작성하면 더 효율적으로 코드를 작성할 수 있다.

```js
const Test = () => {
  const onClick = () => {
    console.log('onclick');
  };
  return (
    <div>
      <div onClick={onClick}>
        <p>하위</p>
        <p>하위</p>
        <p>하위</p>
      </div>
    </div>
  );
};
```

### 브라우저 기본 동작 방지하기

어떤 태그들은 기본적으로 특정한 동작이 실행되도록 설정이 되어있다. 예를 들어 a 태그는 누르면 해당 링크로 페이지가 넘어가고 form 태그를 사용할 때, 해당 태그 내부에서 button을 누르면 form 태그에 내장된 페이지 이동 기능이 작동하게 된다. 이러한 기본 동작을 방지하려면 `e.preventDefault()`를 사용한다.

```js
<a href="https://naver.com" onClick={(e) => e.preventDefault()}>
```

<br/>

## 이벤트 종류

리액트에서 지원하는 이벤트 종류는 다음과 같다. [다음](https://reactjs.org/docs/events.html)에서 더 자세한 사항을 확인해볼 수 있다.

- Clipboard
- Composition
- Keyboard
- Focus
- Form
- Generic
- Mouse
- Pointer
- Selection
- Touch
- UI
- Wheel
- Media
- Image
- Animation
- Transition
