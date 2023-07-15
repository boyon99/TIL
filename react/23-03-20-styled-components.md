# 컴포넌트 스타일링

- **CSS** : 컴포넌트를 스타일링하는 가장 기본적인 방식
- **SASS**
- **CSS Module**
- **styled-components** : 스타일을 자바스크립트 파일에 내장시키는 방법

<br/>

## CSS

CSS를 작성할 때 CSS 클래스를 중복되지 않게 만들어야 한다.

```js
// App.jsx
import "./App.css";
```

### CSS 클래스 이름짓기

1. 클래스 이름-클래스 형태 식으로 작성하기 `App-logo-spin`
2. BEM 방법론을 사용하기 `.card__title--primary`
3. CSS Selector를 사용하여 CSS 클래스가 특정 클래스 내부에 있는 경우에만 스타일을 사용하기 `.App .logo`

<br/>

## SASS

CSS 전처리기로 복잡한 작업을 쉽게 할 수 있게 해주며 스타일 코드의 재활용성 및 가독성을 높여 유지 보수를 더욱 쉽게 해준다. `npm add sass`로 설치한 후 CSS와 같이 사용한다.

```shell
yarn add sass
```

```jsx
// components/Button.jsx
import "../styles/Button.scss";

function Button() {
  return (
    <button className="Button small">
      <p>버튼</p>
    </button>
  );
}
```

```scss
// styles/Button.scss
$main-color: #3d3dff;

.Button {
  // 색상/테두리 스타일 적용
  background-color: $main-color;
}
```

### props 전달하기

props 를 통해서 class 이름을 추가할 수 있다.

```js
// components/Button.jsx
function Button({ size }) {
  return (
    <button className={`Button ${size}`}>
      <p>버튼</p>
    </button>
  );
}
```

```jsx
// app.js
import Button from "./components/Button";

function App() {
  return (
    <div>
      <Button size="large" />
      <Button size="medium" />
      <Button size="small" />
    </div>
  );
}

export default App;
```

```scss
// styles/Button.scss
$main-color: #3d3dff;

.Button {
  // 색상/테두리 스타일 적용
  background-color: $main-color;
  &.small {
    font-size: 16px;
  }
}
```

<br/>

## CSS Module

CSS를 불러와서 사용할 때 클래스 이름을 고유한 값인 `[파일이름]__[클래스이름]__[해시값]` 형태로 자동으로 만들어서 컴포넌트 스타일 클래스 이름이 중첩되는 현상을 방지해 주는 기술이다. `.module.css` 확장자로 파일을 저장하기만 하면 css module이 적용된다.

```js
import styles from "./CSSModule.module.scss";

{...}

const App = () => {
return (
<>
  <div className={styles.wrapper}>
  안녕하세요. 저는 <span className="something">CSS Modules</span>
  </div>
  // 2개 이상 적용하는 경우
  <div className={`${styles.wrapper} ${styles.inverted}`}/>
</>
)
}

```

CSS Module이 적용된 스타일 파일을 불러오면 객체를 전달받는다. 적용하려면 styles.[클래스이름] 형태로 전달해준다. `:global`을 사용하여 전역적으로 선언한 클래스의 경우 그냥 문자열로 넣어준다.

### classnames 라이브러리

css 클래스를 조건부로 설정하거나 css Moddule을 사용할 때 유용하다.

```console
npm add classnames
```

로 설치하며 사용법은 다음과 같다.

```js
import classNames from 'clasnames'

classNames('one','two') // 'one two'
classNames('one',{two: true}) // 'one two'
classNames('one',{two: false}) // 'one'
classNames('one',{"two", 'three'}) // 'one two three'

const myClass = 'hello'
classNames('one', myClass) // 'one hello'
```

여러 가지 종류의 파라미터를 조합하여 CSS 클래스를 설정할 수 있기 때문에 컴포넌트에서 조건부로 클래스를 설정할 때 매우 편리하다.

