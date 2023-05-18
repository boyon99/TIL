# react-query

`react-query` 는 서버 데이터 요청/관리를 위한 라이브러리이다.

- 서버 데이터 캐싱
- 데이터가 오래되면 (fresh 상태가 아니라면) 자동으로 다시 요청
- 한번 GET 해온 데이터에 대해서, POST/PUT 등으로 인해 데이터가 업데이트가 되면 자동으로 다시 요청
- 동일한 데이터를 여러 번 요청할 경우 한번만 요청함 (중복 요청 방지)
- 해당 화면에 focus 할 경우 자동으로 데이터를 다시 요청함
- 요청 실패 시 자동으로 다시 요청

## 세팅하기

`QueryClientProvider`로 컴포넌트를 감싼다. 이를 통해 내부 컴포넌트에서 React-query 관련 함수들과 context api처럼 전역에서 캐싱된 쿼리 데이터를 사용할 수 있다.

```js
import { QueryClient, QueryClientProvider } from "react-query";
import { ReactQueryDevtools } from "react-query/devtools";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/*자동으로 devtools 창이 표시된다.*/}
      <ReactQueryDevtools initialIsOpen={true} />
      <컴포넌트 />
    </QueryClientProvider>
  );
}

export default App;
```

## useQuery

`useQuery`를 통해 값을 받아오며 data, inLoading, error 값을 전달받을 수 있다.

```js
  const { isLoading, data, error } = useQuery(쿼리 키값, axios 요청보내는 함수, {쿼리 옵션})
```

```jsx
const getPosts = async () => {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  return response.data;
};
const { isLoading, data: posts, error } = useQuery("posts", getPosts);
```

### 쿼리 키

쿼리 키 값은 해당 요청에 대한 응답 데이터에 이름을 붙이는 것으로 해당 쿼리 키값 명시 시, 아래 코드를 통해서 해당 응답 데이터를 어디서든 가져와서 사용할 수 있다.

```js
const queryClient = useQueryClient();
const data = queryClient.getQueryData(queryKey);
```

쿼리 키 값은 일정한 컨벤션에 맞춰서 배열형태로 적는 것이 좋다.

```jsx
{
  ['todos', 'list', { filters: 'all' }],
  ['todos', 'list', { filters: 'done' }],
  ['todos', 'detail', 1],
  ['todos', 'detail', 2],
  ['todos', 1],
  ['todos', 2],
}
```

### 쿼리 함수

axios 요청 보내는 함수를 의미한다.

```jsx
const getPosts = async () => {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts"
  );
  return response.data;
};
```

### 반환값

함수 실행 시 다음과 같은 값들을 반환한다.

- isLoading : 로딩 중인지 여부 (처음 요청을 하는 경우)
- isFetching : 로딩 중인지 여부 (첫 요청 이후에 refetch 를 하는 경우)
- isError : 에러 여부
- isSuccess : 요청 성공 여부
- error : 에러 객체
- status : 현재 상태 (loading, error, success 가 있다)
- data : 응답 데이터
- refetch : 다시 요청을 하기 위한 함수 (이 함수를 실행하면 해당 요청을 다시 보낼 수 있음)

### 쿼리 옵션

#### staleTime

재요청을 보내지 않아도 되는 데이터 상태 (아직 오래되지 않은 상태)를 `fresh 상태`, 다시 재요청을 보내야 하는 데이터 상태 (오래된 상태)를 `stale 상태`라고 한다. 쿼리 옵션에서 staleTime 을 지정하면, fresh 상태로 유지되는 시간을 지정할 수 있다.

```jsx
// staleTime을 10초로 설정, 10초가 지난 후에만 재요청 보냄
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { staleTime: 10000 });
```

#### cacheTime

쿼리 요청을 보낸 페이지를 보다가, 다른 페이지를 보게 될 경우 처음의 쿼리는 `inactive 상태`(응답 데이터가 있지만 표시는 하지 않고 있는 상태)이다. 이 순간부터 얼마동안 데이터를 보관하고 있을 지 선택하는 것이 바로 cacheTime이다.

```js
// cacheTime을 10초로 설정, 다른 페이지로 전환되어도 10초각은 inactive 상태로 남아있음.
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { cacheTime: 10000 });
```

#### refetchOnWindowFocus

해당 윈도우에 focus 했을 때 다시 요청을 보낼 지 설정한다. 기본값은 true이며, 항상 윈도우에 focus 할 때마다 요청을 다시 보낸다. (stale 상태일 때만)

```js
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { refetchOnWindowFocus: false });
```

#### retry

실패한 쿼리에 대해서 재요청 횟수를 지정할 수 있다. 값을 true인 경우 실패한 쿼리에 대해서 무한 재요청, 숫자로 놓으면 해당 횟수만큼 재요청한다.

```js
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { retry: 3 });
```

#### refetch

다시 요청을 보내기 위한 함수이다.

```js
const {
  isLoading,
  data: posts,
  error,
  refetch,
} = useQuery("posts", getPosts, {});
```

#### enabled

