## 클로저의 정의
클로저란 함수가 속한 렉시컬 스코프를 기억하여 렉시컬 스코프 밖에서 실행할 때도 그 스코프에 접근할 수 있게 하는 기능입니다. <br/>
다시 말해, 외부 함수 호출이 종료되더라도 외부 함수의 지역 변수 및 변수 스코프 객체의 체인 관계를 유지할 수 있는 구조를 클로저라고 한다.

## 클로저를 통해 얻을 수 있는 장점
- 함수가 리턴되어도 특정값을 보호하면서, 그 값을 계속 사용할 수 있다.
- 클로저는 특정값을 완벽하게 보호할 수 있는 공간이다. (클로저를 만든 코드를 통해서만 접근이 가능하다.)

## 클로저가 생성되는 조건
1. 내부 함수가 익명 함수로 되어 외부 함수의 반환값으로 사용된다.
2. 내부 함수는 외부 함수의 실행 환경에서 실행된다. (외부함수를 호출해야 한다.)
3. 내부 함수에서 사용되는 변수는 외부 함수의 변수 스코프에 있다.

## 예시 코드 
```js
function increment() {
  let saveNumber = 1;

  return function () {
    return saveNumber++;
  }
}

const inc = increment();

console.log(inc()); // 1
console.log(inc()); // 2
console.log(inc()); // 3
```

```javascript
function outer() {
  var a = 2;
  function inner() {
    console.log(a);
  }
  return inner;
}
var func = outer();
func(); // 2
```
