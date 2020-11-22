# 자바스크립트 숫자

# 1. 정수 반올림

- 자바스크립트가 모든 숫자를 나타낼 때 부동소수점을 사용하기 때문에 정수 나눗셈은 소용이 없다.

```javascript
Math.floor; // 가장 가까운 정수로 내림
Math.round; // 반올림
Math.ceil; // 올림
```

# 2. 숫자 알고리즘

## 2.1. 소수 테스트

숫자가 소수인지 알아보는 방법은 숫자 n을 2부터 n-1까지의 수로 나눠 나머지가 0인지 확인해보면 된다.

```javascript
function isPrime(n) {
  if (n <= 1) {
    return false;
  }

  // 2부터 n-1까지의 수로 나눈다.
  for (let i = 2; i < n; i++) {
    if (n % i === 0) {
      return false;
    }
  }
  return true;
}
```

**시간 복잡도 O(n)**

- 0부터 n까지의 모든 수를 확인하기 때문에 O(n)이다.

> 알고리즘 개선

- 소수를 나열해본다.<br>

`2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, ...`
<br>
2와 3을 제외하고는 모든 소수는 6k+-1의 형태를 지닌다. (k는 정수)

`5 = (6-1), 7 = ((1*6) + 1), 13 = ((2*6) + 1)`

- n이 소수인지 알아보기 위해 반복문을 n의 제곱근까지만 확인해본다.
  <br> n의 제곱근이 소수가 아니면 n은 소수가 아니기 때문이다.

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  if (n <= 3) return true;

  // 입력된 수가 2 or 3인 경우 아래 반복문에서
  // 다섯 개의 숫자를 건너뛸 수 있다.
  if (n % 2 === 0 || n % 3 === 0) return false;

  for (let i = 5; i * i <= n; i = i + 6) {
    if (n % i === 0 || n % (i + 2) === 0) return false;
  }

  return true;
}
```

**시간 복잡도: O(sqrt(n))**

- 시간 복잡도를 줄이게 되었다.

<br>

# 2.2. 소인수분해

```javascript
function primeFactors(n) {
  // n이 2로 나눠진다면 나눠질 수 있는 수만큼 2가 출력된다.
  while (n % 2 === 0) {
    console.log(2);
    n = n / 2;
  }

  // 이 지점에서 n은 반드시 홀수이다. 따라서 수를 두 개씩 증가시킨다.
  for (let i = 3; i*i <= n; i i+2) {
    // i가 n을 나눌 수 있는 한 계속해서 i가 출력되고 n을 i로 나눈다.
    while (n % i === 0) {
      console.log(i);
      n = n / i;
    }
  }

  // 다음 조건문은 n이 2보다 큰 소수인 경우를 처리하기 위함
  if (n > 2) {
    console.log(n);
  }
}
primeFactors(10); // '5' 와 '2' 출력
```

**시간 복잡도: O(sqrt(n))**

위의 알고리즘은 i로 나머지가 없이 나눌 수 있는 모든 수를 출력한다.<br>소수가 함수의 입력 값으로 전달된 경우 아무 수도 출력되지 않다가 마지막 조건문에서 n이 2보다 큰지 확인한 다음 n이 2보다 클 경우 n이 출력된다.

# 2.3. 무작위 수 생성기

- Math.random()은 0과 1 사이의 부동소수점을 반환한다.

```javascript
Math.random * 100; // 0부터 100까지의 부동소수점
Math.random() * 25 + 5; // 5부터 30까지의 부동소수점
Math.random() * 10 - 100; // -100부터 -90까지의 부동소수점
```

- 무작위 정수를 얻기 위해선 Math.floor(), Math.round(), Math.ceil()을 사용해 부동소수점을 정수로 만든다.

```javascript
Math.floor(Math.random() * 100); // 0부터 99까지의 정수
Math.round(Math.random() * 25) + 5; // 5부터 30까지의 정수
Math.ceil(Math.random() * 10) - 100; // -100부터 -90까지의 정수
```
