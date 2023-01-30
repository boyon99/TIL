## dataset
HTML5에서 새로 확장된 속성으로 DOM 메서드로 데이터셋 속성에 접근할 수 있다. 자바스크립트는 DOM 생성 시점에 "data-"로 시작하는 속성들을 하나로 모아 "dataset" 맵으로 따로 모아 관리한다. 

```html
<div data-name="value"></div>
```

<br/>

JS에서 데이터셋 속성 추가
```js
element.setAttribute("data-name", "value")
```

JS에서 데이터셋 접근
```js
element.dataset.name
element.getAttribute('data-name')

```

CSS에서 데이터셋 접근
```css
.class[data-name='value']{}
```

