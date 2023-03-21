# Version_Control_System

[커맨드 라인 인터페이스 방식(Command Line Interface, CLI)을 통한 깃 활용 실습](https://github.com/boyon99/Version_Control_Sysyem_1)

# GIT

`git` 입력시 다음과 같은 내용을 확인할 수 있다.

```
다음은 여러가지 상황에서 자주 사용하는 깃 명령입니다:

작업 공간 시작 (참고: git help tutorial)
   clone     저장소를 복제해 새 디렉터리로 가져옵니다
   init      빈 깃 저장소를 만들거나 기존 저장소를 다시 초기화합니다

변경 사항에 대한 작업 (참고: git help everyday)
   add       파일 내용을 인덱스에 추가합니다
   mv        파일, 디렉터리, 심볼릭 링크를 옮기거나 이름을 바꿉니다
   restore   Restore working tree files
   rm        파일을 작업 폴더에서 제거하고 인덱스에서도 제거합니다

커밋 내역과 상태 보기 (참고: git help revisions)
   bisect    이진 탐색으로 버그를 만들어낸 커밋을 찾습니다
   diff      커밋과 커밋 사이, 커밋과 작업 내용 사이 등의 바뀐 점을 봅니다
   grep      패턴과 일치하는 줄을 표시합니다
   log       커밋 기록을 표시합니다
   show      여러가지 종류의 오브젝트를 표시합니다
   status    작업 폴더 상태를 표시합니다

커밋 내역을 키우고, 표시하고, 조작하기
   branch    브랜치를 만들거나, 삭제하거나, 목록을 출력합니다
   commit    바뀐 사항을 저장소에 기록합니다
   merge     여러 개의 개발 내역을 하나로 합칩니다
   rebase    커밋을 다른 베이스 끝의 최상위에서 적용합니다
   reset     현재 HEAD를 지정한 상태로 재설정화합니다
   switch    Switch branches
   tag       태그를 만들거나, 표시하거나, 삭제하거나, GPG 서명을 검증합니다

협동 작업 (참고: git help workflows)
   fetch     다른 저장소에서 오브젝트와 레퍼런스를 다운로드합니다
   pull      다른 저장소 또는 다른 로컬 브랜치에서 가져오거나 통합합니다
   push      원격 레퍼런스 및 그와 관련된 오브젝트를 업데이트합니다
```

<br/>

## 깃 환경 설정하기

`git config` 명령을 통해 사용자 정보를 설정할 수 있다. `--global` 옵션 추가 시 현재 컴퓨터에 있는 모든 저장소에서 같은 사용자 정보를 사용하도록 설정하며 `git config --list` 로 설정을 확인하고 `vi ~/.gitconfig`을 통해 수정할 수 있다.

```console
$ git config --global user.name ""
$ git config --global user.email ""
$ git config --global core.editor "vim"
$ git config --global core.pager "cat"
```

<br/>

## 깃 시작하기

폴더 생성 후 `git init`하여 깃을 세팅한다.

### 버전 만들기

- `git add [파일명]` : 파일이 스테이징된다.
  - `git add .` : 변경된 모든 파일을 스테이징한다.
- `git commit` : 파일이 local repo로 넘긴다.
  - `git commit -m “[커밋메세지]”` : 커밋메세지를 단축해서 사용한다.
  - `git commit -am "[커밋메세지]"` : `git add`와 커밋메세지를 단축해서 사용한다.
  - `git commit --amend`로 커밋 메세지를 수정한다.
- `git push` : remote repo로 파일을 올린다.
  - `git push [저장소이름] [브랜치명]`을 통해 해당 저장소에 해당 브랜치의 내용을 올린다.
- `git pull` : 원격저장소의 내용을 지역저장소로 가져온다.
  - `git pull [저장소이름] [브랜치명]`을 통해 해당 저장소의 내용을 해당 브랜치에 가져온다.

<br/>

### 깃 상태 확인하기

- `git status` : 현재의 깃 상태를 확인한다.
- `git log` : 저장소에 저장된 버전을 확인할 수 있다.
  - `git log --stat` : 커밋에 관한 파일까지 함께 확인할 수 있다.
  - `git log --oneline` : 커밋에 관한 내용을 간략하게 확인할 수 있다.
  - `git log --oneline --branches` : 브랜치 정보를 같이 확인할 수 있다.
  - `git log --oneline --branches --graph` : 그래프 형태로 브랜치와 커밋의 관계를 더 쉽게 확인할 수 있다.
  - `git log [브랜치명]..[브랜치명]` : 두 브랜치의 차이를 알 수 있다.
- `git diff` : 변경 사항을 확인할 수 있다.

<br/>

### tracked 파일과 untracked 파일

- tracked : 한 번이라도 커밋한 파일의 경우 수정 시 내용을 바로 추적한다.
  - `git stash` : 수정중인 파일 감추기
  - `git stash pop` : 감춘 파일 원상복귀하기
- untracked : 한 번도 깃에서 버전 관리를 하지 않았기 때문에 수정 내역을 추적하지 않는다.

<br/>

### 취소하기

- `git checkout -- "file name"` : 수정한 내용을 취소한다. (tracked된 파일 중 수정하고 있는 사항을 취소한다.)
- `git reset HEAD "file name"` : 스테이징 되어 있는 내용을 취소한다.
- `git reset HEAD^` : 가장 마지막에 한 커밋을 취소한다.
  - `git reset --hard "복사한 커밋해시"` : `git log`를 통해 이동할 커밋해시를 선택한 후 명령어를 입력하면 해당 커밋이 가장 최신 커밋으로 변경된다.
- `git revert "복사한 커밋해시"` : 커밋을 되돌리되 삭제하지 않고 보관한다.

<br/>

### 브랜치

- `git branch` : 브랜치를 확인할 수 있다.
- `git branch [브랜치명]` : 브랜치를 생성한다.
- `git checkout [브랜치명] || git switch [브랜치명]` : 해당 브랜치로 이동한다.
- `git merge [브랜치명]` : 현재 checkout되어 있는 브랜치에 해당 브랜치를 병합한다.
- `git branch -d [브랜치명]` : 저장소에서 브랜치를 삭제하는 것이 아니라 로컬에서 해당 브랜치 내역을 삭제한다.

<br/>

### 원격

- `git remote add [저장소이름] [깃허브주소]` : 연결할 깃허브 주소와 저장소 이름을 설정한다.
  - `git remote -v` : 원격저장소를 확인한다.
- `git clone [깃허브주소]` : 원격저장소를 복제하여 지역저장소로 가져온다.
- `git fetch` : 커밋을 가져와 합치는 풀 명령과 다르게 원격 브랜치에 어떤 변화가 있는지 그 정보만 가져온다.
