## GET 메서드 vs POST 메소드
GET 메소드는 리소스를 요청하는 메소드이며, POST 메소드는 리소스를 생성하거나 업데이트하는 메소드입니다. <br/>

두 메소드를 비교하자면, GET 메소드는 북마크와 캐싱이 가능하지만 POST 메소드는 그렇지 않습니다. <br/>

그리고 GET 요청을 해서 받아온 데이터가 HTTP Request Message의 Header 부분의 URL이라는 공간에 담겨지기에 데이터의 크기가 제한적이고 보안성이 떨어집니다.
반면 POST 요청은 HTTP Request Message의 Body 부분에 데이터를 담기 때문에 데이터의 크기와 보안성이 GET 요청보다 낫습니다.

마지막으로 GET 요청은 멱등성을 지니고 있어, 여러 번 요청을 하여도 결과가 달라지지 않습니다. 
반면에 POST 요청은 멱등성이 없어서 여러 번 요청을 하면 새로운 데이터를 만들어냅니다.

<img width="1376" alt="image" src="https://github.com/BeMatthewsong/concepts_for_frontend/assets/98685266/6e9bb5be-06f4-4162-8c4d-0d0ec24f8c9d">
