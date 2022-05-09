# 3. 스코프

- 현재 실행되는 코드의 범위
- javascript에는 글로벌(전역) 스코프, 로컬(지역) 스코프 2가지 타입이 있음
- 모든 변수는 스코프를 가지므로, 선언 위치에 따라 전역, 지역 변수로 나뉘게 됨
- Javascript는 블록 레벨 스코프(Block-level Scope)와 함수 레벨 스코프(function-level scope)를 둘 다 따르게 할 수 있음 
- 함수 레벨 스코프란 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않다
- 블록 레벨 스코프란, 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없음

## Global Scope
- 전역에 선언되어있어 어느 곳에서든지 해당 변수에 접근할 수 있다는 의미
- 전역변수를 만드는 일은 지양하는 것이 좋음
- 다른 라이브러리들을 사용하면서 변수 이름이 겹치게 되면 충돌날 수 있기 때문
```javascript
var global = 'global';

function foo() {
  var local = 'local';
  console.log(global);
  console.log(local);
}
foo();

console.log(global);
console.log(local); // Uncaught ReferenceError: local is not defined
```

## Local Scope
- 해당 지역에서만 접근할 수 있어 지역을 벗어난 곳에선 접근할 수 없다는 의미
```javascript
{
  // 지역 변수를 선언하고 몇 가지 조작을 했지만 그 결과를 밖에서 볼 수 없습니다.

  let message = "안녕하세요."; // 블록 내에서만 변숫값을 얻을 수 있습니다.

  alert(message); // 안녕하세요.
}

alert(message); // ReferenceError: message is not defined
```

## let, const, var
- 기본적으로 let, var은 변수 / const는 상수로 구별한다.
- var는 초기 자바스크립트 구현 방식 때문에 let과 const로 선언한 변수와는 다른 방식으로 동작
- var는 코드 블록을 무시하기 때문에 전역 변수로 선언 할 수 있음
- var 선언은 함수가 시작될 때 처리됨
```javascript
function sayHi() {
  phrase = "Hello";

  alert(phrase);

  var phrase;
}
sayHi();
```
```javascript
function sayHi() {
  var phrase;

  phrase = "Hello";

  alert(phrase);
}
sayHi();
```
```javascript
function sayHi() {
  phrase = "Hello"; // (*)

  if (false) {
    var phrase;
  }

  alert(phrase);
}
sayHi();
```
- 위의 3가지 코드는 모두 동일하게 동작함
- 이렇게 변수가 끌어올려 지는 현상을 '호이스팅(hoisting)'이라 함
  - 호이스팅(hoisting)
     - hoist, 끌어올리다
     - 코드 실행 전, 변수를 미리 정의하는 과정
     > https://developer.mozilla.org/ko/docs/Glossary/Hoisting
- 기존 Javascript는 함수 레벨 스코프를 따랐지만, 최신 Javascript의 let, const를 사용한다면 블록 레벨 스코프(block-level scope)를 사용할 수 있음

## 중첩 함수
- 함수 내부에서 선언한 함수는 ‘중첩(nested)’ 함수라고 함
```javascript
function sayHiBye(firstName, lastName) {

  // 헬퍼(helper) 중첩 함수
  // 외부 변수에 접근해 이름 전체를 반환해줌
  function getFullName() {
    return firstName + " " + lastName;
  }

  alert( "Hello, " + getFullName() );
  alert( "Bye, " + getFullName() );

}
```
- 중첩 함수는 새로운 객체의 프로퍼티 형태나 중첩 함수 그 자체로 반환될 수 있음

## 스코프 체인(scope chain)
- 내부 함수에서는 외부 함수의 변수에 접근 가능하지만 외부 함수에서는 내부 함수의 변수에 접근할 수 없음
```javascript
var name = 'zero';
function outer() {
  console.log('외부', name);
  function inner() {
    var enemy = 'nero';
    console.log('내부', name);
  }
  inner();
}
outer();
console.log(enemy); // undefined
```
- inner 함수는 name 변수를 찾기 위해 먼저 자기 자신의 스코프에서 찾고, 없으면 한 단계 올라가 outer 스코프에서 찾고, 없으면 다시 올라가 결국 전역 스코프에서 찾음
- 만약 전역 스코프에도 없다면 변수를 찾지 못하였다는 에러 발생
- 이렇게 꼬리를 물고 계속 범위를 넓히면서 찾는 관계를 스코프 체인이라 함

## 렉시컬 스코핑(lexical scoping)
- 스코프는 함수를 호출할 때가 아니라 선언할 때 생김
```javascript
var name = 'zero';
function log() {
  console.log(name);
}

function wrapper() {
  var name = 'nero';
  log();
}
wrapper(); // zero
```
- 함수를 처음 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳(상위 범위에서)에 있는 변수를 계속 참조
- 위의 예시에서는 log 함수 안의 name 변수는 선언 시 가장 가까운 전역변수 name을 참조하므로 전역변수 name의 값인 zero가 나옴
- 이런 것을 lexical scoping이라고 함


## 참조
> https://www.zerocho.com/category/JavaScript/post/5740531574288ebc5f2ba97e

> https://ko.javascript.info/closure

> https://hanamon.kr/javascript-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%EB%B3%80%EC%88%98%EC%84%A0%EC%96%B8%ED%82%A4%EC%9B%8C%EB%93%9C-%EC%B0%A8%EC%9D%B4%EC%A0%90/