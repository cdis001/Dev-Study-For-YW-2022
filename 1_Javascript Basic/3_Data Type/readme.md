# 데이터 타입
- 프로그래밍 언어에서 사용할 수 있는 데이터의 종류
- JS는 느슨한 타입(loosely typed)의 동적(dynamic) 언어이므로, 변수가 어떠한 특정 타입과 연결되지 않으므로, 변수를 선언한 뒤에 다른 데이터 타입으로 변경할 수 있음
```javascript
let isTrue = true;

isTrue = 123; //가능
```

```java
boolean isTrue = true;

isTrue = 123 // 불가능
```

1. 원시 타입(Primitive data type)
    - 로우 레벨 언어에서 직접 표현하는 데이터 타입

    1. Boolean
        - 논리형 데이터 타입
        - 참(true), 거짓(false) 값만 있음
        - 0, -1, null, false, ""(빈 문자열), undefined...는 false(거짓)으로 구분

    2. Null
        - 변수에 값이 없을 때 사용하는 타입

    3. Undefined
        - 변수에 값이 존재하지 않을 때 사용되는 타입
        - null은 값이 없을때, undefined는 값이 존재하지 않을때 사용

    4. Number
        - 숫자형 데이터 타입
        - +, -, *, / 등의 연산 가능

    5. String
        - 문자형 데이터 타입
        - +를 이용하여 문자열을 이어붙이는 연산 가능

    6. Symbol 
        - 다른 값과 중복되지 않는 고유값
        - 최신 JS에서 나온 새로운 데이터 타입
        - 유일한 키 값을 만들때 사용
        ```javascript
        const a = Symbol(1)
        const b = Symbol(2)

        alert(a === b); // false
        ```

2. 객체 타입
    - 원시 타입을 제외한 나머지 값
    - 객체는 직접 호출이 되지 않으므로 참조에 의해 전달됨(call by reference)

