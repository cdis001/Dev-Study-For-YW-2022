# 연산자

1. 기본 연산자
    - 가장 기본적인 연산자

    1. +
        - 덧셈 연산자
        - 숫자값을 더하거나, 문자열끼리 이어 붙일때도 사용
        ```javascript
        alert(1 + 2); // 3
        ```

    2. -
        - 뺄셈 연산자
        ```javascript
        alert(1 - 1); // 0
        ```

    3. *
        - 곱셈 연산자
        ```javascript
        alert(1 * 2); // 2
        ```

    4. /
        - 나눗셈 연산자
        ```javascript
        alert(2 / 2); // 1
        ```

    5. %
        - 나머지 연산자
        ```javascript
        alert(3 % 2); // 1
        ```

    6. **
        - 거듭제곱 연산자
        ```javascript
        alert(2 ** 3); // 8
        ```

    7. =
        - 할당 연산자
        - 값을 할당할 때(변수에 넣어줄 때) 사용
        ```javascript
        let one = 1;
        
        alert(one); // 1
        ```

    8. 복합 할당 연산자
        - 복합 할당 연산자
        - +=. -=. /=, *= 처럼 하나의 연산자 + 할당 연산자 조합으로 쓰임
        ```javascript
        let n = 1

        n = n + 1 
        alert(n) // 2
        ```
        ```javascript
        let n = 1

        n += 1 
        alert(n) // 2
        ```

    9. 증가, 감소 연산자
        1. ++
            - 증가 연산자
            - 변수를 1 증가 시켜줌
            ```javascript
            let n = 1;
            n++
            
            alert(n) // 2
            ```

        2. --
            - 감소 연산자
            - 변수를 1 감소시킴
            ```javascript
            let n = 1;
            n--
            
            alert(n) // 0
            ```
        - 증가, 감소 연산자의 순서에 따라 전위형, 후위형으로 나뉨
        ```javascript
        // 전위형 증가 연산
        let n = 1;
        alert(++n) // 2

        // 후위형 증가 연산
        let n = 1;
        alert(n++) // 1
        ```
        - 전위형의 경우, 증가/감소 후의 값을 전달
        - 후위형의 경우, 증가/감소 전의 값을 전달

        - 아래 코드에서 a, b, c, d의 값은?
        ```javascript
        let a = 1, b = 1;

        let c = ++a; // ?
        let d = b++; // ?
        ```
        <details>
          <summary>정답</summary>
          <div markdown="1">
           a = 2
           <br />
           b = 2
           <br />
           c = 2
           <br />
           d = 1
          </div>
        </details>

    10. 비트 연산자
        - 이진 연산을 수행할 때 사용하는 연산자
        - 이진 연산을 수행할 때 사용하므로, 흔히 쓰이진 않음
        - 설명이 길어지므로 우선 생략
        > https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators

2. 비교 연산자
    - boolean형 반환
    1. <, >
        - 초과, 미만 
    2. \>=, <=
        - 이상, 이하
    3. ==, ===
        - 같음
        - ===는 좀 더 엄격히 검사함
        ```javascript
        const a = 1;
        const b = "1";

        alert(a == b); //true
        alert(a === b); //false
        ```
    4. !=, !==
        - 같지 않음
        - not 연산자를 !로 표현
    

3. 논리 연산자
    - boolean형 반환
    1. ||
        - or
        - 둘 중 하나가 true 일 경우 true 반환
        ```javascript
        alert( true || true );   // true
        alert( false || true );  // true
        alert( true || false );  // true
        alert( false || false ); // false
        ```
    2. &&
        - and
        - 두개가 모두 true일 경우 true 반환
        ```javascript
        alert( true && true );   // true
        alert( false && true );  // false
        alert( true && false );  // false
        alert( false && false ); // false
        ```
    3. !
        - not
        - 값을 boolean으로 변환 후 반대 값을 반환
        ```javascript
        alert(!true) // false
        alert(!false) // true
        ```
