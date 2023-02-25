# typescript
- [TS 공식문서](https://www.typescriptlang.org/ko/)
- [REPL](https://www.typescriptlang.org/play?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCbvCwDKgU8JkY7p7ehCTkVDQS2E6gnPCxGcwmZqDSTgzxxWWVoASMFmgYkAAeRJTInN3ymj4d-jSCeNsMq-wuoPaOltigAKoASgAywhK7SbGQZIIz5VWCFzSeCrZagNYbChbHaxUDcCjJZLfSDbExIAgUdxkUBIursJzCFJtXydajBBCcQQ0MwAUVWDEQC0gADVHBQGNJ3KAALygABEAAkYNAMOB4GRonzFBTBPB3AERcwABS0+mM9ysygc9wASmCKhwzQ8ZC8iHFzmB7BoXzcZmY7AYzEg-Fg0HUiQ58D0Ii8fLpDKZgj5SWxfPADlQAHJhAA5SASPlBFQAeS+ZHegmdWkgR1QjgUrmkeFATjNOmGWH0KAQiGhwkuNok4uiIgMHGxCyYrA4PCCJSAA)
   - 작성한 내용이 컴파일러 옵션에 따라 어떻게 자바스크립트로 변환되는지 바로 확인할 수 있다.
- [Repl.it](https://replit.com/languages/typescript)
  - 파일과 디렉터리로 관리되는 타입스크립트 프로젝트를 손쉽게 구성할 수 있다. 
  - 간단한 프로젝트로 타입스크립트를 테스트하기 좋다.


### 설치하기
- 전역 설치하기
`npm i typescript -g`
> mac에서 전역으로 설치할 때의 오류 : 맨 앞에 sudo를 붙인 후 암호를 입력한다. 전역으로 설치하는 이유는 명령어를 사용하기 위함이다. (ts의 경우 tsc의 명령어)
- 단일 프로젝트에서만 사용하기 
`npm install -D typescript`
> 이런 경우 명령어를 사용하기 위해서는 `npx tsc`명령어를 입력해야 한다.


### 컴파일을 위한 다양한 옵션
1. 직접 작성하기
```console
tsc [파일이름].ts
tsc ./src/index.ts --watch --strict true --target ES6 --lib ES2015,DOM --module CommonJS
```

2. `tsconfig.json` 파일로 옵션을 관리할 수 있다. 
  - "include"와 "exclude" 옵션을 같이 추가해, 컴파일에 포함할 경로와 제외할 경로를 설정할 수 있다.
  - `tsc --init`로 초기화하면 `tsconfig.json` 파일이 추가된다.

```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES6",
    "lib": ["ES2015", "DOM"],
    "module": "CommonJS"
  },
  "include": [
    "src/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```
```console
tsc --watch // 변경사항이 자동으로 실행
```


### Parcel
`npm install -D typescript parcel-bundler`



`npm i ts-node -g` : ES5로 변환한 후 실행해주는 패키지





