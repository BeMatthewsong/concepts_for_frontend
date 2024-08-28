## 글로벌 어트리뷰트 (HTML Global Attribute)

글로벌 어트리뷰트는 모든 HTML 요소가 공통으로 사용할 수 있는 어트리뷰트다. 몇몇 요소에는 효과가 적용되지 않을 수 있지만, 글로벌 어트리뷰트는 대체로 모든 요소에 사용될 수 있다.

<Attribute	Description>
id:	유일한 식별자(id)를 요소에 지정한다. 중복 지정이 불가하다.
class:	스타일시트에 정의된 class를 요소에 지정한다. 중복 지정이 가능하다.
hidden:	css의 hidden과는 다르게 의미상으로도 브라우저에 노출되지 않게 된다.
lang:	지정된 요소의 언어를 지정한다. 검색엔진의 크롤링 시 웹페이지의 언어를 인식할 수 있게 한다.
style:	요소에 인라인 스타일을 지정한다.
tabindex:	사용자가 키보드로 페이지를 내비게이션 시 이동 순서를 지정한다.
title:	요소에 관한 제목을 지정한다.

## 느낀 점
여기서 id, class, style 만 알았었는데 tabindex, title, lang 은 유용하게 쓰일 것 같다.

tabinde는 ux 향상, title, lang은 seo 향상

## tabindex

### tabindex = 0
이 기능은 복잡한 UI를 <div>나 <span>과 같이 tab 키로 포커스가 불가능한 요소를 기반으로 구현한 후 포커스가 오게 하고 싶을 때 주로 사용다.
![image](https://github.com/user-attachments/assets/5ab6e4df-550c-4ed1-ae37-bbe01f8cd67a)
```html
<h2 tabindex="0">연락처</h2>
```
a 태그 다음에 연락처라는 내용이 담긴 h2 태그에 tab으로 이동할 수 있다.

### tabindex = -1
해당 요소의 tabindex 속성을 -1로 설정해주면 상호작용이 가능한 요소라도 포커스가 이동하지 않게 된다.
```html
<button tabindex="-1">제출</button>
```
button 태그는 tab으로 접근할 수 없게 만들 수 있다.

### tabindex = 양수
tab으로 접근할 수 있는 요소의 순서를 바꿀 수 있다.
첫번째 <input> 요소의 tabindex 속성을 2로, 두번째 <input> 요소의 tabindex 속성을 1로 설정할 수 있다.
```html
<p>
  <label>
    <span>이름: </span>
    <input type="text" name="name" tabindex="2" />
  </label>
</p>

<p>
  <label>
    <span>이메일: </span>
    <input type="email" name="email" tabindex="1" />
  </label>
</p>
```
