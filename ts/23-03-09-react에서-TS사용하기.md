# React 프로젝트에서 Typescript 사용할 경우

## 설치하기
1. 이미 있는 React 프로젝트에 설치할 경우

```console
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

2. React 프로젝트를 새로 생성할 경우

```console
npx create-react-app my-app --template typescript
```

<br/>

## 리액트에서 TS 문법 사용하기
### 1. 일반 변수, 함수 타입지정
```js
// 일반적인 경우와 동일하다.
let box:string = "";

let num = function(a:string):string{
  return a
}
```

### 2. JSX 타입지정
```js
let 박스 :JSX.Element = <div></div>
let 버튼 :JSX.Element = <button></button>
```

### 3. function component 타입지정
JSX.Element는 자동으로 추가된다.
```js
type AppProps = {
  name: string;
}; 

function App (props: AppProps) :JSX.Element {
  return (
    <div>{message}</div>
  )
}
```

#### props로 JSX를 입력할 수 있게 코드를 작성하는 경우 `JSX.IntrinsicElements`라는 타입을 사용한다.
```js
type ContainerProps = {
  a: JSX.IntrinsicElements['h4'];
}; 

function Container (props: ContainerProps) {
  return (
    <div>{props.a}</div>
  )
}
```

### 4. state 문법 사용시 타입지정 
state 만들 경우 자동으로 타입이 할당된다.
```js
const [user, setUser] = useState<string | null>('kim');
```

### 5. type assertion 문법 사용할 경우
`as`키워드를 사용한다. 그러나 `as` 키워드는 강력하기 때문에 타입을 확신하는 경우에만 사용한다.

