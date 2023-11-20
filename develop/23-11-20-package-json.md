# package.json 이란?

package.json이란 현재 프로젝트에 관한 정보와 패키지 매니저(npm, yarn)을 통해 설치한 모듈들의 의존성을 관리하는 파일이다.

## 생성방법

```shell
npm init // 프로젝트명, 설명 등 작성할 내용이 있을 경우
npm init -y // 입력할 내용 없이 생성할 경우

yarn init
yarn init -y
```

## package.json의 기본 정보

기본 정보란 package.json을 자동으로 생성할 때(npm init), -y를 명령어를 붙이지 않은 경우 입력하게 되는 것들을 나타낸다.

name, version, description, author, license 등을 입력할 수 있는데, 프로젝트에 대한 간략한 내용을 입력할 수 있다. 처음 생성할 때 입력하지 않은 경우에 추후에 package.json을 변경하여 입력할 수 있다.

## 버전 관리

의존성 모듈을 설치하게 되면 dependencies안에 해당 모듈의 버전과 이름이 추가된다.

## 의존성 모듈 설치

```shell
npm install
yarn add
```

## dependencies와 devDependencies

#### dependencies

dependencies는 프로덕션 환경에서 실행에 필요한 패키지들을 정의한다. 이 패키지들은 실제 서비스가 동작할 때 필요한 모듈들로, 애플리케이션의 핵심 기능에 관련된 것들이 포함된다.

```shell
npm install -
```

#### devDependencies

devDependencies는 개발 및 테스트 목적으로만 필요한 패키지들을 정의한다. 이 패키지들은 주로 테스트 프레임워크, 빌드 도구, 코드 스타일 검사 도구 등이며, 프로덕션 환경에서는 필요하지 않다.

```shell
npm install - --save-dev
npm install - -D
```

=> 프로덕션 환경에서는 최소한의 필요한 패키지만 설치되게 하고, 개발 및 테스트 환경에서는 편리하게 필요한 패키지들을 설치할 수 있도록 도와준다.

## 유의적 버전

유의적 버전이란 의미가 있는 버전으로 버전마다 의미를 부여하여 나타내는 약속된 규칙같은 것을 말한다.

<br/>

### Major.Miner.Patch

`^8.31.0`

- **Major** - 기존 버전과 호환되지 않는 새로운 버전
- **Miner** - 기존 버전과 호환되는 새로운 기능이 추가된 버전
- **Patch** - 기존 버전과 호환되는 버그 및 오타 등이 수정된 버전
- **^** - 메이저 버전 안에서 가장 최신 버전으로 업데이트 가능 여부를 의미
- **~** - 마이너 버전이 명시되어 있을 경우 패치버전만 변경하여 버전을 적용함

<br/>

### 모듈 정보 확인하기

`package info module`로 해당 모듈의 정보를 알아볼 수 있다.
