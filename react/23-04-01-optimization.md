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
