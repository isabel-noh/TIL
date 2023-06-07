# Real DOM vs Virtual DOM

React와 Vue에서는 화면에 보여지는 데이터가 변경되면 virtual DOM에 렌더링됩니다.  
그 후, 이전 virtual DOM에 있던 내용과 비교해서, 변경된 부분만 real DOM에 적용되게 합니다.

그러면 여기서 real DOM과 virtual DOM은 뭘까요?

<aside>
💡 학습 목표: Javascript에서의 DOM에 대해 알아보고, DOM과 virtual DOM의 차이점에 대해서 이해해봅시다.

</aside>

## 브라우저 렌더링

**브라우저**: 웹에서 페이지를 찾아서 보여주고, 사용자가 하이퍼링크를 통해 다른 페이지로 이동할 수 있도록 하는 프로그램(MDN)

```markdown
예) Chrome, Firefox, Safari, Opera …
```

**렌더링**: 서버로부터 HTML, CSS, JavaScript 등 작성한 파일을 받아 브라우저에 뿌려주는 것

### **브라우저 렌더링 과정 5단계**

1. **Parsing**

   HTML파일과 CSS파일을 서버로부터 받아와 parsing하여 DOM tree와 CSSOM tree를 생성

2. **Style**

   두 트리를 합쳐 Rendering Tree를 생성

3. **Layout/Reflow**

   Rendering Tree에서 각 노드의 위치와 크기를 계산

4. **Painting(repaint)**

   계산된 값을 이용해 각 노드를 화면상의 실제 픽셀로 변환하고, 레이어 생성

5. **Composite**

   레이어를 합성하여 실제 화면에 출력

# DOM이란?

- 문서 객체 모델 ( **Document Object Model** )의 줄임말

- html 파일을 웹 브라우저에서 보여주게 하기 위해서는 **`브라우저 렌더링 엔진`**은 웹 문서를 parsing하여 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 올림 → `DOM`
- 모든 요소, 텍스트, attribute들은 각각 객체로 만들어지고, 이 객체들은 위와 같이 트리 구조로 구성되어있기 때문에 **`DOM Tree`**라고 부름
- DOM tree는 각 노드들로 이루어져있고, 이 노드들은 각 객체들임
- 화면에 그려진 DOM은 DOM API를 통해 Javascript와 같은 스크립팅 언어로 동적으로 조작할 수 있고, 이 변경된 DOM은 rendering에 반영됩니다.

```
[DOM을 사용하는 API들의 목록]
  document.getElementById(id)
  document.getElementsByTagName(name)
  document.createElement(name)
  parentNode.appendChild(node)
  element.innerHTML
  element.setAttribute
  element.getAttribute
  element.addEventListener
```

```jsx
// DOM 조작 예시
document.querySelector(‘#title”).style.color = “red”;
```

# Virtual DOM

### 1. Virtual DOM이 등장하게 된 배경

- 화면에 보여지는 데이터값이 수정되면 브라우저의 렌더링 과정이 전체가 다시 실행되어, 비효율적
- SPA로 된 웹페이지들이 점차 늘어나면서 사용자 인터렉션에 의해 화면이 즉각적으로 수정되어야 하는 경우가 더욱 많아짐
- 또한 CSR 방식으로 렌더링 되는 경우에는, 처음 렌더링 이후에는 서버로부터 데이터만 받아오고 뷰는 Javascript로 관리하기 때문에 브라우저에서 연산이 많아지면 렌더링 속도가 느려지는 문제도 발생할 수 있음

→ 이러한 문제를 해결하기 위해서 virtual DOM이 등장!

### 2. `Virtual DOM`

- Virtual DOM은 Real DOM을 컴포넌트 단위로 쪼개어 추상화시킨 메모리상에만 존재하는 복사본
- html객체에 기반한 Javascript 객체로 표현되고, 실제 DOM이 아닌 메모리 상에서 동작

html

```html
<ul id="items">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

javascript

```jsx
let domNode = {
  tagName: "ul",
  attributes: {
    id: "items",
  },
  children: [
    {
      tagName: "li",
      textContent: "Item 1",
    },
    {
      tagName: "li",
      textContent: "Item 2",
    },
  ],
};
```

- virtual DOM 적용
  - 데이터가 변경
  - 전체가 virtual DOM에 렌더링
  - **이전** virtual DOM에 있던 내용과 **업데이트 후**의 내용을 **비교**
  - 바뀐 부분만 실제 DOM에 적용
- 변경되는 부분만 real DOM에 적용하기 때문에, 연산 비용 측면에서 효율적
- 수정 사항이 여러 개 있어도 virtual DOM은 real DOM에 렌더링을 1번만 발생
  - DOM 요소의 변화를 **묶어서** 적용 후, 이를 Real DOM에 동기화

### 3. React에서의 Virtual DOM 렌더링

**React의 두 개의 가상돔**

1. \*\*\*\*렌더링 이전 화면 구조를 나타내는 가상돔
2. 렌더링 이후에 보이게 될 화면 구조를 나타내는 가상돔

- React에서 데이터 업데이트 시 virtual DOM에서 real DOM으로 렌더링되는 과정
  - 데이터 업데이트
  - React.createElement()를 통해 JSX.element를 렌더링
  - 모든 virtual DOM object가 업데이트 됨
  - React는 virtual DOM을 이전 virtual DOM의 스냅샷과 비교하여 바뀐 부분을 캐치!

---

<aside>
💡 **`Diffing`** Algorithm: virtual DOM이 업데이트되면, React는 virtual DOM을 이전 virtual DOM의 스냅샷과 비교하여 바뀐 부분을 검사

</aside>

- element의 속성값만 바뀐 경우 → **속성 값만 업데이트**
- element의 태그 혹은 컴포넌트가 변경된 경우 → **해당 node를 포함한 하위 node를 unmount 후 새로운 virtual DOM으로 대체**

---

Diffing 알고리즘을 통해 확인한 새로 바뀐 부분들을 DOM object에 적용 → **`재조정(reconciliation)`**

### 4. 무조건 Virual DOM이 좋음?

정보만 제공하고, 사용자의 interaction이 많지 않은 페이지라면 Real DOM이 성능이 더 좋을수도 있다.

<aside>
💡 SPA로 제작된 큰 규모의 웹페이지는 Virtual DOM을 활용하여 브라우저의 연산 양을 줄여 성능 개선에 도움을 줄 수 있다.

</aside>
