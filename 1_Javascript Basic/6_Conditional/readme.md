# 조건문
- 조건에 따라 다른 계산을 해야할 때 사용

## if-else 문
- 기본 선언식
```javascript
if(조건문) {
    코드
} else {
    코드
}
```

- 예시
```javascript
let age = 19;

if(age > 19) {
    alert("성인입니다.")
} else {
    alert("미성년자 입니다.")
}
```

- if문의 괄호 안의 조건문이 true일 경우 if문 블록 안의 코드가 실행됨
- if문의 조건문이 false일 경우, else문 블록 안의 코드가 실행됨
- else문은 넣어도 되고 안 넣어도 됨
- 여러가지 조건을 판별해야 할 때, else if문을 사용하여 더 세밀한 조건 연산 가능

```javascript
let age = 19

if(age > 19) {
    // age 값이 19 초과인지 확인 => 19 초과가 아님, 넘어감
    // 만약 age 값이 30이라면 아래 코드를 실행한 뒤 종료함
    alert("성인입니다.")
} else if(age === 19) {
    // age 값이 19인지 확인 => age 값이 19임, 코드 실행
    alert("고3 입니다.")
} else {
    alert("미성년자 입니다.")
}
```

## switch문
- 기본 선언식
```javascript
switch(x) {
  case 'value1':
    x = "value01";
    break;

  case 'value2':
    x = "value02";
    break;

  default:
    x = "default";
    break;
}
```
- if-else문으로 표현한다면 아래와 같다
```javascript
if(x === "value1") {
    x = "value01";
} else if(x === "value2") {
    x = "value02";
} else {
    x = "default";
}
```
- 변수 x의 값과 첫 번째 case문의 값 'value1'를 일치하는지 비교한 후, 두 번째 case문의 값 'value2'와 비교. 해당 과정 반복
- case문에서 변수 x의 값과 일치하는 값을 찾으면 해당 case 문의 아래의 코드가 실행 됨. 이때, break문을 만나거나 switch 문이 끝나면 코드의 실행은 멈춤. (break문이 없으면 계속 실행됨)
- 값과 일치하는 case문이 없다면, default문 아래의 코드가 실행(default 문이 있는 경우)

## 삼항 연산
- 기본 선언식
```javascript
(조건문) ? (true일 때 값) : (false일 때 값)
```

- 예시
```javascript
let age = 19;
let adult = (age > 19) ? "성인" : "미성년자"

alert(adult) // 미성년자
```
- 조건문의 값이 true일때 첫번째 값이, false일때 : 뒤의 값이 나옴
- 여러개 연결하여 복수의 조건을 처리할 수 있음