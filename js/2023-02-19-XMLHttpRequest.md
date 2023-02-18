# XMLHttpRequest
브라우저는 주소창이나 HTML의 form 태그나 a 태그를 통해 HTTP 요청 전송 기능을 기본 제공한다. 자바스크립트를 사용하여 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용한다. Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 응답 수신을 위한 다양한 메서드와 프로퍼티를 제공한다.

<br/>


## XMLHttpRequest 객체 생성
XMLHttpRequest 생성자 함수를 호출하여 생성한다. 브라우저가 제공하는 Web API이므로 브라우저 환경에서만 정상적으로 실행된다.

```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();
```

<br/>

## XMLHttpRequest 객체의 프로퍼티와 메서드

| 프로토타입 프로퍼티 | 설명 |
| --- | --- |
| readyState | 요청상태를 나타낸다. 해당 프로퍼티로 클라이언트와 서버간 통신의 진행상태 알수 있다. <br/>- 0 : 초기화되지 않은 상태 <br/>- 1 : 로드되지 않은 상태. 즉 send() 호출되지 않은 상태 <br/>- 2 : 로드된 상태 <br/>- 3 : 상호작용 상태. 데이터 일부분만 받은 상태 <br/>- 4 : 완료 상태 |
| status | HTTP요청에 대한 응답 상태를 나타내는 정수 <br/> - 200 : 성공 <br/> - 404 : 페이지 찾을 수 없음 |
| statusText | 응답으로 반환된 상태 메세지 |
| response | HTTP 요청에 대한 응답몸체(responseType)에 따라 타입이 다르다. |
| responseType | HTTP 응답 타입 |
| responseText | 서버가 전송한 HTTP 요청에 대한 응답 문자열 |


| 이벤트핸들러 프로퍼티 | 설명 |
| --- | --- |
| onreadystatechange | readyState의 값인 요청상태가 변경될 때 발생하는 이벤트 |
| onlaodstart | 요청에 대한 응답을 받기 시작한 경우 |
| onprogress | 요청에 대한 응답을 받는 도중 주기적으로 발생 |
| onabort | abort 메서드에 의해 요청이 중단된 경우 |
| onerror | 요청에 애러가 발생한 경우 |
| onload | 요청이 성공적으로 이뤄진 경우 |
| ontimeout | 요청시간이 초과한 경우 |
| onloaded | 요청이 완료된 경우(실패 또는 성공) |

| 메서드 | 설명 |
| --- | --- |
| open | 요청 초기화 |
| send | 요청 전송 |
| abort | 이미 전송된 요청 중단 |
| setRequestHeader | 특정 요청 헤더의 값을 설정 |
| getResponseHeader | 특정 요청 헤더의 값을 문자열로 반환 |


| 정적프로퍼티 | 값 | 설명 |
| --- | --- | --- |
| UNSENT | 0 | open 메서드 호출 이전 |
| OPENED | 1 | open 메서드 호출 이후 |
| HEADERS_RECEIVED | 2 | send 메서드 호출 이후 |
| LOADING | 3 | 서버 응답 중 |
| DONE | 4 | 서버 응답 완료 |

<br/>

### HTTP 요청 전송
1. XMLHttpRequest.open 메서드로 HTTP 요청을 초기화한다.
2. XMLHttpRequest.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정한다.
3. XMLHttpRequest.send 메서드로 HTTP 요청을 전송한다.

```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
xhr.open('GET', '/users');

// HTTP 요청 헤더 설정
// 클라이언트가 서버로 전송할 데이터의 MIME 타입 지정: json
xhr.setRequestHeader('content-type', 'application/json');

// HTTP 요청 전송
xhr.send();
```

#### xhr.open(method, url, async)
- method : 요청 메서드 `GET` `POST` `PUT` `PATCH` `DELETE`
- url : 요청을 전송할 URL
- async : 비동기 요청 여부로 기본값은 true로 비동기 방식으로 동작한다.

#### xhr.send()
- GET 요청일 경우 데이터를 URL의 일부분인 쿼리 문자열로 서버에 전송한다.
- POST 요청일 경우 데이터를 요청 몸체에 담아 전송한다. 이때 직렬화한 다음 전달해야 한다.

```js
xhr.send(JSON.stringify({ id: 1, content: 'HTML', completed: false }));
```

#### xhr.setRequestHeader()
반드시 open 메서드를 호출한 이후에 호출해야 한다. content-type과 accept를 설정할 수 있다.

- content-type : mime 타입의 정보를 표시한다. 크게 `application/json` `text/plain` `multipart/form-data`이 있다.
- accept : 데이터의 mime 타입을 accept로 정할 수 있다. 이를 설정하지 않으면 호출 시 `*/*`로 전송된다.

```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
xhr.open('POST', '/users');

// HTTP 요청 헤더 설정
// 클라이언트가 서버로 전송할 데이터의 MIME 타입 지정: json
xhr.setRequestHeader('content-type', 'application/json');

// HTTP 요청 전송
xhr.send(JSON.stringify({ id: 1, content: 'HTML', completed: false }));
```

```js
// 서버가 응답할 데이터의 MIME 타입 지정: json
xhr.setRequestHeader('accept', 'application/json');
```

<br/>

### HTTP 응답 처리
응답을 처리하려면 XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 한다. 이는 브라우저 환경에서 실행해야 하며 요청 및 응답을 하려면 서버가 필요하다.

```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
// https://jsonplaceholder.typicode.com은 Fake REST API를 제공하는 서비스다.
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

// HTTP 요청 전송
xhr.send();

// readystatechange 이벤트는 HTTP 요청의 현재 상태를 나타내는 readyState 프로퍼티가
// 변경될 때마다 발생한다.
xhr.onreadystatechange = () => {
  // readyState 프로퍼티는 HTTP 요청의 현재 상태를 나타낸다.
  // readyState 프로퍼티 값이 4(XMLHttpRequest.DONE)가 아니면 서버 응답이 완료되지 상태다.
  // 만약 서버 응답이 아직 완료되지 않았다면 아무런 처리를 하지 않는다.
  if (xhr.readyState !== XMLHttpRequest.DONE) return;

  // status 프로퍼티는 응답 상태 코드를 나타낸다.
  // status 프로퍼티 값이 200이면 정상적으로 응답된 상태이고
  // status 프로퍼티 값이 200이 아니면 에러가 발생한 상태다.
  // 정상적으로 응답된 상태라면 response 프로퍼티에 서버의 응답 결과가 담겨 있다.
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.response));
    // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```

```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
// https://jsonplaceholder.typicode.com은 Fake REST API를 제공하는 서비스다.
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

// HTTP 요청 전송
xhr.send();

// load 이벤트는 HTTP 요청이 성공적으로 완료된 경우 발생한다.
xhr.onload = () => {
  // status 프로퍼티는 응답 상태 코드를 나타낸다.
  // status 프로퍼티 값이 200이면 정상적으로 응답된 상태이고
  // status 프로퍼티 값이 200이 아니면 에러가 발생한 상태다.
  // 정상적으로 응답된 상태라면 response 프로퍼티에 서버의 응답 결과가 담겨 있다.
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.response));
    // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
  } else {
    console.error('Error', xhr.status, xhr.statusText);
  }
};
```