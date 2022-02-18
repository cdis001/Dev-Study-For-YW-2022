# 함수
- 요청할 경우 실행할 수 있는 코드 모음
- 보통 동일한 작업을 여러번 수행해야 할 때 사용

## 선언
- 기본 선언식
```javascript
function 함수명(매개변수){
    코드들
}
```

- 예시
```javascript
// 함수 선언
function plusOne(n) {
    alert(n + 1);
}

// 함수 호출
plusOnd(1);
plusOnd(2);
```

## 변수
1. 지역 변수
    - 함수 내에서 선언한 변수
    - 함수 안에서만 사용할 수 있으며, 함수 밖에서는 사용 불가능
    ```javascript
    function abc() {
        let i = 1;
        alert(i);
    }

    abc(); // 1

    alert(i); // 에러
    ```

2. 전역 변수
    - 함수 외부에서 선언하여 어떤 함수나 변수에서도 호출할 수 있는 변수
    - 함수에서 접근할 수 있으며, 값을 수정하는 것도 가능
    ```javascript
    let i = 1
    function abc() {
        i = 2;
    }

    alert(i); // 1

    abc();

    alert(i); // 2
    ```
3. 매개 변수
    - 함수를 실행할때 필요한 변수
    - 함수를 선언할 때 같이 선언함
    ```javascript
    function helloMessage(text) {
        alert("hello " + text);
    }

    helloMessage("world") // hello world
    helloMessage() // 에러
    ```

## 반환
1. 반환값(return)
    - 함수를 실행한 뒤 특정 값을 전달하고 싶을때 쓰임
    ```javascript
    function sum(a, b) {
        return a + b;
    }

    let result = sum(1, 2);
    alert(result) // 3
    ```
    - return문이 있는 위치에서 함수가 바로 종료됨
    - 아무런 값을 전달하지 않아도 됨. 
    ```javascript
    function sum(a, b) {
        return;
        alert(a + b); // 실행되지 않음
    }

    let result = sum(1, 2);
    alert(result) // null
    ```

    ## 함수 표현
    - js에서는 함수도 변수로 넣을 수 있음
    - 함수를 변수로 넣을 경우에는, 함수 표현식을 사용해야 함
    ```javascript
    // 기존 함수 선언문은 함수의 이름을 줬지만, 함수 표현식의 경우에는 변수명이 함수의 이름이 되므로 함수명은 생략
    let sum = function(a, b) {
        return a + b
    }
    ```
    - 화살표 함수(arrow function)
        - 함수 표현식보다 간단히 함수 표현 가능
        - 아래와 같이 풀어서 표현할 수도 있고
        ```javascript
        let sum = (a, b) => {
            return a + b
        }
        ```
        - 아래와 같이 축약해서 표현할 수도 있음
        ```javascript
        let sum = (a, b) => a + b
        ```
        - 본문이 여러줄일 경우엔, 축약해서 표현할 수 없음