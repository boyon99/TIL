## 최적화시키는 방법

> > - [컴포넌트 성능 최적화를 위한 투두](https://github.com/boyon99/react_todo-app)
> > - [axios를 활용하여 뉴스뷰어 웹 만들기](https://github.com/boyon99/react_news-viewer)
> > - https://mango-tower-9f1.notion.site/React-11-c9c2b10c14ea4b59b7f3297c5daf9a28

- state의 경우

```jsx
// add
setArticles([...articles, 2]);
// remove
setArticles(articles.filter((article) => article.id !== id));
```

- [ ] 최적화하기 - useMemo, useCallback, useTransition, useDeferrenedValue, react.lazy

- **의존성 배열 / useEffect / React.memo / useCallback / useMemo / Context API**
  - 리액트에서 렌더링 최적화를 수행하는 법
  - React.memo를 이용해 컴포넌트 렌더링 최적화하기
  - 메모이제이션을 통한 최적화 수행하기
  - useEffect의 의존성 배열 올바르게 다루기
  - Context API로 컴포넌트에 맥락 전달하기
