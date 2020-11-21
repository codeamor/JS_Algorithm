# 자바스크립트의 독특한 특징

# 1. 자바스크립트의 범위

## 1.1. 전역 선언: 전역 범위

- 자바스크립트에서는 연산자 없이 변수를 선언할 수 있다.

```javascript
test = "aaa";
```

- 가장 안좋은 변수 선언 방식이므로 되도록 사용을 피한다.

## 1.2. var: 함수 범위

- 변수를 어디에서 선언하든 변수 선언이 함수의 맨 앞으로 이동한다.<br>이를 **변수 호이스팅(variable hoisting)** 이라고도 한다.

- 스크립트 실행 시 변수가 스크립트의 가장 마지막에 선언됐다고 하더라도 해당 선언 코드가 가장 마지막에 실행되는 것이 아니다.

```javascript
function scope1() {
  var top = "top";
  bottom = "bottom";
  console.log(bottom);

  var bottom;
}
scope1(); // "bottom"을 출력하며 오류가 발생하지 않는다.
```

위의 코드는 아래와 동일하다.

```javascript
function scope1() {
  var top = "top";
  var bottom;
  bottom = "bottom";
  console.log(bottom);
}
```

- var 키워드의 핵심적인 사항은 해당 변수의 범위가 가장 가까운 함수 범위라는 것이다.

```javascript
function scope2(print) {
  if (print) {
    var insideIf = "12";
  }
  console.log(insideIf);
}
scope2(true); // 12 출력
```

아래와 동일하다.

```javascript
function scope2(print) {
  var insideIf;

  if (print) {
    insideIf = "12";
  }
  console.log(insideIf);
}
scope2(true); // 12 출력
```

- Java에서 위 구문은 오류를 일으킨다. insideIf 변수가 if문 블록 외부에서는 사용할 수 없기 때문이다.

```javascript
var a = 1;
function four() {
  if (true) {
    var a = 4;
  }

  console.log(a); // '4' 출력
}
```

## 1.3. let: 블록 범위

- let을 사용해 선언된 변수는 가장 가까운 블록 범위를 갖는다. <br>
  즉, 변수가 선언된 {} 내에서 유효하다.

```javascript
function scope3(print) {
  if (print) {
    let insideIf = "12";
  }
  console.log(insideIf);
}
scope3(true); // 에러
```

- insideIf 변수는 if문 블록 내에서만 사용 가능하다.

<br>

# 2. 등가와 형

## 2.1. 참/거짓 확인

> fasle

- false
- 0
- 빈 문자열
- NaN
- undefined
- null

> true

- true
- 0이 아닌 다른 숫자
- 비어 있지 않은 문자열
- 비어 있지 않는 객체

## 2.2. 객체

```javascript
let o1 = {};
let o2 = {};

o1 == o2; // false
o1 === o2; // false
```

- 두 변수의 메모리상 주소는 다르기에 false 를 반환한다.

- 이것이 대부분의 자바스크립트 애플리케이션이 lodash나 underscore와 같은 유틸리티 라이브러리를 사용하는 이유다.<br>
  이 두 라이브러리에는 두 객체 혹은 두 값을 정확하게 확인할 수 있는 isEqual 함수가 있다.<br>
  이것이 가능한 이유는 isEqual 함수가 속성 기반 등가 비교 방식으로 구현됐기 때문이다.

```javascript
function isEquivalent(a, b) {
  // 속성 이름 배열
  let aProps = Object.getOwnPropertyNames(a);
  let bProps = Object.getOwnPropertyNames(b);

  // 속성 길이가 다른 경우 두 객체는 다른 객체다.
  if (aProps.length !== bProps.length) {
    return false;
  }

  for (let i = 0; i < aProps.length; i++) {
    let propName = aProp[i];

    // 속성 값이 다른 경우 두 객체는 같지 않다.
    if (a[propName] !== b[propName]) {
      return false;
    }
  }

  // 모든 것이 일치하면 두 객체는 일치한다.
  return true;
}
isEquivalent({ hi: 12 }, { hi: 12 }); // true
```
