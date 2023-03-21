# 마크다운이란?
Markdown은 텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌다. 쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 정보를 기록하는 README.md 문서로 마크다운을 통해서 설치방법, 소스코드 설명, 이슈 등을 간단하게 기록하고 가독성을 높일 수 있다는 강점이 있다.
<br/><br/>

## 마크다운 문법 정리
### 제목 Headers
`#`으로 시작하는 텍스트. 또는 `-`, `=`을 이용하여 h1, h2를 쓸 수 있다. `#`이 늘어날때마다 제목의 수준은 내려간다.

# H1 
```
# H1
```
```
H1 
===
```
## H2
```
## H2
```
```
H2 
---
```
### H3
```
### H3
```
#### H4
```
#### H4
```
##### H5
```
##### H5
```
###### H6
```
###### H6
```

<br/><br/>

### 인용 Blockquotes
`>`으로 시작하는 텍스트
<br>
> 인용문

```
> 인용문
```

> 인용문 
>> 인용문 안의 인용문
```
> 인용문 
>> 인용문 안의 인용문
```
> 인용문
>   > 두번째 인용문
>   >   > 세번째 인용문

```
> 인용문
>   > 두번째 인용문
>   >   > 세번째 인용문
```
<br/><br/>
### 강조 Emphasis
기울여 쓰기(italic)는 `*` `_`로 감싼 텍스트이며 굴게쓰기(bold) `**` `__`로 감싼 텍스트  

*기울여쓰기 italic*  
`*기울여쓰기italic*` `_기울여쓰기 italic_`  
<br/>
**굵게쓰기 bold**  
`**굵게쓰기 bold**` `__굵게쓰기 bold__`
<br/><br/><br/>

### 코드 블럭 Code Blocks
줄바꿈은 `~~~` 을 코드 첫줄과 마지막 줄에 3개 삽입하거나 `<pre><code>{code}</code></pre>`로 사용할 수 있다. 첫 `~~~`옆에 타입을 지정할 수 있다.  
<pre>
<code>
코드 블럭 Code Blocks
</code>
</pre>
은 다음과 같은 코드로 작성할 수 있다. 
```
<pre>
<code>
코드 블럭 Code Blocks
</code>
</pre>
```
<pre>
<code>
```
코드 블럭 Code Blocks
```
</code>
</pre>

<br/><br/>
### 인라인 코드 Inline Code Blocks
` `로 감싸진 텍스트 또는 4개의 공백 또는 tab으로 사용이 가능하다.<br/>
`인라인 코드 블럭`
~~~
`인라인 코드 블럭`
~~~
<br/><br/>

### 수평선 Horizontal Rules
`-` 또는 `*` 또는 `_` 을 3개 이상 작성 (단, -을 사용할 경우 header로 인식할 수 있으니 이 전 라인은 비워둬야 한다.)

---
***
___
```
---
***
___
```
<br/><br/>
### 링크 Links
###### 외부링크의 경우 다음과 같다.<br/>
[google](http://www.google.co.kr "google link입니다.")
```
[google](http://www.google.co.kr "google link입니다.")
```

<http://google.com/><br/>
<http://naver.com/>
```
<http://google.com/><br/>
<http://naver.com/>
```

###### 내부링크의 경우
`[링크이름]#id`로 사용할 수 있다. 
<br/><br/><br/>


### 리스트 Lists
각 항목에 대한 하위 리스트는 `여백(space bar) 세 칸`으로 구분한다. (한줄일 경우 같은 리스트로 판단한다.)<br/>

순서 있는 리스트 Ordered Lists의 경우 `숫자 다음 .`을 찍는다.
1. list 1
   1) list 1-1
   2) list 1-2
3. list 2
5. list 3
   1) list 3-1
```
1. list 1
   1) list 1-1
   2) list 1-2
3. list 2
5. list 3
   1) list 3-1
  ```
<br/>

순서 없는 리스트 Unordered Lists의 경우 `*`, `+`, `-`으로 시작한다.
* list 1
  + list 1-1
  + list 1-2
- list 2

```
* list 1
  + list 1-1
  + list 1-2
- list 2
```
<br/><br/>

### 체크 박스 Check box
`- [ ]` 입력으로 리스트를 체크박스 형태로 표시할 수 있다. `- [X]`은 체크된 형태로 나타난다.
- [ ] Checkbox 1
- [ ] Checkbox 2
- [X] Checkbox 3
```
- [ ] Checkbox 1
- [ ] Checkbox 2
- [X] Checkbox 3
```
<br/><br/>
### 테이블 Tables
테이블 생성 시 다음과 같다.
Header 1 | Header 2
--------- | ---------
Content 1 | Content 3
Content 2 | Content 4
```
Header 1 | Header 2
--------- | ---------
Content 1 | Content 3
Content 2 | Content 4
```
<br/><br/>

### 이미지 Adding Images
인라인 이미지의 경우 <br/>
![alt](/이미지주소 )
```
![alt](/이미지주소 )
```
<br/>

링크 이미지의 경우 <br/>
![alt](이미지URL) 
```
![alt](이미지URL)
```
<br/><br/>

### 접기 Fold
<details><summary>요약제목</summary>
요약내용
</details>

```
<details><summary>요약제목</summary>
요약내용
</details>
```
