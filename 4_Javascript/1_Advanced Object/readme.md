# 1. 객체 심화

## 객체 개념
- 데이터와 함수의 집합
- 객체 내부에 있는 데이터는 프로퍼티(요소)라고 하며, 함수는 메소드라고 함
- 프로퍼티는 이름(name)과 값(value)으로 구성
- 객체를 이용해 만든 값을 인스턴스라고 함
- 객체 예시
```javascript
var cat = "나비"; // 일반적인 변수의 선언

// 객체도 많은 값을 가지는 변수의 하나임.

var kitty = { name: "나비", family: "코리안 숏 헤어", age: 1, weight: 0.1 };

cat          // 나비

kitty.name   // 나비
```
- 프로퍼티 참조
```javascript
// 객체이름.프로퍼티이름
// 객체이름["프로퍼티이름"]
var person = {

    name: "홍길동",      // 이름 프로퍼티를 정의함.

    birthday: "030219",  // 생년월일 프로퍼티를 정의함.

    pId: "1234567",      // 개인 id 프로퍼티를 정의함.

    fullId: function() { // 생년월일과 개인 id를 합쳐서 주민등록번호를 반환함.

        return this.birthday + this.pId;

    }

};

person.name    // 홍길동

person["name"] // 홍길동
```

- 메소드 참조
```javascript
// 객체이름.메소드이름()

var person = {

    name: "홍길동",

    birthday: "030219",

    pId: "1234567",

    fullId: function() {

        return this.birthday + this.pId;

    }

};

person.fullId() // 0302191234567

person.fullId;  // function () { return this.birthday + this.pId; } 
```

## call by reference
- 객체는 원시값과는 달리 참조에 의해 저장되며 복사됨
- 예시
```javascript
// 원시값의 경우
const a = "123";
const b = "123";

alert(a === b); // true
```
```javascript
// 객체의 경우
let a = {};
let b = {}; // 독립된 두 객체

alert( a == b ); // false
alert( a === b ); // false
```
- 객체의 경우 컴퓨터의 메모리 내부에 저장될 때 객체가 그대로 저장되는 것이 아니라, 객체가 저장되어있는 '메모리 주소’인 객체에 대한 '참조 값’이 저장
- 같은 값을 저장한 객체더라도 메모리의 주소가 서로 다르기 때문에 비교시 같지 않다고 나옴
- 메모리 주소를 직접 복사한다면 비교시 같은 객체로 나옴
```javascript
let a = {};
let b = a; // 참조에 의한 복사

alert( a == b ); // true, 두 변수는 같은 객체를 참조합니다.
alert( a === b ); // true
```
- 위 객체를 서랍장에 비유하면 변수(a, b)는 서랍장을 열 수 있는 열쇠라고 할 수 있다. 서랍장(객체의 값)은 하나, 서랍장을 열 수 있는 열쇠(변수)는 두 개인데, 그중 하나를 사용해 서랍장을 열어 정돈한 후, 또 다른 열쇠로 서랍장을 열면 정돈된 내용을 볼 수 있음

## OOP 기초
- 프로그램 내에서 표현하고자 하는 실 세계(real world)의 일들을 객체를 사용해서 모델링 하고, 객체를 사용하지 않으면 불가능 혹은 어려웠을 일들을 쉽게 처리하는 방법을 제공
- 모델링하고자 하고자 하는 일이나 기능 혹은 필요한 행동들을 표현하는 프로그램 코드와 그와 연관된 데이터로 구성
- 객체는 데이터를 감싸서 객체 패키지안에 보관
- 객체는 네트워크를 통해 쉽게 전송될 수 있도록 데이터를 저장하는 용도로도 많이 사용
- 객체 지향 프로그래밍의 4가지 특징
   - 추상화
      - 프로그래머의 의도에 맞추어 가장 중요한 것들만을 뽑아서 복잡한 것들을 보다 단순한 모델로 변환하는 작업

   - 상속
      - 부모 객체의 특징을 물려받는 것
      - 부모가 가진 속성이나 메서드를 그 자식이 부모의 속성이나 메서드를 상속받아 가질 수 있음
      - 자바스크립트에서는 현재 존재하고 있는 객체를 프로토타입으로 사용하여, 해당 객체를 복제하여 재사용하는 것을 상속이라고 함


   - 캡슐화
      - 속성이나 기능을 하나로 묶어 객체로 정의하고 객체 안에서 정의된 속성은 해당 객체에서만 접근이 가능
      - 이는 클래스(class)라는 개념으로 구현
      - 캡슐화의 개념에는 "은닉화"의 특징도 포함
      - 프로그램의 세부적인 구현을 외부로 드러나지 않도록 감추는 것

   - 다형성
      - 객체의 변수나 메서드가 상황에 따라 다른 의미로 해석될 수 있는 것

## 객체 프로토타입
- JS는 다른 객체 지향 언어와는 달리 class 기반 언어가 아닌 프로토타입 기반 언어임(객체 지향 언어는 아님)
- 명령형(imperative), 함수형(functional), 프로토타입 기반(prototype-based) 객체지향 언어
- 자바스크립트의 모든 객체는 프로토타입(prototype)이라는 객체를 가지고 있음
- 자바스크립트의 모든 객체는 최소한 하나 이상의 다른 객체로부터 상속을 받으며, 이때 상속되는 정보를 제공하는 객체를 프로토타입(prototype)이라 함

