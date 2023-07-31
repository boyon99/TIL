## GitHub Actions를 통한 배포 파이프라인 구축하기

GitHub Actions를 통한 배포 파이프라인을 구축하는 이유는 다음과 같다.

- 자동화된 배포
- 일관성 유지
- 확장성과 유연성
- 협업 강화

## GitHub Actions를 통한 배포 파이프라인을 구축하는 방법

1. GitHub 저장소에서 .github/workflows 디렉토리를 생성
2. .github/workflows 디렉토리 안에 배포 작업을 정의할 main.yml 파일을 만든다.
3. main.yml 파일 안에 다음과 같은 내용을 작성한다.

```yaml
name: CI/CD Pipeline

on:
push:
branches: - main # 배포할 브랜치를 지정 (예: main 브랜치)

jobs:
build:
runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'   # Node.js 버전 지정

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test

deploy:
needs: build
runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Build application
      run: npm run build   # 프로덕션용 빌드 스크립트를 지정

    - name: Deploy to server   # 여기에서 실제 배포 스크립트를 실행
      run: |
        # 여기에 실제로 서버에 배포하는 스크립트를 작성
```

GitHub Actions를 사용하여 CI/CD 파이프라인을 구축하면, 코드 변경이 발생하면 자동으로 빌드, 테스트, 배포가 이루어져 소프트웨어 개발과 배포를 더 효율적으로 관리할 수 있다.
