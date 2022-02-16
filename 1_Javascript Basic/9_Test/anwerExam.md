## 1. 계산기
```javascript
const plus = (n1, n2) => {
    return Number(n1) + Number(n2)
}

const minus = (n1, n2) => {
    return n1 - n2
}

const multiply = (n1, n2) => {
    return n1 * n2
}

const divide = (n1, n2) => {
    return n1 / n2
}

let n1 = prompt("첫번째 숫자를 입력하세요");
let n2 = prompt("두번째 숫자를 입력하세요");
let operator = prompt("연산자를 입력하세요", "+ - * / 만 입력할 수 있습니다.");

switch(operator) {
    case "+": 
    alert(plus(n1, n2));
    break;

    case "-": 
    alert(minus(n1, n2));
    break;
    
    case "*": 
    alert(multiply(n1, n2));
    break;
    
    case "/": 
    alert(divide(n1, n2));
    break;
}
```