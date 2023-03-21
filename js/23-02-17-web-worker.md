## web worker
자바스크립트 코드를 백그라운드에서 실행시킬 수 있는 HTML5 표준 기능으로 실행 시간이 긴 계산 작업을 별도로 백그라운드에서 실행시켜 사용자 인터페이스를 원할하게 할 수 있다.

<br/>

### 웹 워커 작동 원칙
- 자바스크립트 코드는 자바스크립트 파일형태로 만들어야 하며 웹 페이지와 동일한 웹 사이트에 설치되어 있는 자바스크립트 파일에 대해서만 웹 워커 기능이 작동한다. 이를 동일 도메인 원칙이라고 한다.
- 로컬 컴퓨터에 있는 웹 페이지에서는 작동하지 않는다.

<br/>

### 워커 테스크
웹 워커 기능을 이용하여 만든 백그라운드 태스크를 워커 태스크라고 한다.

#### 웹 워커 객체 생성
```js
let addWorker = new Worker(".js")
```

#### 워커 객체의 메소드
- `worker()` : 워커 태스크 생성
- `postMessage()` : 워커 태스크에 메시지 전송, 워커 태스크에는 message 이벤트 발생
- `terminate()` : 즉각 워커 태스크의 실행을 종료시킴

#### 워커 객체의 이벤트 리스너
- `onmessage` : 워커 태스크로부터 발생한 message 이벤트를 받는 리스너
- `onerror` : 오류를 발생할 때 받는 이벤트 리스너

#### 워커 태스크의 실행 환경
- UI 없는 실행 환경 
- 일부 프로퍼티와 메소드, 이벤트 리스너 및 자바스크립트 코어 객체들만 사용할 수 있다.
- 분리된 공간에서 실행하므로 변수나 메모리를 공유할 수 없다. 오직 message 이벤트를 통해서만 서로 정보를 교환한다.

#### 워커 태스크 종료
addWorker에 연결된 워커 태스크를 종료시킬 경우
```js
addWorker.terminate()
```

워커 태스크의 경우
```js
close()
```


<br/>

### 예제

#### 워커 태스크에서 워커 객체로 message 이벤트 보내기
```html
<body>
<div>1에서 10까지의 합은 <span id="sum"></span></div>
<script>
	// addWorker 워커 객체 생성 및 워커 태스크 시작
	let addWorker = new Worker("add1to10.js");
	
	// 워크 태스크로부터 message 이벤트 수신
	addWorker.onmessage = function (e) { // e는 MessageEvent 객체
		// 이벤트 객체의 data(합) 출력		
		document.getElementById("sum").innerHTML = e.data; 	
	}
</script>
</body>
```
```js
// add1to10.js
let sum = 0;
for(let i=0; i <= 10; i++){
  sum += i;
}

postMessage(sum);
```

#### 메인 태스크에서 워커 태스크로 message 이벤트 보내기
```html
<body>
<input id="sum" type="text" size="10">
<button type="button" id="add" onclick="send()">add</button>
<script>
	let addWorker = new Worker("add.js"); // 워커 태스크 생성

	function send() { // 워크 태스크에 시작 숫자와 끝 숫자 전송
		let parameters = {
			from: 10,
			to: 20
		};
		 // 시작 숫자와 끝 숫자를 담은 객체를 워커 태스크로 전송
		addWorker.postMessage(parameters);
	}

	// 워커 태스크로부터 결과를 기다리는 리스너 등록
	addWorker.onmessage = function (e) { 
		// 워커 태스크로부터 전달받은 합 출력
		document.getElementById("sum").value = e.data;
	}
</script>
</body>
```

```js
// add.js
onmessage = function(e){
  let sum = 0;
  let form = parseInt(e.data.from)
  let ro = parseInt(e.data.to)
  for(let i=from; i <= to; i++){
  sum += i;
  }
  postMessage(sum)
}
```


