# 변수

1. 변수
    - 변할 수 있는 데이터를 저장할 때 사용하는 저장소

    1. let
        - 최신 JS에서 변수를 만들기 위해 사용하는 키워드(명령어)
        ```javascript
        // 변수 선언
        let message;

        // 변수에 값을 넣어줌
        message = "hello!";

        // 변수에 있는 값을 보여줌
        alert(message);
        ```
        - 한 줄에 바로 값을 넣어줄 수 있음
        ```javascript
        // 변수 선언
        let message = "hello!";
        ```
        - 한 줄에 여러개의 변수를 선언할 수 있음
        ```javascript
        // 변수 선언
        let message1 = "hello1", message2 = "hello2", message3 = "hello3";
        ```
        - 변수이기 때문에 값을 바꿀 수 있음
        ```javascript
        // 변수 선언
        let message = "hello!";

        message = "hi!";

        alert(message); // result = hi!
        ```

    2. var
        - 예전 JS에서 변수를 저장하기 위해 만든 키워드(명령어)
        - let과 거의 비슷하게 동작
        - 

2. 상수
    - 변화하지 않는 데이터를 관리할 때 사용하는 키워드(명령어)
    - const
    ```javascript
    const message = "hello";
    message = "hi!"; // 변하지 않는 값이므로 에러
    ```

3. 변수 명명 규칙
    - 간결하며, 명확해야 함
    - 이름만으로 어떤 데이터를 담고 있는지 알 수 있어야 함
    - 변수명에는 문자, 숫자, $, _만 사용 가능
    - 첫 글자는 숫자를 넣어선 안 됨
    - JS에서 사용하는 키워드(명령어)는 사용할 수 없음(ex. let, class, return, function...)

