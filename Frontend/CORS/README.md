## CORS (Cross-Origin-Resource-Sharing)

### 정의
**CORS**란 브라우저에서 cross-origin 요청을 안전하게 할 수 있도록 하는 매커니즘을 말합니다. <br/>
브라우저는 SOP인 동일 출처 정책을 따릅니다. 동일 출처 정책은 Origin에서 프로토콜, 도메인, 포트 3가지를 비교해서 동일한지 따지는 걸 말합니다.
이 중에 하나라도 다르다면 CORS 에러가 발생합니다.

>cross-origin<br/>
cross-origin이란 다음 중 한 가지라도 다른 경우를 말합니다.
>
>프로토콜 - http와 https는 프로토콜이 다르다.<br/>
도메인 - domain.com과 other-domain.com은 다르다.<br/>
포트 번호 - 8080포트와 3000포트는 다르다.

### CORS를 사용하는 이유
CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 된다면, <br/>
다른 사이트에서 원래 사이트를 흉내낼 수 있게 됩니다. <br/>
그래서 한 예시로는 원래 사이트인 척하면서 사용자가 로그인하도록 유인하여 악의적으로 사용자의 개인정보를 탈취할 수 있습니다. <br/>
그래서 이런 공격을 할 수 없도록 브라우저에서 보호하기 위해 CORS가 필요합니다.


### CORS 에러 대응하기
1. 서버에서 Access-Control-Allow-Origin를 세팅하기

-> 수락할 출처를 명시적으로 등록할 수 있습니다. (다만, 보안이 약해질 가능성이 있습니다.)

2. 프록시 서버 사용하기

-> 프록시를 사용하여 리소스와 동일한 출처에서 요청을 보내는 것처럼 할 수 있습니다.

##### 참고 링크
[CORS는 무엇인가요?](https://hannut91.github.io/blogs/infra/cors) <br/>
[토스 - cors](https://docs.tosspayments.com/resources/glossary/cors)
