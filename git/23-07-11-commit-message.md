## 깃모지 시작하기

[깃모지](https://gitmoji.dev/)

- :hammer: Add or update development scripts.
- :lipstick: Add or update the UI and style files
- :iphone: Work on responsive design.
- (:dizzy: Add or update animations and transitions.
- :bug: Fix a bug
- :wrench: Add or update configuration files.
- :package: Add or update compiled files or packages.
- :bulb: Add or update comments in source code.
- :speech_balloon: Add or update text and literals.
- :loud_sound: Add or update logs.
- :mute: Remove logs.
- :building_construction: Make architectural changes.
- :label: Add or update types.
- :goal_net: Catch errors.
- :tada: Begin a project.
- :see_no_evil: Add or update a .gitignore file.
- :recycle: Refactor code.
- :truck: Rename .md to .md
- :memo: Create .md
- :pencil2: Fix typos
- :construction: Work in progress
- :truck: Move resources
- :fire: Remove A (from B)

등의 아이콘들이 있다.

<br/>

## 커밋 메세지 구조

```html
<type
  >(<scope
    >):
    <subject>
      -- 헤더
      <BLANK LINE>
        -- 빈 줄
        <body>
          -- 본문
          <BLANK LINE>
            -- 빈 줄
            <footer>-- 바닥 글</footer></BLANK
          >
        </body></BLANK
      ></subject
    ></scope
  ></type
>
```

### type

해당 commit의 성격을 나타내며 아래 중 하나여야 한다.

- `feat` 기능 개발 관련
- `fix` 오류 개선 혹은 버그 패치
- `docs` 문서화 작업
- `test` test 관련
- `conf` 환경설정 관련
- `build` 빌드 관련
- `ci` Continuous Integration 관련
- `design` 디자인 변경
- `comment` 주석 수정
- `refactor` 리펙토링 : 결과의 변경 없이 코드의 구조를 재조정함
- `move` 파일, 폴더 경로 수정
- `remove` 파일삭제
- `DB` DB 관련 작업
- `chore` 빌드 업무 수정, 패키지 매니저 수정
- `style` 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우

### body

본문으로 헤더에서 생략한 상세한 내용을 작성한다. 헤더로 충분한 표현이 가능하다면 생략이 가능하다.

### footer

바닥글로 어떤 이슈에서 왔는지와 같은 참조 정보를 추가하는 용도로 사용한다. `"유형: #이슈 번호"` 형식으로 사용하며 여러 개의 이슈 번호를 적을 때는 쉼표(,)로 구분한다.

- `Fixes` 이슈 수정중 (아직 해결되지 않은 경우)
- `Resolves` 이슈를 해결했을 때 사용
- `Ref` 참고할 이슈가 있을 때 사용
- `Related to` 해당 커밋에 관련된 이슈번호 (아직 해결되지 않은 경우)

ex) Fixes: #45 Related to: #34, #23

<br/>

## 커밋 메세지 예시

```
Feat: 관심지역 알림 ON/OFF 기능 추가(#123)

시군구의 알림을 각각 ON/OFF 할 수 있도록 기능을 추가함
 - opnion0055: 구분 코드

해결: close #123
```
