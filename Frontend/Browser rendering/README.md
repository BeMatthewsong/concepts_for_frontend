# 브라우저의 렌더링

### ⭐️ 요약
```
브라우저의 렌더링은 Parsing -> Style -> Layout -> Paint -> (Reflow or Repaint) 단계로 진행됩니다.

1. Parsing 단계에서 서버로부터 받은 HTML, CSS 파일로 DOM, CSSOM을 생성합니다.
2. Style 단계에서는 DOM과 CSSOM을 결합하여 Render Tree를 생성합니다.
3. Layout 단계에서는 렌더 트리를 레이아웃을 실행시켜 각 노드의 위치, 크기와 같은 기하학적 형태를 계산합니다.
4. Paint 단계에서는 각 노드를 레이아웃과 무관한 CSS를 적용하여 화면에 그립니다.
5. 렌더 트리의 변화에 따라 리플로우 및 리페인트 단계를 실행합니다.

브라우저의 성능 저하를 막기 위해서는 리플로우와 리페인트 단계를 줄여야 합니다.
예를 들어, 리플로우를 막기 위해 레이아웃에 잦은 변화를 주는 요소를 fixed나 absolute로 포지션을 줄 수 있는 방법이 있습니다.
```

### 렌더링 과정

1. DOM 트리 생성 (HTML parser에 의한 DOM Tree)
2. CSSOM 생성 (CSS parser에 의한 CSSOM 생성) (1 과 병렬적으로 작동)
3. DOM트리 + CSSOM 접합 및 Render Tree 생성

   → display: none; 과 같은 속성은 화면에서 공간을 차지하지 않기 때문에 렌더 트리에서 제외됨
5. Layout (Reflow)

   → 뷰포트 내의 각 노드들의 정확한 위치와 크기 계산

   → %, vh, vw와 같이 상대적인 위치, 크기를 실제 화면에 그려지는 px 단위로 변환하는 과정
7. Paint

   → Layout 과정이 완료되면 요소들의 위치, 크기, 스타일 계산이 완료된 렌더트리 존재

   → 렌더트리 이용하여 브라우저는 요소들을 실제 화면에 그린다.

   → backgroud-color, color 등의 경우에는 빠르게 painting 되지만, 그라데이션, 그림자 효과 등 복잡한 스타일은 Painting 소요시간이 비교적 오래걸린다.
   
9. 렌더트리의 변화

   → 특정 이벤트에 따라 HTML 요소의 크기, 위치 등이 변경되면 영향받는 자식 노드, 부모 노드 들을 포함하여 Layout을 다시 수행한다.

   → 다시 Layout (계산하는 과정)을 수행하는 걸 Reflow 라고 하고

   → 다시 화면에 그려주는 과정을 Repaint라고 한다.

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