```js
const Mycomponent = ({heighted, theme}=>(
  <div classname={classNames("Mycomponent", {heighted}, theme)}>Hello</div>
  // 라이브러리를 사용하지 않을 경우
  // classname={`Mycomponent", ${heighted ? 'heighted': ""}, ${theme}`}
))
```

### 일반 CSS 파일에서 전역으로 사용하기

일반 CSS 파일에서도 `:local`을 사용하여 CSS 모듈 식으로 사용할 수 있다.

```css
:local .wrapper {
}
```

<br/>

## styled-components

자바스크립트 파일 안에 스타일을 선언하는 방식으로 이러한 방식을 CSS-in-JS라고 부른다. 관련 라이브러리는 [이곳](https://github.com/MicheleBertoli/css-in-js)에서 확인할 수 있다. 이중 가장 선호되는 라이브러리는 styled-components이다. props 값으로 전달해주는 값을 쉽게 스타일에 적용할 수 있다.

```console
npm add styled-components
```

#### 스타일링된 엘리먼트 만들기

컴포넌트 상단에 styled를 불러오고 `styled.태그명`을 사용하여 구현한다. 그 후 Tagged 템플릿 리터럴 문법을 통해 스타일을 넣으면 해당 스타일이 적용된 div로 이뤄진 리액트 컴포넌트가 생성된다.

```js
import React from "react";
import styled from "styled-components";

const example = () => {
  const Box = styled.div`
    width: 100px;
    height: 100px;
    background-color: #666;
  `;

  return (
    <div>
      <Box />
    </div>
  );
};
```

#### 스타일에서 props 조회하기

```js
const Box = styled.div`
  /* props 로 넣어준 값을 직접 전달해줄 수 있다. */
  background: ${(props) => props.color || 'blue'};
`;

{...}

return(
    <Box color="black" />
)
```

#### props에 따른 조건부 스타일링

조건부 스타일링을 props를 통해 처리할 수 있다.

```js
import styled from "styled-components";

export const Button = styled.button`
  background-color: ${({ isClicked }) => (isClicked ? "gray" : "blue")};
`;
```

```js
return (
  <S.Button isClicked={isClicked} onClick={() => setIsClicked(!isClicked)} />
);
```

#### 반응형 디자인

함수화하여 반응형 디자인을 만들 수 있다.

```js
const media = Object.keys(sizes).reduce((acc, label) => {
  acc[label] = (...args) => css`
    @media (max-width: ${sizes[label] / 16}em) {
      ${css(...args)};
    }
  `;

  return acc;
}, {});

const Box = styled.div`
  ${media.desktop`width: 768px;`}
  ${media.tablet`width: 100%;`};
`;
```

#### themeprovider 활용하기

`themeprovider`는 앱 전체에서 공통된 스타일 값을 쓸 수 있도록 도와주는 역할을 담당한다.

```js
// styles/theme.js
const palette = {
  orange: "#FFA500",
  black: "#000000",
};

const theme = {
  palette,
};

export default theme;
```

```js
// app.jsx
import { ThemeProvider } from "styled-components";
import theme from "./styles/theme";
import Button from "./components/Button";

function App() {
  return (
    <ThemeProvider theme={theme}>
      <Button />
    </ThemeProvider>
  );
}

export default App;
```

#### keyframes 활용하기

animation을 만들고자 할 때, keyframes을 만들기 위한 함수를 불러와서 사용할 수 있다.

```js
// button/style.js
import styled, { keyframes } from "styled-components";

const fadeIn = keyframes`
  from {
    opacity: 0
  }
  to {
    opacity: 1
  }
`;

export const Button = styled.button`
  animation-name: ${fadeIn};
  animation-duration: 1s;
  animation-timing-function: ease-out;
`;
```

#### globalstyle 활용해서 폰트 추가하기

앱 전체에 적용하고자 하는 속성이 있다면, `createGlobalStyle`을 통해서 스타일 컴포넌트를 만들고 해당 컴포넌트를 앱 전체에 적용한다. 일반적으로 앱 전체에서 사용하기 위한 폰트 등을 적용하고자 할 때 사용한다.

```js
// globalStyle.js
import { createGlobalStyle } from "styled-components";
import NotoSansBold from "../assets/fonts/NotoSansKR-Bold.otf";

export default createGlobalStyle`
    @font-face {
        font-family: "NotoSansBold";
        src: url(${NotoSansBold}) format('opentype');
    }
`;
```

이때 format(’opentype’) 부분은 폰트 파일의 확장자에 따라서 변경해야 한다.

- otf → opentype
- ttf → truetype
- woff → woff

```js
// app.js
import { ThemeProvider } from "styled-components";
import theme from "./styles/theme";
import Button from "./components/Button";
import GlobalStyle from "./styles/globalStyle";

function App() {
  return (
    <ThemeProvider theme={theme}>
      <GlobalStyle />
      <Button />
    </ThemeProvider>
  );
}

export default App;
```

```css
font-family: "NotoSansBold";
```