해당 쿼리 요청을 활성화할지 여부를 정하기 위한 옵션으로 enabled 우측에 명시한 값이 true 가 되면 쿼리 요청을 보내고, false인 경우 보내지 않는다. enabled 는 특정한 동작이 완료된 후에 요청을 보내고자 할 때 많이 사용한다.

```js
const [isPrepared, setIsPrepared] = useState(false);
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { enabled: isPrepared });

return <button onClick={() => setIsPrepared(true)}>요청보내기</button>;
```

### 요청 후 처리

react-query 에서는 요청의 성공, 실패 등의 여부에 따라서 특정한 코드를 실행하도록 설정할 수 있다.

#### onSuccess (요청 성공 시 실행)

```jsx
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, {
  onSuccess: (data) => {
    console.log("데이터 요청 성공", data);
  },
});
```

#### onError (요청 실패 시 실행)

```jsx
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, {
  onError: (error) => {
    console.log("데이터 요청 실패", error);
  },
});
```

#### onSettled (성공, 실패 여부와 상관없이 요청 완료 시 실행)

```jsx
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, {
  onSettled: (data, error) => {
    console.log("데이터 요청 완료");
  },
});
```

#### select (데이터 받은 후 가공처리 가능)

```jsx
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, {
  select: (posts) => {
    return posts.filter((post) => post.id === 1);
  },
});
```

### 병렬 처리

병렬 처리를 하고 싶은 경우 `useQueries`를 사용한다.

```js
const results = useQueries([
  {
    queryKey: "users",
    queryFn: getUsers,
  },
  {
    queryKey: "posts",
    queryFn: getPosts,
  },
]);

// 로딩을 한번에 처리 가능
useEffect(() => {
  // 하나라도 로딩 중이면 isLoading 은 true
  const isLoading = results.some((result) => result.isLoading);
  console.log(isLoading);
}, [results]);
```

### 전역 설정하기

#### QueryClient를 만들 때, default 설정을 할 수 있다.

```jsx
const queryClient = new QueryClient({
  queryCache: new QueryCache({
    onError: (error, query) => {
      console.log(error, query); // query 를 통해 queryKey, state 등에 접근 가능
    },
    onSuccess: (data) => {
      console.log(data);
    },
  }),
});
```

#### 쿼리 옵션 기본값을 설정할 수 있다.

```js
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 0,
    },
  },
});
```

#### react suspense 와 함께 사용할 수 있다.

```jsx
return (
  // isLoading이 true면 Suspense의 fallback 내부 컴포넌트가 보여진다.
  // isError가 true면 ErrorBoundary의 fallback 내부 컴포넌트가 보여진다.
  <Suspense fallback={<div>로딩 중</div>}>
  {/*ErrorBoundary의 경우 설치해야 함*/}
    <ErrorBoundary fallback={<div>에러 발생</div>}>
      <div>{data}</div>
    </ErrorBoundary>
  </Supense>
);
```

사용하기 위해서는 `suspense: true` 옵션을 꼭 명시해주어야 한다.

```jsx
const {
  isLoading,
  data: posts,
  error,
} = useQuery("posts", getPosts, { suspense: true });
```

또는 default 옵션으로 명시할 수 있다.

```js
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 0,
      suspense: true,
    },
  },
});
```

<br/>

## useMutation

`useMutation`은 post, put, delete 등의 method로 서버의 데이터에 변화를 일으키고자 할 때 쓰는 Hook이다. useMutation은 useQuery 와 마찬가지로 isLoading, isError 등을 반환하지만, 쿼리 키값을 명시하지 않는다.

```jsx
const { mutate, isLoading, error } = useMutation(axios 요청 함수);
```

```jsx
export const createPost = async (post) => {
  const response = await axios.post(
    `https://jsonplaceholder.typicode.com/posts`,
    post
  );
  return response.data;
};

const { mutate, isLoading, error } = useMutation(createPost);

return (
  <button type="button" onClick={() => mutate(post)}>
    글쓰기
  </button>
);
```

### 요청 후 처리

요청의 성공, 실패 등의 여부에 따라서 특정한 코드를 실행하도록 설정해줄 수 있다.

#### onMutate (mutate 시 실행)

```jsx
const { mutate, isLoading, error } = useMutation(createPost, {
  onMutate: (variables) => {
    console.log("요청 시 내가 명시한 값", variables);
    return { id: 1 };
  },
});
```

#### onSuccess (요청 성공 시 실행)

```jsx
const { mutate, isLoading, error } = useMutation(createPost, {
  onSuccess: (data, variables, context) => {
    console.log("요청 성공", data);
    console.log("요청 시 내가 명시한 값", variables);
    console.log("onmutate 에서 리턴한 값", context);
  },
});
```

#### onError (요청 실패 시 실행)

```jsx
const { mutate, isLoading, error } = useMutation(createPost, {
  onError: (error, variables, context) => {
    console.log("요청 실패", error);
    console.log("요청 시 내가 명시한 값", variables);
    console.log("onmutate 에서 리턴한 값", context);
  },
});
```

#### onSettled (성공, 실패 여부와 상관없이 요청 완료 시 실행)

```jsx
const { mutate, isLoading, error } = useMutation(createPost, {
  onSettled: (data, error, variables, context) => {
    console.log("요청 완료");
    console.log("요청 시 내가 명시한 값", variables);
    console.log("onmutate 에서 리턴한 값", context);
  },
});
```

### 업데이트 (put, post) 및 자동 Get (invalidateQueries)

#### invalidateQueries

특정한 쿼리 키에 대해서 현재 받아온 데이터가 유효하지 않으니, 다시 해당 쿼리 키를 가진 useQuery 를 실행하라는 함수이다.

```js
const queryClient = useQueryClient();

