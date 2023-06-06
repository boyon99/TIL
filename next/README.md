# Next

## next.js란?

서버 사이드 렌더링(SSR), 동적 라우팅 등을 아주 손쉽게 사용할 수 있도록 해주는 강력한 리액트 프레임워크이다.

- **서버 사이드 렌더링** 지원
- 기본적으로 사전 렌더링 지원 (빌드할 때 미리 HTML 을 만들어놓음)
- 서버 사이드 렌더링으로 인한 검색 엔진 최적화 (이미 HTML 이 채워져 있으므로, 검색 엔진이 우리 웹 페이지 정보를 원활하게 수집할 수 있음)
- 동적 라우팅 지원 (react-router-dom 필요없이 그냥 파일을 만드는 것만으로 자동으로 route 가 구성됨)
- 간단한 API 서버 구축 지원
- 이미지, 폰트 최적화 지원
- 기본적으로 타입스크립트 지원
- 코드 분할 지원 (따로 설정하지 않아도, 알아서 번들을 조각내어서 필요한 부분만 전송함)
- 서버 사이드 렌더링 + 사전 렌더링 + 코드 분할로 인한 빠른 로딩

## 렌더링의 방식

### 클라이언트 사이드 렌더링 (CSR)

기본적으로 SPA 는 `클라이언트 사이드 렌더링` 방식으로 구현되고 있다. CSR로 구현된 페이지는 html 만 보았을 때는 요소들이 비워져 있으며 사이트에 사용자가 접속해서, 자바스크립트가 실행되는 순간 요소들이 채워지기 시작한다. 그래서 요소들을 그리는 주체가 클라이언트라는 점에서 클라이언트 사이드 렌더링이라고 말한다.

단점으로는

- 사용자가 첫 화면을 보기까지의 시간이 오래 걸림 (화면을 그리는 자바스크립트가 실행되기 전까지 사용자는 빈 화면을 보아야 함)
- HTML 이 비어있기 때문에, 검색 엔진이 우리 페이지의 정보를 원활하게 수집할 수 없음

### 서버 사이드 렌더링 (SSR)

서버 사이드 렌더링은 말그대로 요소들을 그리는 주체가 `서버`가 되는 것이다.

사용자가 사이트에 접속하는 순간, 서버 (HTML 을 공급하는 서버)는 HTML 에다가 요소들을 그리고, 요소들이 그려진 HTML 파일과 함께 필요한 자바스크립트 코드를 사용자에게 보낸다. 그러면 사용자가 받는 파일은 빈 파일이 아니라, 요소들이 채워져있는 HTML 파일이 된다. 다만 요소들이 그려져 있다고 해서 실제로 사용자와의 인터렉션 (클릭 등) 이 가능한 것은 아니다.

장단점으로는

**장점**

- 페이지 로딩이 빨라짐
- 검색 엔진 최적화 (SEO) 가 가능

**단점**

- 서버가 요소를 그려야 하기 때문에, 서버에 부하가 걸림
- 사용자가 사이트를 본 순간 (Time To View) 과 인터렉션이 가능한 순간 (Time To Interact) 의 차이가 발생함 (요소가 그려지기만 하고, 아직 자바스크립트 코드가 실행되지는 않았기 때문)
- 새로고침 시 페이지를 다시 서버에서 받아와야 하기 때문에, 새로고침 시 화면이 비었다가 채워지는 Blinking Issue 가 발생

### 정적 생성 (Static Site Generation, SSG)

`Next.js` 의 핵심적인 기능 중 하나로 `Static Generation` 이란 특정 페이지의 HTML을 `빌드할 때` 미리 그려놓는 것을 말한다. 즉, 사용자가 사이트에 접속할 때마다 서버가 직접 HTML을 그리는 것이 아니라, 미리 그려놓은 채로 해당 HTML을 저장해놓고, 사용자가 사이트에 접속하면 저장해놓은 HTML을 공급하는 것이다.

**Next.js 는 컴포넌트가 따로 외부에서 데이터를 가져오지 않는 한, 항상 static generation 방식으로 사전 렌더링을 진행한다.** (따로 설정을 해주면, 외부에서 데이터를 가져오더라도 static generation 방식으로 렌더링해줄 수 있다.)

단점으로는

- 빌드 시간이 오래 걸릴 수 있음
- 오래된 데이터를 미리 그려놓는 경우, 유저가 옛날 데이터를 보는 상황이 발생할 수 있음

