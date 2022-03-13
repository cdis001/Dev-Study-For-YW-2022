# 3. This
- JavaScript에서 함수에서 쓰이는 키워드
- 대부분의 경우 this의 값은 함수를 호출한 방법에 의해 결정
- 어디에서 어떻게 호출하느냐에 따라 값이 변함
- ES5에서는 함수를 어떻게 호출했는지 상관하지 않고 this 값을 설정할 수 있는 bind 메서드를 도입
- ES2015는 스스로의 this 바인딩을 제공하지 않는 화살표 함수를 추가
- 실행 컨텍스트(global, function)에서의 this는 비엄격 모드(non-strict)에서 항상 객체를 참조
- 엄격 모드에서는 어떠한 값이든 될 수 있음
- 함수 내부에서 this를 사용하는 경우에 따라 값이 바뀔 수 있음

## Globla에서의 this
- 전역 객체를 참조
```javascript
// 웹 브라우저에서는 window 객체가 전역 객체
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

## 단순 함수 호출
- 함수 내부에서 this의 값은 함수를 호출한 방법에 따라 다름
- 브라우저에서는 전역 객체인 window를 참조(non strict)
```javascript
function f1() {
  return this;
}

// 브라우저
f1() === window; // true

// Node.js
f1() === global; // true
```
- strict 모드에서의 this 값은 실행 문맥에 진입하며 설정되는 값을 유지
```javascript
function f2(){
  "use strict"; // 엄격 모드 참고
  return this;
}

f2() === undefined; // true
```

## 객체의 메소드(Method)
- 함수를 어떤 객체의 메소드로 호출하면 this의 값은 그 객체를 사용
- 함수를 객체 외부에서 선언하고, 객체 안에서 호출하는 경우에도 this는 해당 객체의 this를 참조
- 객체의 함수를 외부에서 호출할 때 this는 Window가 됨
```javascript
// 1. 객체 또는 클래스 안에서 메소드를 실행한다면 this는 Object 자기 자신
var man = {
    name: 'john',
    hello: function() {
        // 2. 객체이므로 this는 man을 가리킴
        console.log('hello ' + this.name);
    }
}
man.hello(); // 3. hello john

// 3. 일반 함수 welcome을 선언
function welcome() {
    // 4. 여기서 this는 전역 객체 Window이므로, 만약 실행시키면 undefined가 뜸
    console.log('welcome ' + this.name);
}

// 5. man 객체의 welcome 속성에 일반 함수 welcome을 추가
man.welcome = welcome;

// 6. welcome이 man 객체에서 호출되었으므로 welcome john이 출력됨
man.welcome();

// 7. man 객체의 thanks 속성에 함수를 선언
man.thanks = function () {
    // 8. man.thanks()를 호출하면 thanks john이 출력
    console.log('thanks ' + this.name);
}

// 8. 이 함수를 객체 외부에서 참조
var thankYou = man.thanks;

// 9. 객체 외부이므로 this가 Window 객체가 되어서 thanks (undefined)가 출력
thankYou();

// 10. 그럼 또 다른 객체에서 이 함수를 호출하면 어떻게 될까?
women = {
    name: 'barbie',
    thanks: man.thanks // 11. man.thanks 함수를 women.thanks에 참조
}

// 12. this가 포함된 함수가 호출된 객체가 women이므로 thanks barbie가 출력
women.thanks();
```

## 콜백 함수
- this가 Window를 가리킴
```javascript
// 1. 콜백함수
var object = {
    callback: function() {
        setTimeout(function() {
            console.log(this); // 2. this는 window
        }, 1000);
    }
}
```

## 생성자
- 함수를 new 키워드와 함께 생성자로 사용하면 this는 새로 생긴 객체에 묶임
- class를 이용해 작성할 수도 있음
- new 키워드를 붙이지 않을 경우 this가 해당 객체로 바인딩 되지 않기 때문에 Window 객체를 건드리는 일이 발생할 수 있음
```javascript
// 1. 클래스 역할을 할 함수 선언
function Man () {
    this.name = 'John';
}

// 2. 생성자로 객체 선언
var john = new Man();

// 3. this가 Man 객체를 가리키고 있어 이름이 정상적으로 출력된다
john.name; // => 'John'

// 1. Class Man 선언
class Man {
    constructor(name) {
        this.name = name;
    }
    hello() {
        console.log('hello ' + this.name)
    }
}

