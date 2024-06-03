## getStaticPaths
> 만약 블로그 포스팅이 100개가 있다면, 이런 경우에는 경로를 어떻게 설정해야될까? 매 포스팅마다 pages/ 폴더 아래 자바스크립트 파일을 만들어줘야 한다면?
> 
> -> Next.js에는 동적 라우팅(dynamic routes) 기능이 있고, getStaticPaths를 사용해 렌더링하기 위해 필요한 경로를 설정할 수 있다.

**getStaticPaths**는 동적 경로를 위한 정적 경로 생성 함수이며, 동적으로 생성되는 페이지를 사전 렌더링할 때 사용된다.

```js
export async function getStaticPaths() {
  const paths = await fetchDynamicPaths();
  return {
    paths,
    fallback: false, // 없는 경로는 404 페이지로 처리
  }
}
```


![image](https://github.com/BeMatthewsong/concepts_for_frontend/assets/98685266/65ec49f7-454f-46be-92f1-d5cd6649033c)
```js
function BlogPost({ post }) {
  return (
    <div>
      <h1> {post.title} </h1>
      <div> {post.content} </div>
    </div>
  )
}

export async function getStaticPaths() {
  const res = await fetch('http://.../posts')
  const posts = await res.json()
  
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))
  
  return { paths, fallback: false }

}

export async function getStaticProps({ params }) {
  const res = await fetch(`https://.../posts/${params.id}`)
  const post = await res.json()
  return {
    props: {
      post,
    }
  }
}

export default BlogPost
```

[참고 링크: [Next.js] getStaticProps, getStaticPaths, getServerSideProps 란?](https://velog.io/@jwhan/nextjs-getStaticProps-getStaticPaths-getServerSideProps#getstaticpaths)
