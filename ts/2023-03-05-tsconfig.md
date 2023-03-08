# 타입스크립트 구성

`tsconfig.json` 파일을 사용해 타입스크립트 컴파일러가 프로젝트를 JS로 변환하는 방법을 지정

```json
{
  "compilerOptions": {},
  "files": ["node_modules/my-library/index.ts"],
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"],
  "extends": "config/base.json"
}
```

| 옵션    | 우선순위 | 설명                                                                                                              |
| ------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| files   | 1        | 컴파일할 개별 파일 목록 (확장자 필수)                                                                             |
| exclude | 2        | 컴파일에서 제외할 파일 경로 목록                                                                                  |
| include | 3        | 컴파일할 파일 경로 목록<br/>- `.ts` `.tsx` `.d.ts` 확장자 생략 가능하나 `allowJS: true`인 경우 `.js`, `.jsx` 추가 |
| extends | -        | 상속할 다른 TS 구성                                                                                               |

<br/>

## CompilerOptions

```json
{
  "compilerOptions": {
    "target": "es5", // 'es3', 'es5', 'es2015', 'es2016', 'es2017','es2018', 'esnext' 가능
    "module": "commonjs", //무슨 import 문법 쓸건지 'commonjs', 'amd', 'es2015', 'esnext'
    "allowJs": true, // js 파일들 ts에서 import해서 쓸 수 있는지
    "checkJs": true, // 일반 js 파일에서도 에러체크 여부
    "jsx": "preserve", // tsx 파일을 jsx로 어떻게 컴파일할 것인지 'preserve', 'react-native', 'react'
    "declaration": true, //컴파일시 .d.ts 파일도 자동으로 함께생성 (현재쓰는 모든 타입이 정의된 파일)
    "outFile": "./", //모든 ts파일을 js파일 하나로 컴파일해줌 (module이 none, amd, system일 때만 가능)
    "outDir": "./", //js파일 아웃풋 경로바꾸기
    "rootDir": "./", //루트경로 바꾸기 (js 파일 아웃풋 경로에 영향줌)
    "removeComments": true, //컴파일시 주석제거

    "strict": true, //strict 관련, noimplicit 어쩌구 관련 모드 전부 켜기
    "noImplicitAny": true, //any타입 금지 여부
    "strictNullChecks": true, //null, undefined 타입에 이상한 짓 할시 에러내기
    "strictFunctionTypes": true, //함수파라미터 타입체크 강하게
    "strictPropertyInitialization": true, //class constructor 작성시 타입체크 강하게
    "noImplicitThis": true, //this 키워드가 any 타입일 경우 에러내기
    "alwaysStrict": true, //자바스크립트 "use strict" 모드 켜기

    "noUnusedLocals": true, //쓰지않는 지역변수 있으면 에러내기
    "noUnusedParameters": true, //쓰지않는 파라미터 있으면 에러내기
    "noImplicitReturns": true, //함수에서 return 빼먹으면 에러내기
    "noFallthroughCasesInSwitch": true //switch문 이상하면 에러내기
  }
}
```

| 옵션                         | 기본값                      | 설명                                                                       | 허용 값 예시                           |
| ---------------------------- | --------------------------- | -------------------------------------------------------------------------- | -------------------------------------- |
| target                       | `"ES3"`                     | 컴파일될 ES(JS) 버전 명시, `"ES2015"`(ES6)를 권장(대부분의 브라우저 지원)  | `"ES3"` `"ES5"` `"ES2015"` `"ESNext"`  |
| lib                          | -                           | 컴파일에서 사용할 라이브러리 지정                                          | `"ESNext"` `"DOM"`                     |
| module                       | `"CommonJS"`                | 모듈 시스템 지정                                                           | `"CommonJS"` `"AMD"` `"ESNext"`        |
| moduleResolution             | `"Node"`                    | 모듈 해석 방식 지정                                                        | `"Classic"` `"Node"`                   |
| esModuleInterop              | `false`                     | ESM 모듈 방식 호환성 활성화                                                |
| isolatedModules              | `false`                     | 모든 파일을 모듈로 컴파일, `import` 혹은 `export`가 없는 경우 에러         |
| allowSyntheticDefaultImports | `true`                      | 기본 내보내기(`export default`)가 없는 모듈에서 기본 가져오기 가능         |
| baseUrl                      | -                           | 모듈 해석에 사용할 기준 경로 지정                                          | `"./"` `"./project/"`                  |
| paths                        | -                           | 모듈 해석에 사용할 경로 별칭 지정                                          | `{"~/*": ["./src/*"]}`                 |
| types                        | -                           | 컴파일러가 참조할 @types 패키지의 목록을 지정, 명시되지 않으면 무시        | `["lodash", "node", "jest"]`           |
| typeRoots                    | `["./node_modules/@types"]` | 컴파일러가 참조할 타입 선언(d.ts)의 경로 목록을 지정, 명시되지 않으면 무시 | `["./types", "./node_modules/@types"]` |
| allowJs                      | `false`                     | JS 파일 컴파일 허용                                                        |
| checkJs                      | `false`                     | `.js` 파일의 오류 보고 여부, `allowJs`가 `true`일 때만 유효                |
| jsx                          | `"preserve"`                | JSX 지정                                                                   | `"preserve"` `"react"`                 |
| declaration                  | `true`                      | 모든 TS(JS) 파일의의 d.ts 파일 생성 여부                                   |
| sourceMap                    | `false`                     | 소스맵 파일 생성 여부, 디버깅 도구 등에서 JS 파일의 원본 TS 파일 표시 가능 |
| strict                       | `false`                     | 더 엄격한 타입 검사 활성화                                                 |
| noImplicitAny                | `false`                     | 암시적 `any` 타입 검사 활성화                                              |
| noImplicitThis               | `false`                     | 암시적 `this` 타입 검사 활성화                                             |
| strictNullChecks             | `false`                     | 엄격한 `null`, `undefined` 타입 검사 활성화                                |
| strictFunctionTypes          | `false`                     | 엄격한 함수의 매개변수 타입 검사 활성화                                    |
| strictPropertyInitialization | `false`                     | 엄격한 클래스의 속성 초기화 검사 활성화                                    |
| strictBindCallApply          | `false`                     | 엄격한 Bind, Call, Apply 메소드의 인수 검사 활성화                         |