> next.js 앱을 yarn dev 로 실행한 경우에는 SSG 로 구현해놓은 코드라도 SSR 과 동일한 방식으로 작동한다. (아직 미리 빌드하지 않았기 때문)

<br/>

## next.js 기본 기능

### pages 폴더를 통한 라우팅

next.js 는 pages 폴더 안에 파일 혹은 폴더를 만드는 것만으로 해당 파일 이름으로 route 가 구성되며, id 번호 등에 맞추어 페이지를 보여줘야 하는 경우의 동적 라우팅도 지원한다.

- `pages/index.jsx` 라고 하면 해당 파일이 ‘/’ 주소에 연결
- `pages/post.jsx` 라고 하면 해당 파일이 ‘/post’ 주소에 연결
- `pages/post/index.jsx` 라고 하면 해당 파일이 ‘/post’ 주소에 연결
- `pages/post/first.jsx` 라고 하면 해당 파일이 ‘/post/first’ 주소에 연결
- `pages/post/[id].jsx` 라고 하면 해당 파일이 ‘/post/1’, ‘/post/2’ 등의 동적 주소에 연결 (useRouter 를 사용해서 해당 id 를 가져올 수 있다.)

```js
// post/[id].jsx
import { useRouter } from "next/router";
import React from "react";

function PostDetail() {
  const router = useRouter();
  const { id } = router.query;

  return <div>PostDetail {id}</div>;
}

export default PostDetail;
```

- `pages/post/[…params].jsx` 라고 하면 해당 파일이 ‘/post/_/_/\*’ 등의 동적 주소에 연결 (route 의 깊이를 무한하게 지정할 수 있다. 단, ‘/post/1’ 로 접근할 경우 위 [id].jsx를 우선한다.)

### Link 태그와 query 객체 (useRouter)

페이지 이동시에 Link 태그를 활용한다.

```jsx
// 정적 라우팅인 경우
<Link href={{ pathname: "/post", query: { name: "hello" } }}>
  name과 함께 post로 가기
</Link>

// 동적라우팅인 경우
<Link href={{ pathname: '/post/[id]', query: { id: 1, name: 'hello' } }}>
    name과 함께 1번 post로 가기
</Link>
```

```jsx
import { useRouter } from "next/router";

const router = useRouter();
// 정적 라우팅인 경우
const { name } = router.query;
// 동적 라우팅인 경우
const { id, name } = router.query;
```

다중 경로인 경우

```jsx
<Link href="/post/1/2/3">다중 경로인 경우</Link>
```

```jsx
import { useRouter } from "next/router";
import React from "react";

function PostParams() {
  const router = useRouter();
  console.log(router.query);

  return <div>PostParams</div>;
}

export default PostParams;
```

<img src="https://mango-tower-9f1.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F81de7d2a-bdb6-4b4b-84b5-4f64f5290c42%2FScreenshot_2023-02-20_at_9.57.51_PM.png?id=3ef593b9-1d40-4df5-ac33-666c1e36b5f0&table=block&spaceId=3e16dc82-3f48-4560-82ef-93bb527f3234&width=860&userId=&cache=v2" width="200px"/>

배열 형태로 저장되는 것을 확인할 수 있다.

버튼을 통해서 이동하고 싶은 경우 `router.push()`를 이용할 수 있다.

```jsx
import { useRouter } from "next/router";
import React, { useEffect } from "react";

function Post() {
  const router = useRouter();

  return (
    <div>
      <button onClick={() => router.push("/post/1")}>1번 글로가기</button>
      {/*또는*/}
      <button
        onClick={() =>
          router.push({ pathname: "/post/[id]", query: { id: 1 } })
        }
      >
        1번 글로가기
      </button>
    </div>
  );
}

export default Post;
```

### 스타일 적용하기

next.js 는 기본적으로 css, css modules, 인라인 css (css-in-js), styled-jsx 를 모두 지원한다.

### Image 태그

next.js 의 image 태그는 아래와 같은 특징을 가진다.

- **직접 리사이징 해줄 필요없이 자동으로 뷰포트에 맞춰춤**
- **해당 뷰포트에 진입할 때만 이미지를 로딩**
- **레이아웃 이동을 최소화 (Cumulative Layout Shift 방지)**
- **디바이스 종류에 따라 이미지 파일 크기를 조절해서 공급**

