
# 2. DOM
- 웹 페이지 내의 모든 콘텐츠를 객체로 나타내는데, 이를 문서 객체 모델(Document Object Model, DOM)이라 함
- document 객체를 이용해 사용 가능
```javascript
// 배경을 붉은색으로 변경하기
document.body.style.background = "red";

// 1초 후 원상태로 복구하기
setTimeout(() => document.body.style.background = "", 1000);
```
- 브라우저 객체 모델(Browser Object Model, BOM)은 문서 이외의 모든 것을 제어하기 위해 브라우저(호스트 환경)가 제공하는 추가 객체를 나타냄
   - navigator 객체는 브라우저와 운영체제에 대한 정보를 제공
   - location 객체는 현재 URL을 읽을 수 있게 해주고 새로운 URL로 변경(redirect)할 수 있게 함
```javascript
```
- 모든 HTML 태그는 객체이므로, 자바스크립트를 통해 접근할 수 있고, 페이지를 조작할 때 이 객체를 사용

### 노드
- 정보를 저장하는 계층적 단위
- DOM은 이러한 노드들을 정의하고, 그들 사이의 관계를 설명해 주는 역할을 함
- 노드 트리(node tree)라고 불리는 계층적 구조에 저장
   - 노드들의 집합이며, 노드 간의 관계
- 최상위 레벨인 루트 노드(root node)로부터 시작하여, 가장 낮은 레벨인 텍스트 노드까지 뻗어 내려감
- DOM을 이용하여 노드 트리에 포함된 모든 노드에 접근 가능
- 노드의 관계
   1. 루트 노드(root node)
      - 노드 트리의 가장 상위의 노드

   2. 자식 노드(child node)
      - 바로 아래의 자식 요소

   3. 형제 노드(sibling node)
      - 같은 부모 노드를 가지는 모든 노드
      
   4. 조상 노드(ancestor node)
      - 부모 노드를 포함해 계층적으로 현재 노드보다 상위에 존재하는 모든 노드
      
   5. 자손 노드(descendant node)
      - 자식 노드를 포함해 계층적으로 현재 노드보다 하위에 존재하는 모든 노드
      

### 노드 종류
1. document.documentElement
   - \<html> 태그에 해당
   - document를 제외하고 DOM 트리 꼭대기에 있는 노드

2. document.body
   - \<body> 태그에 해당
   - 자주 쓰이는 노드 중 하나

3. document.head
   - \<head> 태그에 해당
   
4. childNodes
   - 텍스트 노드를 포함한 모든 자식 노드
   
5. firstChild
   - 첫번째 자식 노드
   
6. lastChild
   - 마지막 자식 노드

7. nextSibling
   - 다음 형제 노드

8. previousSibling 
   - 이전 형제 노드

9. parentNode 
   - 부모 노드

### 요소 검색
- 상대 위치를 이용하지 않으면서 웹 페이지 내에서 원하는 요소 노드에 접근하는 방법

1. .getElementById(id)
   - 요소에 id 속성이 있으면 위치에 상관없이 접근 가능
   - 요소의 id 속성값은 중복되어선 안 됨

2. .querySelectorAll
   - "."이나 "#"(css 선택자)을 이용해 해당하는 모든 요소를 가져올 수 있음

3. .querySelector
   - "."이나 "#"(css 선택자)을 이용해 해당하는 첫 번째 요소를 가져올 수 있음

4. .closest
   - "."이나 "#"(css 선택자)을 이용해 해당하는 가장 가까운 요소를 가져올 수 있음
   ```html
   <h1>목차</h1>

    <div class="contents">
    <ul class="book">
        <li class="chapter">1장</li>
        <li class="chapter">2장</li>
    </ul>
    </div>

    <script>
    let chapter = document.querySelector('.chapter'); // LI

    alert(chapter.closest('.book')); // UL
    alert(chapter.closest('.contents')); // DIV

    alert(chapter.closest('h1')); // null(h1은 li의 조상 요소가 아님)
    </script>
   ```

5. 비표준 속성값 가져오기
- DOM은 HTML 표준 속성을 인식하고, 이 표준 속성을 사용해 DOM 프로퍼티를 만듦(id, class...)
- 표준이 아닌 속성일 때 요소를 가져오는 메서드
   1. elem.hasAttribute(name) 
       - 속성 존재 여부 확인
   2. elem.getAttribute(name) 
       - 속성값을 가져옴
   3. elem.setAttribute(name, value)
       - 속성값을 변경함
   4. elem.removeAttribute(name)
       - 속성값을 지움
- 비표준 속성?
   - 비표준 속성은 사용자가 직접 지정한 데이터를 HTML에서 자바스크립트로 넘기고 싶은 경우나 자바스크립트를 사용해 조작할 HTML 요소를 표시하기 위해 사용
   - 비표준 속성을 사용해 코드를 작성했는데 나중에 그 속성이 표준으로 등록되게 되면 문제가 발생되므로, ’data-'로 시작하는 속성 전체는 개발자가 용도에 맞게 사용하도록 별도로 예약
   - dataset 프로퍼티를 사용하면 이 속성에 접근할 수 있음
   - 커스텀 데이터를 안전하고 유효하게 전달
   ```html
   <style>
    .order[data-order-state="new"] {
        color: green;
    }

    .order[data-order-state="pending"] {
        color: blue;
    }

    .order[data-order-state="canceled"] {
        color: red;
    }
    </style>

    <div id="order" class="order" data-order-state="new">
    A new order.
    </div>

    <script>
    // 읽기
    alert(order.dataset.orderState); // new

    // 수정하기
    order.dataset.orderState = "pending"; // (*)
    </script>
   ```