// 2. 생성자 실행
var john = new Man('John');
john.hello(); // 3. hello John 출력
```

## 화살표 함수(Arrow function)
- this를 외부 스코프에서 정적으로 바인딩된 문맥(정적 컨텍스트, Lexical context)을 가짐
- 정적 컨텍스트(Lexical context)는 소스코드가 작성된 그 문맥의 실행 컨텍스트나 호출 컨텍스트에 의해 결정
- 정적 컨텍스트는 함수가 실행된 위치가 아닌, 정의(defined)된 위치에서의 컨텍스트를 참조
```javascript
// 1. 화살표 함수
var obj = {
    a: this, // 2. 일반적인 경우 this는 window,
    b: function() {
      console.log(this) // 3. 메소드의 경우 this는 객체
    },
    c: () => {
        console.log(this)
        // 4. 화살표 함수의 경우 정적 컨텍스트를 가짐, 함수를 호출하는 것과 this는 연관이 없음
        // 5. 따라서 화살표 함수가 정의된 obj 객체의 this를 바인딩하므로 this는 window
    }

}

obj.b() // 6. obj
obj.c() // 7. window
```
- 화살표 함수는 this가 없기 때문에, 부모 스코프의 this를 바인딩하는데 위의 예시에서 이는 곧 Window객체를 의미

## DOM 이벤트 처리기
- 함수를 이벤트 처리기로 사용하면 this는 이벤트를 발사한 요소로 설정
```javascript
// 처리기로 호출하면 관련 객체를 파랗게 만듦
function bluify(e) {
  // 언제나 true
  console.log(this === e.currentTarget);
  // currentTarget과 target이 같은 객체면 true
  console.log(this === e.target);
  this.style.backgroundColor = '#A5D9F3';
}

// 문서 내 모든 요소의 목록
var elements = document.getElementsByTagName('*');

// 어떤 요소를 클릭하면 파랗게 변하도록
// bluify를 클릭 처리기로 등록
for (var i = 0; i < elements.length; i++) {
  elements[i].addEventListener('click', bluify, false);
}
```

## call(), apply(), bind()
- 다른 문맥의 this를 필요에 따라 변경할 수 있는 함수

1. call()
   - this와 매개변수들을 이용해 함수를 호출하는 방법
   - call()을 이용해 this를 대체할 수 있음
   ```javascript
   function Product(name, price) {
     this.name = name;
     this.price = price;
   }

   function Food(name, price) {
     Product.call(this, name, price);
     this.category = 'food';
   }

   console.log(new Food('cheese', 5).name);
   //"cheese"
   ```
   - 이미 할당되어있는 객체의 함수/메소드를 다른 객체의 값으로 재할당할때 사용
   - this는 현재 객체(호출하는 객체)를 참조
   - 새 객체를 위한 메소드를 재작성할 필요 없이 call()을 이용해 다른 객체에 상속할 수 있음
   > https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call
   - 다른 객체 대신 메소드를 호출하는데 사용
   ```javascript
   // 1. 이것은 객체의 메소드
   var man = {
       name: 'john',
       // 2. 객체의 메소드 안에서 함수를 선언하는 것이니까 내부 함수
       hello: function() {
           function getName() {
               // 3. 여기서 this가 무엇을 가리키고 있을까?
               return this.name;
           }
           // 4. 이번에는 call()을 통해 현재 문맥에서의 this(man 객체)를 바인딩해주었다
           console.log('hello ' + getName.call(this));
       }
   }

   // 이번에는 메소드를 실행시키면 john가 뜬다!
   // this가 man 객체로 바인딩 된 것을 확인할 수 있다
   man.hello();
   ```

   ```javascript
   var obj = {
     string: 'zero',
     yell: function() {
       alert(this.string);
     }
   };
   var obj2 = {
     string: 'what?'
   };
   obj.yell(); // 'zero';
   obj.yell.call(obj2); // 'what?'
   ```

2. apply()
   - call()과 비슷하지만, 매개변수를 하나씩 넣어주는 call과는 다르게 매개변수를 배열로 넣어줌
   ```javascript
   var obj = {
     string: 'zero',
     yell: function() {
       alert(this.string);
     }
   };
   var obj2 = {
     string: 'what?'
   };
   obj.yell(); // 'zero';
   obj.yell.call(obj2); // 'what?'
   ```

3. bind()
   - 함수가 가리키는 this만 바꾸고 호출하지는 않는 함수
   - 바인딩한 함수를 새롭게 만듦
   - 바인딩한 함수는 원본 함수 객체를 감싸는 함수
   ```javascript
   var obj = {
     string: 'zero',
     yell: function() {
       alert(this.string);
     }
   };
   var obj2 = {
     string: 'what?'
   };
   var yell2 = obj.yell.bind(obj2);
   yell2(); // 'what?'
   ```

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this
> https://wormwlrm.github.io/2019/03/04/You-should-know-JavaScript-this.html.html