```jsx
import Image from "next/image";

<Image
  src="/images/profile.jpg" // 이미지 주소, 경로
  height={144} // CLS 방지를 위해 사용됨
  width={144} // CLS 방지를 위해 사용됨
  alt="Your Name"
/>;
```

핵심적인 요소인 경우 priority 옵션을 통해 다른 요소들에 비해 먼저 로딩해올 수 있다.

```jsx
<Image src={dogImage} alt="dog" priority />
```

fill을 통해 이미지 크기를 모르는 경우 부모 태그에 맞추도록 설정할 수 있다.

```jsx
// 부모 요소가 position: relative 및 display: block 속성을 가지고 있어야 함
<Image src={dogImage} alt="dog" fill />
```

sizes를 통해 디바이스 크기 별 이미지를 지정할 수 있다.

```jsx
<Image src={dogImage} alt="dog" fill sizes="(max-width: 768px) 33vw, (max-width: 1200px) 50vw, 100vw"/>7
```

이미지를 외부에서 가져오는 경우 next.config.js 설정을 해야 한다.

```jsx
images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'via.placeholder.com', // 전부 허용하고자 할 경우에는 **
        port: '',
        pathname: '**', // 전부 허용하고자 할 경우에는 **
      },
    ],
  },
```

### Font 설정하기

`_app.js`에 다음과 같이 작성한다. 이런 경우 컴포넌트 전체의 폰트가 적용된다.

```jsx
import { Black_Han_Sans } from "next/font/google";

const blackHanSans = Black_Han_Sans({
  weight: "400",
  preload: false, // 한글 폰트라면 필요 (정확히는 한글 subset 을 지원하지 않아서 필요)
});

export default function App({ Component, pageProps }) {
  return (
    <main className={blackHanSans.className}>
      <Component {...pageProps} />
    </main>
  );
}
```

### Head 태그와 Script 태그

Head 태그를 통해서 각 페이지 별 Head 태그를 설정해줄 있다.

`Head 태그`를 작성하면, 브라우저에 글 있는 곳 라는 타이틀이 표시되며,

```jsx
import React from "react";
import * as S from "@/styles/post";
import Head from "next/head";

function Post() {
  return (
    <>
      <Head>
        <title>글 있는 곳</title>
      </Head>
      <S.Container>
        <p>폰트가 적용됐나요?</p>
      </S.Container>
    </>
  );
}

export default Post;
```

`Script 태그`를 사용하면, 외부 스크립트를 효율적으로 가져올 수 있다.

```js
import React from "react";
import * as S from "@/styles/post";
import Script from "next/script";

function Post() {
  return (
    <>
      <Script src="https://example.com/script.js" />
      <S.Container>
        <p>폰트가 적용됐나요?</p>
      </S.Container>
    </>
  );
}

export default Post;
```

### Layout Component 활용 (내브, 푸터 설정 등)

```jsx
// components/Layout.jsx
import React from "react";

function Layout({ children }) {
  return (
    <>
      <nav>내브바</nav>
      <main>{children}</main>
      <footer>푸터</footer>
    </>
  );
}

export default Layout;
```

```jsx
// _app.js
import Layout from "@/components/Layout";

export default function App({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  );
}
```

<br/>

## next.js 심화 기능

### 정적 사이트 생성 (SSG)

외부에서 데이터를 가져오지 않는 경우에는 next.js 가 **기본적으로** SSG 방식으로 HTML 파일을 그려놓고, 외부에서 데이터를 가져오는 경우, **따로 설정을 해주어야만** 빌드할 때 해당 데이터를 가져와서 저장해놓고 HTML 파일을 그린다.

#### getStaticProps 사용하기

```jsx
export async function getStaticProps() {
    요청을 보내고 데이터 받아오기
    return { props: { 데이터 } }
}

function 페이지컴포넌트({ 데이터 }) {
    return (
        <div>
        </div>
    )
}
```

```jsx
import axios from "axios";
import Link from "next/link";
import React from "react";

export async function getStaticProps() {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  const posts = response.data;
  return { props: { posts } };
}

function Post({ posts }) {
  return (
    <div>
      <Link href="/">홈으로 가기</Link>
      {posts.map((post) => (
        <div key={post.id}>
          <h1>{post.title}</h1>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
}

export default Post;
```

#### getStaticPaths 사용하기

