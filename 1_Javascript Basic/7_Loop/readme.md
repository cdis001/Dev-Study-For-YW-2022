# 반복문
- 여러 동작을 반복해야 할 때 사용
- 동일한 동작을 여러번 반복할때 사용됨

## while문
- 기본식
```javascript
while (조건문) {
  // 코드
  // '반복문 본문(body)'이라 불림
}
```
- 예시
```javascript
let i = 0;
while (i < 3) { // 0, 1, 2가 출력됩니다.
  alert( i );
  i++;
}
```
- 조건문이 true일 경우에, 반복문의 본문이 실행됨
- 조건문을 true로 설정할 경우, 반복문이 영원히 실행됨

## do-while문
- 기본식
```javascript
do {
  // 반복문 본문
} while (조건문);
```
- 예시
```javascript
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```
- 본문을 실행한 뒤, 조건문을 판별하여 true일 경우에 반복함
- 본문을 최소한 한번이라도 실행하고 싶을 때 사용


## for문
- 기본 선언식
```javascript
for (선언문; 조건문; step) {
  // ... 반복문 본문 ...
}
```

- 예시
```javascript
// 0부터 4까지 반복해서 보여짐
for (let i = 0; i < 5; i++) {
  alert(i);
}
```

- 선언문
    - for문 진입시 한 번 실행됨
    - 주로 변수를 선언하여 초기화 할 때 사용

- 조건문
    - 매 반복마다 평가하는 조건
    - 조건문의 결과값이 false라면 for문을 종료함

- step
    - 반복문의 본문이 끝난 뒤 실행되는 식
    - 주로 변수의 값을 증감할때 사용

- 순서
    1. 선언문에서 변수를 선언함
    2. 조건문을 판별함
    3. 조건문이 true일 경우, 본문 실행
    4. 본문 실행 후 step 실행
    5. 이후 2 ~ 4 번 반복 실행 후 조건문이 false일 경우 멈춤

- 조건을 미리 정의하거나 필요 없을 경우 조건문 생략 가능
```javascript
let i = 0
for(; i < 5; i++) {
    alert(i);
}
```
- step도 생략 가능
```javascript
let i = 0
for(; i < 5;) {
    alert(i);
    i++
}
```
- 조건문도 생략 가능하나, 조건문이 전혀 없을 경우 영원히 반복
```javascript
// 계속 0만 출력함
let i = 0
for(;;;) {
    alert(i);
}
```

## Break, Continue

1. break
    - 반복문을 종료하는 명령어
    ```javascript
    let sum = 0;

    while (true) {

    let value = +prompt("숫자를 입력하세요.", '');

    if (!value) break; // (*)

    sum += value;

    }
    alert( '합계: ' + sum );
    ```
    - 위 함수의 경우, value가 없을 경우 반복문을 종료함

2. contiune
    - 현재 반복문을 넘기는 명령어
    ```javascript
    for (let i = 0; i < 10; i++) {

    // 조건이 참이라면 남아있는 본문은 실행되지 않습니다.
    if (i % 2 == 0) continue;

    alert(i); // 1, 3, 5, 7, 9가 차례대로 출력됨
    }
    ```
    - 위 함수의 경우, i가 짝수일 경우에는 숫자를 호출하지 않고 넘어감
