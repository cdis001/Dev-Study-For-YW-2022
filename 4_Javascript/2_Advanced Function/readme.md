# 2. 함수 심화

## 일급 객체
- 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체
- 함수에 인자로 넘기기, 함수의 결과로 반환하기, 변수에 대입하기가 가능할 경우 일급 객체로 분류됨
- 자바스크립트에서는 일반 자료형 뿐만 아니라 함수도 일급 객체로 취급함

```javascript
// 함수의 인자로 함수 넘기기
function mul(num) { return num * num }

function mulNum(func, number) { // func가 파라미터로 받음
  return func(number);
}

// 함수의 결과로 반환하기
function add(num1) {
  return function (num2) {
    return num1 + num2;
  }
}

add(3)(4);

// 변수에 대입하기
const square = function (num) {
  return num*num;
}
```

## 고차함수
- 함수를 인자로 받거나 또는 함수를 반환함으로써 작동 하는 함수
- 매개변수를 함수로 받는 함수 이거나, 반환값(return)이 함수인 함수
- 자바스크립트가 제공해주는 대표적인 고차 함수로는 Array.prototype.map, Array.prototype.filter, Array.prototype.reduce가 있음
- Array.prototype.map
   - 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환
   - 배열의 요소를 일괄적으로 변경하는데 효과적
   ```javascript
   // 고차함수(map)를 사용하지 않을 경우
   const arr1 = [1, 2, 3];
   const arr2 = [];

   for(let i=0; i<arr1.length; i++) {
     arr2.push(arr1[i] * 2);
   }

   // prints [2, 4, 6]
   console.log(arr2);
   ```
   ```javascript
   // 고차함수(map)를 사용했을 경우
   const arr1 = [1, 2, 3];

   const arr2 = arr1.map(function(item) {
      return item * 2;
   });

   console.log(arr2);
   ```
   ```javascript
   // 고차함수(map) + 화살표 함수를 사용했을 경우
   const arr1 = [1, 2, 3];
   const arr2 = arr1.map(item => item * 2);
   console.log(arr2);
   ```

- Array.prototype.filter
   - 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환
   - 배열의 요소 중에서 특정 조건을 만족하는 요소들만을 걸러내는(filter) 메소드
   - 걸러내는 기준이 되는 조건은 함수 형태로 filter 메소드의 인자로 전달되어야 함
   ```javascript
   // 고차함수(filter)를 사용하지 않을 경우
   const persons = [
     { name: 'Peter', age: 16 },
     { name: 'Mark', age: 18 },
     { name: 'John', age: 27 },
     { name: 'Jane', age: 14 },
     { name: 'Tony', age: 24},
   ];
   const fullAge = [];
   for(let i = 0; i < persons.length; i++) {
     if(persons[i].age >= 18) {
       fullAge.push(persons[i]);
     }
   }
   console.log(fullAge);

   ```
   ```javascript
   // 고차함수(filter) + 화살표 함수를 사용했을 경우
   const persons = [
     { name: 'Peter', age: 16 },
     { name: 'Mark', age: 18 },
     { name: 'John', age: 27 },
     { name: 'Jane', age: 14 },
     { name: 'Tony', age: 24},
   ];
   const fullAge = persons.filter(person => person.age >= 18);
   console.log(fullAge);
   ```
   
- Array.prototype.reduce
   - 배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환
   - 기본 사용법
   ```javascript
   arr.reduce(callback[, initialValue])
   ```
   - callback: 배열의 각 요소에 대해 실행할 함수. accumulator, currentValue, currentIndex, array 4가지의 매개변수를 가질 수 있음
      - accumulator: 누산기. 콜백의 반환값을 누적. 콜백의 이전 반환값 또는, 콜백의 첫 번째 호출이면서 initialValue를 제공한 경우에는 initialValue의 값임
      - currentValue: 처리할 현재 요소
      - currentIndex (Optional): 처리할 현재 요소의 인덱스. initialValue를 제공한 경우 0, 아니면 1부터 시작
      - array (Optional): reduce()를 호출한 배열
   - initialValue (Optional): callback의 최초 호출에서 첫 번째 인수에 제공하는 값. 초기값을 제공하지 않으면 배열의 첫 번째 요소를 사용. 빈 배열에서 초기값 없이 reduce()를 호출하면 오류 발생

   ```javascript
   // 고차함수(reduce)를 사용하지 않을 경우
   const arr = [5, 7, 1, 8, 4];

   let sum = 0;

   for (let i=0; i<arr.length; i++) {
     sum = sum + arr[i];
   }

   // prints 25
   console.log(sum);
   ```
   ```javascript
   // 고차함수(reduce)를 사용했을 경우
   const arr = [5, 7, 1, 8, 4];

   const sum = arr.reduce(function(accumulator, currentValue) {
     return accumulator + currentValue;
   });

   // prints 25
   console.log(sum);
   ```
   ```javascript
   // 대표적인 reduce 예시
   const arr = [1, 2, 3, 4, 5];
   const result = arr.reduce((acc, cur, idx) => { return acc += cur; }, 0);
   console.log(result);  // 15

   const arr2 = [1, 2, 3, 4, 5];
   const result2 = arr2.reduce((acc, cur, idx) => { return acc += cur; }, 10);
   console.log(result2);  // 25
   ```

## 콜백함수
- 파라미터로 함수를 전달하는 함수
- 매개변수로 넘겨받은 함수는 일단 넘겨받고, 때가 되면 나중에 호출(called back)한다는 것이 콜백함수의 개념
- 주로 비동기 처리시에 사용
- 코드의 가독성을 위해 사용하는 경우도 있음
- 콜백함수 하나만 바꿔서 하나의 함수를 여러개로 이용할 수 있어 유용함
```javascript
function introduce (lastName, firstName, callback) { 
    var fullName = lastName + firstName; 
    callback(fullName); 
} 

introduce("홍", "길동", function(name) { console.log(name); });
```

## 재귀함수
- 함수가 자기 자신을 호출하는 함수
- 예제
```javascript
// 팩토리얼을 구하는 함수
// 팩토리얼: n이 하나의 자연수일 때, 1에서 n까지의 모든 자연수의 곱
function factorial(x) {
  if (x<0) return;
  if (x===0) return 1;
  return x * factorial(x-1);
}

factorial(3);
```
- 재귀의 구성
   - 종료 조건
      - 옳지 않은 값이 들어왔을 때 재귀를 멈추는 조건
      - 재귀가 계속하여 동작하는 것을 방지
      - 위 예제에서는, if (x < 0) return; 
         - 음수의 팩토리얼을 구할 수 없기 때문

   - 기반 조건(Base case, 기저 상태)
      - 재귀함수의 모든 조건을 만족했을 때 재귀를 멈추는 조건
      - 기반 조건은 재귀 함수의 목적 
      - 위 예제에서는, if (x === 0) return 1;
         - x가 0까지 진행된다면, 재귀함수를 모두 구한것이기 때문
   
   - 재귀
      - 자기 자신을 호출하는 것
      - 위 예제에서는, return x * factorial(x - 1);
