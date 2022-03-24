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

## Float
- 한 요소(element)가 보통의 흐름(normal flow)으로부터 빠져 텍스트 및 인라인(inline) 요소가 그 주위를 감싸는 자기 컨테이너의 좌우측을 따라 배치되어야 함을 지정
- position 속성의 absolute와 같이 쓸 수 없음
- 이미지에 텍스트를 둘러싸게 만들려는 목표로 나온 기법

- 설명
   > https://developer.mozilla.org/ko/docs/Web/CSS/float

   > https://css-tricks.com/all-about-floats/

### clear 속성
- float 속성이 적용된 이후 나타나는 요소들의 동작을 조절
- float 속성이 적용된 후 나타나는 요소들이 더 이상 float 속성에 영향을 받지 않도록 설정
- 일부 속성에 float 속성이 적용되지 않아야 할 때 사용

### overflow
- 내용(content)의 크기가 해당 요소를 감싸고 있는 컨테이너 요소보다 클 때 어떻게 처리할지를 설정
- overflow-x를 이용해 박스가 수평(가로)방향의 크기를 넘길 때 어떻게 해야할 지 설정할 수 있음
- overflow-y를 이용해 박스가 수직(세로)방향의 크기를 넘길 때 어떻게 해야할 지 설정할 수 있음

## Positioning
- HTML 문서 상에서 요소가 배치되는 방식을 결정
- 요소의 정확한 위치 지정을 위해서 top, left, bottom, right 속성과 함께 사용

- 설명
   > https://developer.mozilla.org/ko/docs/Web/CSS/position

   > https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/

### static
- 기본값
- 속성을 지정하지 않을 경우의 position값
- top, left, bottom, right, z-index등이 아무런 영향도 주지 않음

### relative
- 원래 위치를 기준으로 상대적(relative)으로 배치
- 자기 자신을 기준으로 top, right, bottom, left의 값에 따라 위치 변경
- 다른 요소에는 영향을 주지 않음

### absolute
- 요소를 일반적인 문서 흐름에서 제거하고, 페이지 레이아웃에 공간도 배정하지 않음
- 배치 기준을 자신이 아닌 상위 요소에서 찾음
- 가장 가까운 위치 지정 조상 요소에 대해 상대적으로 배치
- 조상 중 위치 지정 요소가 없다면 초기 컨테이닝 블록을 기준

### fixed
- 브라우저 화면의 특정 부분에 고정함
- 배치 기준은 브라우저 전체 화면(viewport)

### sticky
- 일반적인 문서 흐름에 따라 배치하고, 테이블 관련 요소를 포함해 가장 가까운, 스크롤 되는 조상과, 가장 가까운 블록 레벨 조상을 기준으로 top, right, bottom, left의 값에 따라 오프셋을 적용
- static과 fixed 속성의 특징을 모두 가지고 있는 속성
- sticky 영역의 x 또는 y 위치값이 설정한 위치에 도달하기 전까지는 static, 도달 이후에는 fixed의 기능을 함

## Dispaly
- 요소를 어떻게 보여줄지를 결정

- 설명
   > http://www.tcpschool.com/css/css_position_display

   > https://ofcourse.kr/css-course/display-%EC%86%8D%EC%84%B1

   > https://www.freecodecamp.org/news/the-css-display-property-display-none-display-table-inline-block-and-more/

### none
- 요소가 보이지 않음

### block
- 언제나 새로운 라인(line)에서 시작하며, 해당 라인의 모든 너비를 차지
- 

### inline
- 새로운 라인(line)에서 시작하지 않음
- 요소의 너비도 해당 라인 전체가 아닌 해당 HTML 요소의 내용(content)만큼만 차지

### inline-block
- block과 inline의 중간 형태
- 줄 바꿈이 되지 않지만 크기를 지정 할 수 있음

## Box Model
> https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/The_box_model

## Flex
> https://flexboxfroggy.com/#ko

## Gird
> https://cssgridgarden.com/#ko