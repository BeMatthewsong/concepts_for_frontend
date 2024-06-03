# 브라우저의 렌더링

### ⭐️ 요약
```
브라우저의 렌더링은 Parsing -> Style -> Layout -> Paint -> (Reflow or Repaint) 단계로 진행됩니다.

1. Parsing 단계에서 서버로부터 받은 HTML, CSS 파일로 DOM, CSSOM을 생성합니다.
2. Style 단계에서는 DOM과 CSSOM을 결합하여 Render Tree를 생성합니다.
3. Layout 단계에서는 렌더 트리를 레이아웃을 실행시켜 각 노드의 위치, 크기와 같은 기하학적 형태를 계산합니다.
4. Paint 단계에서는 각 노드를 화면에 그립니다.
5. 렌더 트리의 변화에 따라 리플로우 및 리페인트 단계를 실행합니다.

브라우저의 성능 저하를 막기 위해서는 리플로우와 리페인트 단계를 줄여야 합니다.
예를 들어, 리플로우를 막기 위해 레이아웃에 잦은 변화를 주는 요소를 fixed나 absolute로 포지션을 줄 수 있는 방법이 있습니다.

추가로
`translate` → 리페인트, 리플로우 모두 X (가능하면 이걸로 사용)
`left, right`  → 리플로우 발생
`backgroundColor, opacity` → 리페인트 발생
```

### 렌더링 과정

1. **DOM 트리 생성** (HTML parser에 의한 DOM Tree)
2. **CSSOM 생성** (CSS parser에 의한 CSSOM 생성) (1 과 병렬적으로 작동)
3. **DOM트리 + CSSOM 접합 및 Render Tree 생성**

   → display: none; 과 같은 속성은 화면에서 공간을 차지하지 않기 때문에 렌더 트리에서 제외됨
5. **Layout (Reflow)**

   → 뷰포트 내의 각 노드들의 정확한 위치와 크기 계산

   → %, vh, vw와 같이 상대적인 위치, 크기를 실제 화면에 그려지는 px 단위로 변환하는 과정
7. **Paint**

   → Layout 과정이 완료되면 요소들의 위치, 크기, 스타일 계산이 완료된 렌더트리 존재

   → 렌더트리 이용하여 브라우저는 요소들을 실제 화면에 그린다.

   → backgroud-color, color 등의 경우에는 빠르게 painting 되지만, 그라데이션, 그림자 효과 등 복잡한 스타일은 Painting 소요시간이 비교적 오래걸린다.
   
9. **렌더트리의 변화**

   → 특정 이벤트에 따라 HTML 요소의 크기, 위치 등이 변경되면 영향받는 자식 노드, 부모 노드 들을 포함하여 Layout을 다시 수행한다.

   → 다시 Layout (계산하는 과정)을 수행하는 걸 Reflow 라고 하고

   → 다시 화면에 그려주는 과정을 Repaint라고 한다.

---
### Reflow가 일어나는 경우

- 페이지 초기 렌더링 (최초 Layout)
- 브라우저 리사이징 (Viewport 크기 변경)
- 노드 추가 또는 제거
- 요소의 위치, 크기 변경
- 폰트 변경, 이미지 크기 변경

### Repaint가 일어나는 경우

- Reflow만 수행됐을 때는 실제 화면에 반영되지 않는다.
- 그려주는 과정이 Repaint이다.
- 반드시 Reflow가 진행되어야만 Repaint가 진행되는 것은 아니다. background-color, opacity 등 레이아웃에는 영향을 주지 않는 스타일 속성이 변경되었을 때는 Repaint만 수행된다.

### 브라우저 성능저하의 원인

1. 잦은 Reflow와 Repaint

---
### 렌더링 최적화

1. Reflow 최소화

   → Reflow 발생하는 속성보다, Repaint만 발생하는 속성 사용

   → border, margin 등 위치가 조금이라도 변경되는 건 Reflow가 발생한다

