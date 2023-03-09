# location

Location 인터페이스는 객체가 연결된 장소(URL)를 표현한다. Location 인터페이스에 변경을 가하면 연결된 객체에도 반영되는데, Document와 Window 인터페이스가 이런 Location을 가지고 있다. 각각 `Document.location`과 `Window.location`으로 접근할 수 있다.

## 속성

- `Location.href`: 전체 URL 주소
- `Location.protocol`: 프로토콜
- `Location.host`: 포트 번호를 포함한 도메인 이름
- `Location.hostname`: 도메인 이름
- `Location.port`: 포트 번호
- `Location.pathname`: 도메인 이후 경로
- `Location.search` : '?' 문자 뒤 URL의 쿼리스트링 값
- `Location.hash`: 해시 정보(페이지의 ID)
- `Location.origin` : 지정한 장소 오리진의 표준 형태

```js
var url = document.createElement("a");
url.href =
  "https://developer.mozilla.org:8080/en-US/search?q=URL#search-results-close-container";
console.log(url.href); // https://developer.mozilla.org:8080/en-US/search?q=URL#search-results-close-container
console.log(url.protocol); // https:
console.log(url.host); // developer.mozilla.org:8080
console.log(url.hostname); // developer.mozilla.org
console.log(url.port); // 8080
console.log(url.pathname); // /en-US/search
console.log(url.search); // ?q=URL
console.log(url.hash); // #search-results-close-container
console.log(url.origin); // https://developer.mozilla.org:8080
```

## 메소드

페이지가 항상 새로고침된다.

- `Location.assign(URL)`: 해당 '주소'로 페이지 이동
- `Location.replace(URL)`: 해당 '주소'로 페이지 이동, 현재 페이지 히스토리를 제거
- `Location.reload()`: 페이지 새로고침, `true` 인수는 '강력' 새로고침
