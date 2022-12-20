# 속성 (properties)

`span {color:blue;}` 에서 `span`은 선택자이며, `color`는 속성(properties)이며 `blue`는 값(value)에 해당된다. 즉, `선택자 {속성:값;}`의 형식으로 이루어져 있다.


<br/>


## CSS background 속성


```css
background: #000 url(images/bg.gif) no-repeat top right;
```

| 속성 | 설명 |
| --- | --- |
| background | 모든 background 속성을 이용한 스타일을 한 줄에 설정할 수 있음. |
| background-color | HTML 요소의 배경색을 설정함. |
| background-image | HTML 요소의 배경 이미지를 설정함. |
| background-repeat | 설정된 배경 이미지의 반복 유무를 설정함. |
| background-position | 반복되지 않는 배경 이미지의 상대 위치를 설정함. |
| background-attachment | 배경 이미지를 스크롤과는 무관하게 해당 위치에 고정시킴. |


<br/>


## CSS text 속성


| 속성 | 설명 |
| --- | --- |
| color | 텍스트의 색상을 설정함. |
| direction | 텍스트가 쓰이는 방향을 설정함. |
| letter-spacing | 텍스트 내에서 문자 사이의 간격을 설정함. |
| word-spacing | 텍스트 내에서 단어 사이의 간격을 설정함. |
| text-indent | 단락의 첫 줄을 들여쓰기할지 안 할지를 설정함. |
| text-align | 텍스트의 수평 방향 정렬을 설정함. |
| text-decoration | 텍스트에 여러 가지 효과를 설정하거나 제거함. |
| text-transform | 텍스트에 포함된 영문자에 대한 대소문자를 설정함. |
| line-height | 텍스트의 줄 간격을 설정함. |
| text-shadow | 텍스트에 그림자 효과를 설정함. |
| unicode-bidi | direction 속성과 같이 사용하여 텍스트의 기본 출력 방향을 설정함. |
| vertical-align | HTML 요소 내의 수직 방향 정렬을 설정함. |
| white-space | HTML 요소 내의 여백을 설정함. |


<br/>


## CSS font 속성


```css
font: italic 1.2em "Fira Sans", serif;
```

| 속성 | 설명 |
| --- | --- |
| font | 모든 font 속성을 이용한 스타일을 한 줄에 설정할 수 있음. |
| font-family | 텍스트의 글꼴 집합(font family)을 설정함. |
| font-style | 주로 이탤릭체를 사용하기 위해 사용함. |
| font-variant | 텍스트에 포함된 영문자 중 소문자만을 작은 대문자(small-caps) 글꼴로 변경시킴. |
| font-weight | 텍스트를 얼마나 두껍게 표현할지를 설정함. |
| font-size | 텍스트의 크기를 설정함. |


<br/>


## 링크의 상태


| 상태 | 설명 |
| --- | --- |
| :link | 링크의 기본 상태이며, 사용자가 아직 연결된 페이지를 방문하지 않은 상태 |
| :visited | 사용자가 한 번이라도 해당 링크를 통해 연결된 페이지를 방문한 상태 |
| :hover | 사용자의 마우스 커서가 링크 위에 올라가 있는 상태 |
| :active | 사용자가 마우스로 링크를 클릭하고 있는 상태 |
| :focus | 키보드나 마우스의 이벤트 또는 다른 형태로 해당 요소가 포커스를 가지고 있는 상태 |


<br/>


## CSS list-style 속성


| 속성 | 설명 |
| --- | --- |
| list-style | 모든 list-style 속성을 이용한 스타일을 한 줄에 설정할 수 있음. |
| list-style-type | 리스트 요소의 마커(marker)를 설정함. |
| list-style-image | 리스트 요소의 마커로 사용할 이미지를 설정함. |
| list-style-position | 리스트 요소의 위치를 설정함. |


<br/>

## CSS table 속성


```css
border: 2px ****solid orange;
```

| 속성 | 설명 |
| --- | --- |
| border | 모든 border 속성을 이용한 스타일을 한 줄에 설정할 수 있음.  |
| border-collapse | 테이블의 테두리를 한 줄로 나타낼지를 설정함. |
| border-spacing | 테이블 요소(th, td)간의 여백을 설정함. |
| caption-side | 테이블의 캡션(caption)을 설정함. |
| empty-cells | 테이블 내의 빈 셀(cell)들의 테두리 및 배경색을 표현할지 안 할지를 설정함. |
| table-layout | 테이블에 사용되는 레이아웃 알고리즘을 설정함. |