2. 영향을 주는 노드 최소화하기

   → 레이아웃 변화가 많은 요소의 경우(변화가 찾은 컴포넌트의 경우), position을 absolute / fixed 로 사용하면 좋다.

   → fixed 의 경우 layout이 수정되지 않기 때문에 reflow과정이 필요없어져 repaint 연산비용만 들게 되어 효율적이다.

3. 프레임 줄이기

   → 덜 부드럽게 표현하게 되면 성능개선 (사용자 경험은 나빠지겠지만..)

4. Reflow / Repaint 가 모두 발생하지 않는 속성도 있다.

   → transform, opacity, cursor, orphans, perspective

---
## :hammer_and_wrench: 용어 공부

### :gear: 렌더링엔진

- 브라우저 마다 다르지만, 브라우저는 렌더링을 수행하는 렌더링 엔진을 가지고 있습니다. 크롬은 블링크(Blink), 사파리는 웹킷(Webkit) 그리고 파이어폭스는 게코(Gecko)라는 렌더링 엔진을 사용합니다.

### :gear: CRP

- CRP (Critical Rendering Path, 중요 렌더링 경로)는 브라우저가 HTML, CSS, Javascipt를 화면에 픽셀로 변화하는 일련의 단계를 말합니다. CRP는 Document Object Model (DOM), CSS Object Model (CSSOM), 렌더 트리 그리고 레이아웃을 포함합니다.

### :gear: 파싱

- 파싱은 하나의 프로그램을 런타임 환경(예를 들면, 브라우저 내 자바스크립트 엔진)이 실제로 실행할 수 있는 내부 포맷으로 분석하고 변환하는 것을 의미합니다. 즉, 파싱은 문서의 내용을 토큰(token)으로 분석하고, 문법적 의미와 구조를 반영한 파스 트리(parse tree)를 생성하는 과정입니다.

### :gear: DOM

- **DOM(Document Object Model)이란?** 웹 페이지를 이루는 태그들을 자바스크립트가 이용할 수 있게끔 브라우저가 트리구조로 만든 객체 모델을 의미합니다. 영어 뜻풀이 그대로 하자면 문서 객체 모델을 의미합니다. 문서 객체란 html, head, body와 같은 태그들을 javascript가 이용할 수 있는 (메모리에 보관할 수 있는) 객체를 의미합니다. DOM은 HTML과 스크립팅 언어(JavaScript)를 서로 이어주는 역할을 합니다.

### :gear: CSSOM

- **CSSOM(CSS Object Model)이란?** CSS 내용을 파싱하여 자료를 구조화 한 것을 CSSOM이라고 합니다. 즉 DOM처럼 CSS의 내용을 해석하고 노드를 만들어 트리 구조로 만든 것을 CSSOM이라 합니다.

### :gear: 렌더트리

- **렌더트리(Render Tree)란?** 렌더 트리는 CSSOM과 DOM 트리의 결합으로 만들어집니다. 렌더 트리는 웹 페이지에 나타낼 각 요소들의 위치(Layout, 레이아웃)을 계산하는데 사용되고 픽셀을 화면에 렌더링하는 페인트(Paint) 즉 화면에 요소들을 표현하는 프로세스를 위해 존재합니다.

### :gear: Layout

- **Layout(Reflow)이란?** 뷰포트 내에서 노드의 정확한 위치와 크기를 계산합니다. 이것이 바로 'Layout' 단계이며 경우에 따라 'Reflow' 라고도 합니다.

### :gear: Paint

- **Paint란?** 노드와 해당 노드의 계산된 스타일 및 기하학적 형태에 대해 파악했으므로, 렌더링 트리의 각 노드를 화면의 실제 픽셀로 변환하는 마지막 단계에 이러한 정보를 전달합니다. 이 단계를 흔히 '페인팅' 또는 '래스터화'라고 합니다.

<br>
