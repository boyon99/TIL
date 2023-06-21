### Image 태그

next.js 의 [image 태그](https://nextjs.org/docs/pages/api-reference/components/image)는 아래와 같은 특징을 가진다.

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

### Font

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
