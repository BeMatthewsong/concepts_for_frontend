CSS방법론에는 다양한 방법론들이 존재하지만 크게 **OOCSS, BEM, SMACSS**로 나눠지게 되며 상황에 따라 다르게 적용된다.

### OOCSS

<aside>
💡 OOCSS(Object Oriented CSS)는 CSS를 **모듈(module) 방식**으로 작성하여 중복을 줄이는 방식의 방법론이다

중복되는 디자인 요소를 따로 빼내어 작성하기 때문에 반복적으로 사용가능하다. 또한 코드의 재사용성이 높아져 적은 코드량으로 최적의 성능을 보인다.

```html
// 기존 방식
<a class=”instagram_btn instagram_skin”>Instagram</a>
<a class=”facebook_btn facebook_skin”>Facebook</a>

// OOCSS 적용
<a class=”btn skin instagram”>Instagram</a>
<a class=”btn skin facebook”>Facebook</a>

.btn -> 공통 버튼 스타일 정의
.skin -> 공통 스킨 스타일 정의
```

</aside>

### BEM

<aside>
💡 BEM(Block Element Modifier)은 **블록(block), 요소(element), 상태(modifier)**로 구분하여 클래스 이름을 작성하는 방식의 방법론이다

각 부분을 `__`와 `--`로 구분하여 짓게 된다.

- 블록(block): 재사용성이 가능하고 기능적으로 독립이 가능한 컴포넌트이다. 일반적으로 하나의 단어를 사용하되 길어질 경우엔 ``를 사용한다.

```css
.header {..}
.block {..}
```

- 요소(element): 블록을 구성하는 단위이다. `__`를 사용한다.

```css
.header {..}
.header__tap {..}
.header__content {..}
.header__logo__button {..}
```

- 블록이나 요소의 속성으로 `--`를 사용한다.

```css
.header--hide {..}
.header__tap--big {..}
.header__content--disabled {..}
```

</aside>

### SMACSS

<aside>
💡 **SMACSS(Scalable and Modular Architecture for CSS)**는 CSS를 **범주화(Categorization)**로 패턴화 하고자 하는 방법론이다

*기본(base), 레이아웃(layout), 모듈(module), 상태(state), 테마(theme)* 다섯가지의 범주를 제시한다.

</aside>

##### 참고 링크
[CSS방법론 (OOCSS, BEM, SMACSS)](https://velog.io/@hahan/CSS방법론OOCSS-BEM-SMACSS)
