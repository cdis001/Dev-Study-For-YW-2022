# 3. 이벤트
- 무언가가 일어났다는 신호
- 모든 DOM 노드는 이러한 신호를 발생할 수 있음

## 대표적인 이벤트
1. 마우스 이벤트
   - click: 요소 위에서 마우스 왼쪽 버튼을 눌렀을 때(터치스크린이 있는 장치에선 탭 했을 때) 발생
   - contextmenu: 요소 위에서 마우스 오른쪽 버튼을 눌렀을 때 발생
   - mouseover / mouseout:  마우스 커서를 요소 위로 움직였을 때, 커서가 요소 밖으로 움직였을 때 발생
   - mousedown / mouseup: 요소 위에서 마우스 왼쪽 버튼을 누르고 있을 때, 마우스 버튼을 뗄 때 발생
   - mousemove: 마우스를 움직일 때 발생

2. 폼 요소 이벤트
   - submit: 사용자가  \<form>을 제출할 때 발생
   - focus: 사용자가 \<input>과 같은 요소에 포커스 할 때 발생

3. 키보드 이벤트
   - keydown & keyup: 사용자가 키보드 버튼을 누르거나 뗄 때 발생

4. 문서 이벤트
   - DOMContentLoaded: HTML이 전부 로드 및 처리되어 DOM 생성이 완료되었을 때 발생

5. CSS 이벤트
   - transitionend – CSS 애니메이션이 종료되었을 때 발생

## 이벤트 핸들러
- 이벤트에 반응하려면 이벤트가 발생했을 때 실행되는 함수인 핸들러(handler) 를 할당해야함
1. HTML tag 내부 on[event] 속성
   ```html
   <!-- 버튼 클릭시 onclick 안의 코드 실행 -->
   <input value="클릭해 주세요." onclick="alert('클릭!')" type="button">
   ```
   - 함수를 만들어서 이를 호출하는 방법을 추천
   ```html
   <script>
   function countRabbits() {
       for(let i=1; i<=3; i++) {
       alert(`토끼 ${i}마리`);
       }
   }
   </script>
    <input type="button" onclick="countRabbits()" value="토끼를 세봅시다!">
   ```

2. DOM 프로퍼티 on[event]
```html
<input type="button" id="button" value="클릭해 주세요.">
<script>
  button.onclick = function() {
    alert('클릭!');
  };
</script>
```
- onclick 프로퍼티는 단 하나밖에 없기 때문에, 복수의 이벤트 핸들러를 할당할 수 없음
- 핸들러를 제거하고 싶다면 elem.onclick = null 같이 null을 할당

3. 객체 형태의 핸들러와 handleEvent
- addEventListener를 사용하면 함수뿐만 아니라 객체를 이벤트 핸들러로 할당할 수 있음
- 이벤트가 발생하면 객체에 구현한 handleEvent 메서드가 호출
```html 
<button id="elem">클릭해 주세요.</button>

<script>
  let obj = {
    handleEvent(event) {
      alert(event.type + " 이벤트가 " + event.currentTarget + "에서 발생했습니다.");
    }
  };

  elem.addEventListener('click', obj);
</script>
```

## 버블링(bubbling)
- 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작함. 가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작
```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```
- 가장 안쪽의 \<p>를 클릭하면 순서대로 다음과 같은 일이 벌어짐
   1. \<p>에 할당된 onclick 핸들러가 동작
   2. 바깥의 \<div>에 할당된 핸들러가 동작
   3. 그 바깥의 \<form>에 할당된 핸들러가 동작
   4. document 객체를 만날 때까지, 각 요소에 할당된 onclick 핸들러가 동작

- 이벤트가 제일 깊은 곳에 있는 요소에서 시작해 부모 요소를 거슬러 올라가며 발생하는 모양이 마치 물속 거품(bubble)과 닮았기 때문에 이런 흐름을 '이벤트 버블링’이라고 부름

1. event.target
   - 이벤트가 발생한 가장 안쪽의 요소는 타깃(target) 요소라고 불리고, event.target을 사용해 접근할 수 있음
   - event.target은 실제 이벤트가 시작된 ‘타깃’ 요소. 버블링이 진행되어도 바뀌지 않음
   - event.preventDefault()를 이용하면 브라우저의 기본 동작을 막을 수 있음

## 이벤트 위임
- 이벤트 위임은 비슷한 방식으로 여러 요소를 다뤄야 할 때 사용
-  요소마다 핸들러를 할당하지 않고, 요소의 공통 조상에 이벤트 핸들러를 단 하나만 할당해도 여러 요소를 한꺼번에 다룰 수 있음
- [예시](./event.html)
- 이벤트 위임의 알고리즘
   1. 컨테이너에 하나의 핸들러를 할당.
   2. 핸들러의 event.target을 사용해 이벤트가 발생한 요소가 어디인지 알아냄.
   3. 원하는 요소에서 이벤트가 발생했다고 확인되면 이벤트를 핸들링

## 커스텀 이벤트
- 자바스크립트를 사용하면 핸들러를 할당할 수 있을 뿐만 아니라 이벤트를 직접 만들 수도 있음
- 직접 만든 커스텀 이벤트(custom event)는 '그래픽 컴포넌트(graphical component)'를 만들 때 사용
- click, mousedown 같은 내장 이벤트를 직접 만들 수도 있음
   - 테스팅을 자동화할 때 유용
   - 이런 경우엔 아주 조심해야함

### 이벤트 생성
```javascript
let event = new Event(type[, options]);
```
- type: 이벤트 타입을 나타내는 문자열로 "click"같은 내장 이벤트, "my-event" 같은 커스텀 이벤트가 올 수도 있음
- options: 두 개의 선택 프로퍼티가 있는 객체가 옴
   - bubbles: true/false – true인 경우 이벤트가 버블링 됨
   - cancelable: true/false – true인 경우 브라우저 '기본 동작’이 실행되지 않음

### 이벤트 실행
```javascript
<button id="elem" onclick="alert('클릭!');">자동으로 클릭 되는 버튼</button>

<script>
  let event = new Event("click");
  elem.dispatchEvent(event);
</script>
```
- dispatchEvent
- 이벤트 객체를 생성한 다음엔 elem.dispatchEvent(event)를 호출해 요소에 있는 이벤트를 반드시 '실행’시켜줘야 함

### 커스텀 이벤트
```javascript
<h1 id="elem">이보라님, 환영합니다!</h1>

<script>
  // 추가 정보는 이벤트와 함께 핸들러에 전달됩니다.
  elem.addEventListener("hello", function(event) {
    alert(event.detail.name);
  });

  elem.dispatchEvent(new CustomEvent("hello", {
    detail: { name: "보라" }
  }));
</script>
```
- new CustomEvent()
- CustomEvent의 두 번째 인수엔 객체가 들어갈 수 있는데, 개발자는 이 객체에 detail이라는 프로퍼티를 추가해 커스텀 이벤트 관련 정보를 명시하고, 정보를 이벤트에 전달할 수 있음
- detail 프로퍼티엔 어떤 데이터도 들어갈 수 있음
- 다른 이벤트 프로퍼티와 충돌을 피하기 위해 detail 프로퍼티 사용


- 출처
   > https://ko.javascript.info/

   > https://developer.mozilla.org/
   
   > https://ko.javascript.info/dispatch-events
   
- 추후 JS this 공부 후 event와 this 내용 추가!!