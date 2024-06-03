## getStaticProps
정적 페이지 생성 (SSG)을 위한 데이터 가져오기 함수이며, **런타임이 아닌 빌드 타임에서만 실행이 되므로 변동이 거의 없는 데이터 대상으로만 적용하는 게 좋다**.

예시) 변동이 거의 없는 랜딩 페이지 혹은 FAQ 페이지

```js
export async function getStaticProps() {
  const posts = await getPosts(); // 데이터 가져오는 함수
  // 리턴하는 방식이 정해져 있으니 유의하자 ⭐️
  return {
    props: {
      posts,
    }
  }  
}
```
