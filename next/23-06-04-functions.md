### 정적 사이트 생성 (SSG)

외부에서 데이터를 가져오지 않는 경우에는 next.js 가 기본적으로 SSG 방식으로 HTML 파일을 그려놓고, 외부에서 데이터를 가져오는 경우, 따로 설정을 해주어야만 빌드할 때 해당 데이터를 가져와서 저장해놓고 HTML 파일을 그린다.

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

### next.js 와 react-query 함께 사용해보기

#### initialData 지정하기

getStaticProps 혹은 getServerSideProps 를 통해서 받아온 데이터를 useQuery 의 initialData 부분에 할당한다.

```tsx
export async function getStaticProps() {
    const posts = await getPosts()
    return { props: { posts } }
}

function Post({ posts }) {
    const { data } = useQuery('posts', getPosts, { initialData: posts })

    return (
        ...
    )
}
```

```tsx
// api/services/Post.js
import axios from "axios";

export const getPosts = async () => {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  return response.data;
};
```

```tsx
// pages/post/index.jsx
import { getPosts } from "@/api/services/Post";
import Link from "next/link";
import React from "react";
import { useQuery } from "react-query";

export async function getStaticProps() {
  // SSG 활용
  const posts = await getPosts(); // 미리 작성한 api 함수 사용
  return { props: { posts } };
}

function Post({ posts }) {
  // 캐싱한 데이터를 사용할 수 있게 staleTime 설정
  const { data } = useQuery("posts", getPosts, {
    initialData: posts,
    staleTime: 10000,
  });

  return (
    <div>
      <Link href="/">홈으로 가기</Link>
      {data.map((post) => (
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

```tsx
// _app.js
import { QueryClient, QueryClientProvider } from "react-query";

const queryClient = new QueryClient();

export default function App({ Component, pageProps }) {
  return (
    <QueryClientProvider client={queryClient}>
      <Component {...pageProps} />
    </QueryClientProvider>
  );
}
```

#### Hydration 활용하기

1. (getStaticProps 등에서) 새로운 QueryClient를 만든다.
2. prefetchQuery를 통해서 미리 요청을 보낸다.
3. 요청에 대한 데이터가 저장되어있는 QueryClient를 dehydrate 처리한다.
4. 해당 QueryClient를 컴포넌트에서 hydrate해서 저장된 캐시를 사용한다.

```tsx
// pages/post/index.jsx
import { getPosts } from "@/api/services/Post";
import Link from "next/link";
import React from "react";
import { dehydrate, QueryClient, useQuery } from "react-query";

export async function getStaticProps() {
  const queryClient = new QueryClient();
  await queryClient.prefetchQuery("posts", getPosts);
  return {
    props: {
      dehydratedState: dehydrate(queryClient),
    },
  };
}

function Post() {
  const { data: posts, isLoading } = useQuery("posts", getPosts);

  if (isLoading) return <div>로딩 중..</div>;
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
