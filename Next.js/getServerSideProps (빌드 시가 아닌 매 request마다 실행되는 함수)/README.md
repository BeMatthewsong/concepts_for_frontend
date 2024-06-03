## getServerSideProps
서버 사이드 렌더링을 위한 데이터 가져오기 함수이며 빌드 시가 아닌 **매 요청마다** 데이터를 서버에서 가져온다.

ex) 자주 업데이트되는 posts 데이터들을 외부 API로부터 fetch해서 사전 렌더링하고 싶을 때 사용한다. 


```js
export async function getServerSideProps () {
  const data = await fetchData(); // 서버에서 데이터 가져오기
  return {
    props: {
      data,
    }, 
  }
}
```