queryClient.invalidateQueries("posts");
```

invalidateQueries 와 함께 onSuccess 를 활용하면, 글 작성 혹은 수정이 성공했을 때 자동으로 해당 글을 다시 받아오도록 코드를 작성할 수 있다. 다만 자동으로 다시 요청을 보내기 위해서는, posts 라는 쿼리 키를 가진 데이터가 표시되고 있어야 한다.

```js
// query client 를 가져옴
const queryClient = useQueryClient();

const { mutate } = useMutation(createPost, {
  onSuccess: () => {
    // createPost 가 성공하면 posts 라는 쿼리 키를 가진 useQuery 함수를 다시 실행한다.
    queryClient.invalidateQueries("posts");
  },
});
```

#### setQueryData

글을 수정하는 요청인 경우, useQuery로 값을 받아온 후 → mutate 해서 수정한 값을 put 하고 → setQueryData 로 저장된 캐시 데이터를 현재 수정된 값으로 변경하는 방식으로 진행된다.

```js
const { status, data, error } = useQuery(["posts", 글 번호], () => getPost(글 번호));

const queryClient = useQueryClient();

const { mutate } = useMutation(updatePost, {
  onSuccess: (data) => {
    // 요청 성공시 위 useQuery의 data가 자동으로 현재 data로 수정됨
    queryClient.setQueryData(["posts", 글 번호], data);
  }
});

mutate({title: '제목', body: '내용'});
```

<br/>

## pagination

### 간단하게 구현하기

```js
export const getPostsByPage = async (page) => {
  const response = await axios.get(
    `https://jsonplaceholder.typicode.com/posts?_limit=10&_page=${page}`
  );
  return response.data;
};

const [pageNum, setPageNum] = useState(1);
const {
  isLoading,
  data: posts,
  error,
} = useQuery(["posts", { page: pageNum }], () => getPostsByPage(pageNum), {});

return (
  <div>
    <button onClick={() => setPageNum(pageNum - 1)}>이전 페이지</button>
    <button onClick={() => setPageNum(pageNum + 1)}>다음 페이지</button>
  </div>
);
```

### useInfiniteQuery 활용하기

react query 는 데이터를 누적하면서 불러올 수 있도록 useInfiniteQuery 라는 함수를 지원하고 있다.

```jsx
const { data, fetchNextPage } = useInfiniteQuery({
    queryKey: 'posts',
    queryFn: (pageParam 을 인자로 받는 axios 함수),
    getNextPageParam: (lastPage, pages) => {
        return (다음 pageParam)
    },
})
```

```js
export const getPostsByPage = async ({
  pageParam = { start: 0, limit: 10 },
}) => {
  const response = await axios.get(
    `https://jsonplaceholder.typicode.com/posts?_start=${pageParam.start}&_limit=${pageParam.limit}`
  );
  return response.data;
};

const { data, fetchNextPage, isLoading } = useInfiniteQuery({
  queryKey: "posts",
  queryFn: getPostsByPage,
  getNextPageParam: (lastPage, pages) => {
    const lastPost = lastPage[lastPage.length - 1];
    return lastPost.id < 100 ? { start: lastPost.id, limit: 10 } : false;
  },
});

if (isLoading) return <>로딩 중</>;
return (
  <div>
    {data.pages && data.pages.map((page) => <PostList posts={page} />)}
    <button onClick={() => fetchNextPage()}>더 불러오기</button>
  </div>
);
```

#### pageParam

useInfiniteQuery 에 명시하는 쿼리 함수는 pageParam 이라는 인자를 무조건 받아야 한다. fetchNextPage 라는 함수를 실행하면, 자동으로 위에 명시한 getNextPageParam 함수가 실행되면서 그 리턴값이 다시 쿼리 함수의 pageParam 으로 들어간다.

#### getNextPageParam

getNextPageParam 은 다음 페이지로 넘어가기 위한 파라미터를 리턴할 수 있도록 작성해야 한다. getNextPageParam 에서는 lastPage (바로 이전 페이지의 데이터들) 및 pages (지금까지 받아온 모든 페이지의 데이터들) 에 접근할 수 있다.

#### data

pages라는 키에 페이지 별 데이터가 들어가는 형태로 구성해야 한다. 데이터에 접근하려면 data.pages 를 map 함수를 통해서 접근해야 한다.