## 프로토타입 체인(prototype chain)
- 객체 이니셜라이저를 사용해 생성된 같은 타입의 객체들은 모두 같은 프로토타입을 가짐
- new 연산자를 사용해 생성한 객체는 생성자의 프로토타입을 자신의 프로토타입으로 상속 가능
```javascript
var obj = new Object(); // 이 객체의 프로토타입은 Object.prototype

var arr = new Array();  // 이 객체의 프로토타입은 Array.prototype

var date = new Date();  // 이 객체의 프로토타입은 Date.prototype
```

- 하지만 Object.prototype 객체는 어떠한 프로토타입도 가지지 않으며, 아무런 프로퍼티도 상속받지 않음
- 자바스크립트에 내장된 모든 생성자나 사용자 정의 생성자는 바로 이 객체를 프로토타입으로 가짐
```javascript
var date = new Date(); // 이 객체는 Date.prototype 뿐만 아니라 Object.prototype도 프로토타입으로 가집니다
```

### 프로토타입의 생성
- 객체 생성자 함수(object constructor function)를 작성하여 같은 프로토타입을 가지는 객체들을 생성
```javascript
function Dog(color, name) { // 개에 관한 생성자 함수를 작성함.

    this.color = color;          // 색에 관한 프로퍼티

    this.name = name;            // 이름에 관한 프로퍼티

}

var myDog = new Dog("흰색", "찰스"); // 이 객체는 Dog라는 프로토타입을 가짐.

alert("우리 집 강아지는 " + myDog.name + "라는 이름의 " + myDog.color + " 털이 매력적인 강아지입니다.");
```

### 객체에 프로퍼티 및 메소드 추가
```javascript
function Dog(color, name) {

    this.color = color;

    this.name = name;

}

var myDog = new Dog("흰색", "찰스");

myDog.family = "포메라니안"; // 품종에 관한 프로퍼티를 추가함.

myDog.breed = function() {        // 털색을 포함한 품종을 반환해 주는 메소드를 추가함.

    return this.color + " " + this.family;

}

alert("우리 집 강아지는 " + myDog.breed() + "입니다.");
```
- 새롭게 추가된 family 프로퍼티와 breed() 메소드는 오직 myDog 인스턴스에만 추가

### prototype 프로퍼티
```javascript
function Dog(color, name, age) {

    this.color = color;

    this.name = name;

    this.age = age;

}

// 현재 존재하고 있는 Dog 프로토타입에 family 프로퍼티를 추가함.

Dog.prototype.family = "시베리안 허스키";

// 현재 존재하고 있는 Dog 프로토타입에 breed 메소드를 추가함.

Dog.prototype.breed = function() {

    return this.color + " " + this.family;

};

var myDog = new Dog("흰색", "마루", 1);

var hisDog = new Dog("갈색", "콩이", 3);

 

alert("우리 집 강아지는 " + myDog.family + "이고, 친구네 집 강아지도 " + hisDog.family + "입니다.");

alert("우리 집 강아지의 품종은 " + myDog.breed() + "입니다.<br>");

alert("친구네 집 강아지의 품종은 " + hisDog.breed() + "입니다.");
```

## 그 외 객체 생성 방법

### Literal
- 가장 간단하게 변수에 직접 객체를 작성해 넣는 것
- 방법
```javascript
const headphone = {
  volume: 0,
  volumeUp: function() {
    if (this.volume < 10) {
      this.volume++;
    }
  },
  volumeDown: function () {
    if (this.volume > 0) {
      this.volume--;
    }
  }
};
```
- 간단하게 작성할 수 있으나, 외부에서 내부 속성에 접근할 수 있기 때문에 객체의 기능을 임의로 조작할 수 있음
- 생성자 함수(new) 사용과는 달리 대량 생산에 어려움이 있을 수 있음

### ES6 class
- ES6부터 class라는 개념이 등장하여 다른 객체 지향 언어처럼 사용 가능
- 단, 작성법이 달라졌을 뿐 prototype과 크게 다르지 않음
- 방법
```javascript
// 오디오 객체
class Audio {
  constructor() {
    this.volume = 0;
    this.power = false;
  }
  
  volumeUp = function () {
    if (this.volume < 10) {
      this.volume++;
    }
  }
    
  volumeDown = function () {
    if (this.volume > 0) {
      this.volume--;
    }
  }
}

// 오디오 객체를 상속받은 헤드폰 객체
// extends는 상속 할 때 쓰이는 명령어
class Headphone extends Audio {
  constructor(props) {
    super(props);
    
    this.noiseCancelling = false;
  }
  
  setNoiseCancelling = function () {
    this.noiseCancelling = !this.noiseCancelling;
  }
}

// 오디오 객체를 상속 받은 에어팟 객체
class AirPod extends Audio {
  constructor(props) {
    super(props);
    
    this.pairingConnected = false;
  }
  
  pairingConnect = function () {
    this.pairingConnected = !this.pairingConnected;
  }
}
```
- 함수 선언과 클래스 선언의 중요한 차이점은 함수의 경우 정의하기 하기 전에 호출할 수 있지만, 클래스는 반드시 정의한 뒤에 사용할 수 있다는 점
- 최근 JS에서는 OOP보다는 함수형 프로그래밍을 주로 이용함