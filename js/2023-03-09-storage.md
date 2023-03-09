# Storage

Web Storage API의 Storage 인터페이스는 특정 도메인을 위한 세션 저장소 또는 로컬 저장소의 접근 경로로서 데이터를 키와 값의 형식으로 추가하고 수정하거나 삭제할 수 있다.

### sessionStorage

각각의 출처에 대해 독립적인 저장 공간을 페이지 세션이 유지되는 동안(브라우저가 열려있는 동안) 제공한다.

- 세션에 한정해, 즉 브라우저 또는 탭이 닫힐 때까지만 데이터를 저장합니다.
- 데이터를 절대 서버로 전송하지 않습니다.
- 저장 공간이 쿠키보다 큽니다. (최대 5MB)

### localStorage

브라우저를 닫았다 열어도 데이터가 남아있다.

- 저장 공간이 셋 중 제일 크다.
- 유효기간 없이 데이터를 저장하고, JavaScript를 사용하거나 브라우저 캐시 또는 로컬 저장 데이터를 지워야만 사라진다.

<br/>

## Storage 속성 및 메서드

### Storage.length

Storage 객체에 저장된 데이터 항목의 수를 반환한다.

```js
function populateStorage() {
  localStorage.setItem("bgcolor", "yellow");
  localStorage.setItem("font", "Helvetica");
  localStorage.setItem("image", "cats.png");

  return localStorage.length; // Should return 3
}
```

### Storage.key()

주어진 숫자 n에 대하여 저장소의 n번째 항목 키를 반환한다.

```js
for (var i = 0; i < localStorage.length; i++) {
  console.log(localStorage.getItem(localStorage.key(i)));
}
```

### Storage.setItem()

키가 저장소에 존재하는 경우 값을 재설정한다. 존재하지 않으면 키와 값을 저장소에 추가한다.

```js
function populateStorage() {
  localStorage.setItem("bgcolor", "red");
}
```

### Storage.getItem()

주어진 키에 연결된 값을 반환한다.

```js
function setStyles() {
  const currentColor = localStorage.getItem("bgcolor");
  document.getElementById("bgcolor").value = currentColor;
}
```

### Storage.removeItem()

주어진 키를 저장소에서 제거한다.

```js
function populateStorage() {
  localStorage.setItem("bgcolor", "red");
  localStorage.setItem("font", "Helvetica");
  localStorage.setItem("image", "myCat.png");

  localStorage.removeItem("image");
}
```

### Storage.clear()

저장소의 모든 키를 저장소에서 제거한다.

```js
function populateStorage() {
  localStorage.setItem("bgcolor", "red");
  localStorage.setItem("font", "Helvetica");
  localStorage.setItem("image", "miGato.png");

  localStorage.clear();
}
```

<br/>
