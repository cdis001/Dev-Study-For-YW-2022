# 1. 객체
- 원시형이 아닌 데이터 타입
- 다양한 데이터를 담을 수 있음
- JS에선 객체는 중괄호 {…}를 이용해 만들 수 있음
- 중괄호 안에는 ‘키(key): 값(value)’ 쌍으로 구성된 프로퍼티(property) 를 여러 개 넣을 수 있는데, 키엔 문자형, 값엔 모든 자료형이 허용
- 선언 방법
```javascript
let user = new Object(); // '객체 생성자' 문법
let user = {};  // '객체 리터럴' 문법

// 프로퍼티 값 얻기
alert( user.name ); // John
alert( user.age ); // 30

// 프로퍼티 추가
user.isAdmin = true;

// 프로퍼티 삭제
delete user.age;
```
- ‘키: 값’ 쌍으로 구성된 프로퍼티가 들어감
- 마지막 프로퍼티 끝은 쉼표로 끝날 수 있음
- 키값이 공백 없는 단어일 경우에는 "" 생략
```javascript
let user = {
    name: "john",
    age: "john",
}
```
- 배열처럼 []를 이용하여 값을 가져올 수 있음(key값이 공백이 있는 경우 주로 사용)
```javascript
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]); // true

// delete
delete user["likes birds"];
```
- 대괄호 표기법을 사용하면 변수를 키로 사용할 수 있음(.으로 가져오는건 불가능)
```javascript
let key = "likes birds";

// user["likes birds"] = true; 와 같습니다.
user[key] = true;
```
- 이름과 값이 변수의 이름과 동일하다면, 프로퍼티 값 단축 구문(property value shorthand) 을 사용할 수 있음
```javascript
function makeUser(name, age) {
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
    // ...
  };
}

// 객체를 선언 할 때도 사용 가능
let user = {
  name,  // name: name 과 같음
  age: 30
};
```
- 연산자 in을 사용하면 프로퍼티 존재 여부를 확인할 수 있음
```javascript
let user = { name: "John", age: 30 };

alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.
```
- in 연산자는 for문으로도 사용 가능
```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // 키
  alert( key );  // name, age, isAdmin
  // 키에 해당하는 값
  alert( user[key] ); // John, 30, true
}
```