유저가 접근 가능한 동적 라우트 주소가 무엇이 있는지를 지정해주는 함수이다.

```jsx
// post/[id].jsx
import axios from "axios";
import React from "react";

export async function getStaticPaths() {
  const response = await axios.get(
    `https://jsonplaceholder.typicode.com/posts`
  );
  const posts = response.data;
  const paths = posts.map((post) => ({ params: { id: `${post.id}` } }));
  return { paths, fallback: false };
}

// getStaticPaths 에서 리턴한 paths 내부 값을 인자 형태로 받아올 수 있음
export async function getStaticProps({ params }) {
  const response = await axios.get(
    `https://jsonplaceholder.typicode.com/posts/${params.id}`
  );
  const post = response.data;
  return { props: { post } };
}

function PostDetail({ post }) {
  return (
    <div>
      <h5>{post.id}</h5>
      <h4>{post.title}</h4>
      <p>{post.body}</p>
    </div>
  );
}

export default PostDetail;
```

> 빌드할 때 1번 게시글부터 100번 게시글 모두에 요청을 보내고 데이터를 저장해둔다. 다만 정적 사이트 생성 방식은 데이터를 미리 받아서 저장해놓기 때문에, 예전 데이터를 보여줄 가능성이 있다. 만약 지속적으로 데이터가 업데이트되는 경우라면 서버 사이드 렌더링을 사용하되, 그 외의 경우에는 SSG 를 사용하시는 것을 추천한다.

> yarn dev 로 실행한 경우에는 SSG 로 구현해놓은 코드라도 SSR 과 동일한 방식으로 작동한다.

`fallback`은 다음과 같은 옵션이 있다.

- false : 미리 데이터를 받아놓은 path 가 아니라면 404 페이지로 이동
  → 데이터가 한정된 경우 이 방식을 사용
- true : 미리 데이터를 받아놓은 path 가 아니라면 요청 시 해당 path 에 대한 HTML 과 JSON 데이터를 정적으로 생성하면서, 로딩을 보여줌 (한번 생성하면 캐싱됨)
  → 데이터가 너무 많은 경우 이 방식을 사용
- blocking : 미리 데이터를 받아놓은 path 가 아니라면 요청 시 해당 path 에 대한 HTML 과 JSON 데이터를 정적으로 생성하면서, 로딩을 보여주지 않음 (로딩이 완료되어야 페이지를 보여줌, 한번 생성하면 캐싱됨)

로딩 시 페이지는 다음과 같이 작성할 수 있다.

```jsx
const router = useRouter();

if (router.isFallback) {
  return <div>로딩 중..</div>;
}
```

### SSG 의 단점 해결하기 (ISR)

ISR (Incremental Static Regeneration) 란 일정한 주기를 정해두고, 해당 주기마다 다시 데이터를 가져와서 정적 사이트에 그려놓는 방식을 의미한다. 사용하기 위해서는 getStaticProps 에 revalidate 를 명시한다.

```jsx
import axios from "axios";
import Link from "next/link";
import React from "react";

export async function getStaticProps() {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  const posts = response.data;
  return { props: { posts }, revalidate: 10 };
}

function Post({ posts }) {
  return (
    <div>
      <Link href="/">홈으로 가기</Link>
      {posts.map((post) => (
        <div key={post.id}>
          <Link href={`/post/${post.id}`}>
            <h1>{post.title}</h1>
          </Link>
        </div>
      ))}
    </div>
  );
}

export default Post;
```

revalidate: 10 이라고 명시하면, 정적 사이트가 생성되고 10초 동안 저장해놓은 데이터를 사용하게 된다.

### 서버 사이드 렌더링 구현 (SSR)

서버 사이드 렌더링은 getServerSideProps 함수를 사용하며 사용 방식은 SSG 와 동일하다. 함수 이름만 `getServerSideProps`로 작성한다.

```jsx
import axios from "axios";
import Link from "next/link";
import React from "react";

export async function getServerSideProps() {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  const posts = response.data;
  return { props: { posts } };
}

function Post({ posts }) {
  return (
    <div>
      <Link href="/">홈으로 가기</Link>
      {posts.map((post) => (
        <div key={post.id}>
          <Link href={`/post/${post.id}`}>
            <h1>{post.title}</h1>
          </Link>
        </div>
      ))}
    </div>
  );
}

export default Post;
```

<br/>

## next.js 와 react-query 함께 사용해보기
