# 리플로우와 리페인트

브라우저 화면에 무엇인가 출력하기 위해, 크기나 위치 등을 계산하는 과정을 리플로우(Reflow) 라고 한다. 리플로우 이후 화면에 실제 출력하는 과정을 리페인트(Repaint) 라고 한다.

노드의 크기, 여백, 위치 등 주변 노드에 영향을 주는 레이아웃 속성이 변경되면, 브라우저는 모든 노드를 리플로우하고 영향을 받은 모든 화면 영역을 다시 리페인트한다. 노드의 visibillty, outline, transform, filter, background-color, color 등, 주변 노드에 영향을 주지 않는 단순 표시 속성이 변경되면, 브라우저는 리플로우 없이 해당 노드만 리페인트한다.

### requestAnimationFrame()

브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 한다. 이 메소드는 리페인트 이전에 실행할 콜백을 인자로 받는다. 즉 브라우저의 리페인트 주기에 맞게 콜백을 실행한다.

```js
var start = null;
var element = document.getElementById("SomeElementYouWantToAnimate");
element.style.position = "absolute";

function step(timestamp) {
  if (!start) start = timestamp;
  var progress = timestamp - start;
  element.style.left = Math.min(progress / 10, 200) + "px";
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```
