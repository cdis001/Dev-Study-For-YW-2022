# 배열
- 변수들로 이루어진 집합
- 배열을 구성하는 각각의 값을 요소(element)라고 하며, 배열에서의 위치를 가리키는 숫자는 인덱스(index)라 함

- 기본식
```javascript
let arr = new Array();
let arr = [];
```
- 예시
```javascript
let numbers = [1, 2, 3, 4, 5];
```

- 배열 내 특정 요소를 얻고 싶다면 대괄호 안에 순서를 나타내는 숫자인 인덱스를 넣어주면 됨
- 인덱스는 0부터 시작함
```javascript
let numbers = [1, 2, 3, 4, 5];

alert(numbers[0]) //1
```

## 배열 요소 수정

```javascript
let numbers = [1, 2, 3, 4, 5];

numers[0] = 2; //numbers = [2, 2, 3, 4, 5];
```

## 배열 요소 추가

```javascript
let numbers = [1, 2, 3, 4, 5];

numers[5] = 6; //numbers = [2, 2, 3, 4, 5, 6];
```

## 배열 요소 갯수 확인

```javascript
let numbers = [1, 2, 3, 4, 5];

numers.length; //numbers = [2, 2, 3, 4, 5, 6];
```

