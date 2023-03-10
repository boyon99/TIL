# selectors

### 기본 선택자

1. 전체선택자 `*` 는 모든 요소를 선택한다.
2. 태그선택자는 `태그`를 선택한다.
3. 클래스 선택자 `.`는 클래스 속성인 값을 선택한다.
4. ID 선택자 `#` 는 ID 속성인 값을 선택한다.


<br/>


### 복합 선택자

- 일치 선택자는 여러 선택자를 동시에 만족하는 요소를 선택한다. `span.class`
- 자식 선택자 `>` 는 선택자의 자식 요소를 선택한다.
- 후손 선택자  ` ` 는 선택자의 하위 요소를 선택한다.
- 인접 형제 선택자 `+` 는 선택자의 다음 형제 요소 중 하나를 선택한다.

```html
<ul>
<!--.C의 이전 요소-->
        <li>A</li>
        <li>B</li>
<!--.C-->
        <li class="C">C</li>
<!--.C의 다음 요소-->
        <li>D</li> 
        <li>E</li>
    </ul>
```

```css
.C + li{
    color: aquamarine; /*D의 색상만 변경됨*/
}
```

- 일반 형제 선택자 `~` 는 다음 형제 요소 전체를 선택한다.


<br/>


### 가상 클래스 선택자 `:`

- `:active`는 마우스를 클릭하고 있는 동안 선택한다.
- `:hover`는 마우스 커서가 올라가 있는 동안에만 선택한다.
- `:link`는 방문하지 않은 링크를 선택하고 `:visited`는 방문 링크를 선택한다.
- `:fouus`는 요소가 포커스되면 선택한다.
- `:first-child`는 형제 요소 중 첫째를 `:last-child`는 마지막을 `:nth-child(n)`는 n번째를 선택한다.

```css
ul > *:nth-child(n){
    color: aquamarine; /* 모든 항목의 색상이 변경됨
2n인 경우 짝수, 2n+1은 홀수이며 n+2는 2번 이외에 모든 색상을 의미한다 */
}
```

- `:not(selector)`는 선택자가 아닌 요소를 선택한다.
- `:empty`는 선택자의 자식 요소가 없을 때 선택한다.

<br/>

[가상 클래스 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/:active)에서 더 많은 가상 클래스 선택자를 확인할 수 있다.

<br/>


### 가상 요소 선택자  `::`

- `::before`은 선택자 요소의 내부 앞에 내용을 삽입한다. `content` 속성이 필수이다.

```html
<div class="box">div class box</div>
```

```css
.box::before{
    content: "before"; /*before div class box*/
}
```

- `::after`은 선택자 요소의 내부 뒤에 내용을 삽입한다. `content` 속성이 필수이다.
- `::first-letter`은 첫 문자를 선택하고 `::first-line`은 첫 줄을 선택한다.
- `::placeholder`은 요소의 해당 값을 선택한다.


<br/>

[가상 요소 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/::after)에서 더 많은 가상 요소 선택자를 확인할 수 있다.

<br/>

### 속성선택자 `[]`

- 속성선택자 `[type]`은 해당 속성이 포함된 요소를 선택한다. 
- `[attr=value]`는 일치하는 요소를 `[attr^=value]` 는 시작을 `[attr$=value]` 는 끝을 `[attr*=value]` 은 값이 포함된 요소를 선택한다. 
- `[attr~=title]` 는 속성의 title 값이 `[attr|=lang]` 은 lang 값이 일치하는 요소를 선택한다.

<br/>

[속성 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/Attribute_selectors)에서 더 많은 속성선택자를 확인할 수 있다.



<br/>


### 우선순위

- `!important`을 사용한다.


| 선택자 방식 | 적용 예 | 선택자 우선 순위 | 혼용 방식의 점수 산정 | 비고 |
| --- | --- | --- | --- | --- |
| !important | !important | 속성 기준 가장 우선 | 속성 기준 가장 우선 | 속성 기준 가장 우선 |
| 인라인 스타일 | style=”” | 1 | 요소 기준 가장 우선 | 요소 기준 가장 우선 |
| ID 선택자 | #selector | 2 | 100 |  |
| CLASS 선택자 | .selector | 3 | 10 |  |
| 속성 기반 선택자 | a[href*=”#”] | 3 | 10 |  |
| 가상 클래스 | a:hover | 3 | 10 |  |
| 가상 요소 | span::after | 3 | 10 |  |
| 태그 선택자 | a | 4 | 1 |  |
| 전체 선택자 | * | 5 | 0 |  |
