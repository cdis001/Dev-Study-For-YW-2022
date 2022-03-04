# CSS
- Cascading Style Sheets
- 웹페이지를 꾸미기 위한 코드

## CSS의 구조
```css
선택자 {
   속성: 속성 값;
}
```
```css
h1 {
   color: red;
}
```

## CSS 선택자
- HTML 요소 이름, 꾸밀 요소를 선택함
- 선택자는 여러개의 요소를 선택할 수도 있음
```css
h1, h2 {
   color: white;
}
```
- 선택자 종류
  1. 요소 선택자
    ```css
    h1 {
       color: red
    }
    ```
    - 특정 타입의 모든 HTML 요소

  2. 아이디 선택자
    ```html
    <h1 id="my-id">
    ```
    ```css
    #my-id {
       color: red
    }
    ```
    - 특정 아이디를 가진 페이지의 요소

  3. 클래스 선택자
    ```html
    <h1 class="my-class">
    ```
    ```css
    .my-class {
       color: red
    }
    ```
    - 특정 클래스를 가진 페이지의 요소

  4. 속성 선택자
    ```html
    <img src="myimage.png">
    ```
    ```css
    img[src] {
       background-color: red;
    }
    ```
    - 특정 속성을 갖는 페이지의 요소.
    - scr라는 속성을 갖고 있는 요소만 선택함

  5. 가상 클래스 선택자
    ```css
    a:hover {
       background-color: red;
    }
    ```
    - 특정 요소이지만 특정 상태에 있을 때만
    - a가 hover(마우스 포인터가 해당 태그 위에 있는 상태)일 때만 선택