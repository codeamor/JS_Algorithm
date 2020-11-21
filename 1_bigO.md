# 1. 빅오 표기법

## 1.1. 일반적인 예

- O(1)은 입력 공간에 대해 변하지 않는다. <br>
  따라서 O(1)을 상수 시간이라 부른다.

  - 배열에 있는 항목을 인덱스를 이용해 접근하는 경우가 O(1) 알고리즘의 예다.

- O(n)은 선형 시간이고 최악의 경우엔 n번의 연산을 수행해야 하는 알고리즘에 적용된다.

```javascript
function exampleLinear(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

- O(n^2)

```javascript
function exampleOeuadratic(n) {
  for (let i = 0; i < n>, i++) {
    console.log(i);
    for (let j = i; j < n; j++) {
      console.log(j);
    }
  }
}
```

- O(n^3)

```javascript
function exampleCubic(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
    for (let j = i; j < n; j++) {
      console.log(j);
      for (let k = j; k < n; k++) {
        console.log(k);
      }
    }
  }
}
```

- 로그 시간 복잡도를 지닌 알고리즘 (2^2 ~ 2^n)

  - 로그 시간 복잡도의 효율은 백만 개의 항목과 같이 큰 입력이 있는 경우에 효과적이다.

```javascript
function exampleLogarithmic(n) {
  for (let i = 2; i <= n; i = i * 2) {
    console.log(i);
  }
}
```

<br>

## 1.2. 빅오 표기법 규칙

> 계수 법칙

: 상수 k가 0보다 크다고 할 때(상수 k > 0), f(n)이 O(g(n))이면 kf(n)은 O(g(n))이다.

- 입력 크기 n과 관련되지 않는 계수를 제거한다.<br>
  n이 무한에 가까워지는 경우 다른 계수는 무시해도 되기 때문이다.

> 합의 법칙

: f(n)이 O(h(n))이고 g(n)이 O(p(n))이면 f(n)+g(n)은 O(h(n)+p(n))이다.

- 합의 법칙은 결과값인 시간 복잡도가 두 개의 다른 시간 복잡도의 합이라면 결과값인 빅오 표기법 역시 두 개의 다른 빅오 표기법의 합이라는 것을 의미한다.

> 전이 법칙

: f(n)이 O(g(n))이고 g(n)이 O(h(n))이면 f(n)은 O(h(n))이다.

- 교환 법칙은 동일한 시간 복잡도는 동일한 빅오 표기법을 지님을 나타내기 위한 간단한 방법이다.

> 다항 법칙

: f(n)이 k차 다항식이면 f(n)은 O(n^k)이다.

- 직관적으로 다항 법칙은 다항 시간 복잡도가 동일한 다항 차수의 빅오 표기법을 지님을 나타낸다.
  <br>

---

<br>

## | 계수 법칙: "상수를 제거하라"

> 시간 복잡도 O(n) 을 가진 코드

> f(n) = n

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < n; i++) {
    count += 1;
  }
  return count;
}
```

> f(n) = 5n

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < 5 * n; i++) {
    count += 1;
  }
  return count;
}
```

> f(n) = n+1

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < n; i++) {
    count += 1;
  }
  count += 3;
  return count;
}
```

- count += 3 으로 인해 n에 +1 이 추가되었다.
- 추가된 연산이 입력 n에 영향을 받지 않기 때문에 여전히 O(n)의 빅오 표기법이다.

<br>

## | 합의 법칙: "빅오를 더하라"

- 상위 알고리즘의 빅오 표기법은 단순히 그에 포함되는 두 개의 알고리즘의 합이다.
- 합의 법칙을 적용한 다음 계수 법칙을 적용해야 한다.

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < n; i++) {
    count += 1;
  }
  for (let i = 0; i < 5 * n; i++) {
    count += 1;
  }
  return count;
}
```

- f(n) = n과 f(n) = 5n의 합은 6n이지만 계수 법칙을 적용시켜 최종 결과는 O(n)=n이 된다.

## | 곱의 법칙: "빅오를 곱하라"

- 곱의 법칙은 빅오가 어떤 식으로 곱해지는지에 관한 것이다.

> 다음 코드는 두 개의 중첩 for 루프를 포함하며 해당 중첩 for 루프에 곱의 법칙이 적용된다.

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < n; i++) {
    count += 1;
    for (let i = 0; i < 5 * n; i++) {
      count += 1;
    }
  }
  return count;
}
```

- f(n) = 5n\*n 이다. <br>
  계수 법칙을 적용하여 결과는 O(n) = n^2 이 된다.

## | 다항 법칙: "빅오의 k승"

- 다항 법칙은 다항 시간 복잡도가 동일한 다항 차수를 지닌 빅오 표기법을 지님을 나타낸다.
  > f(n) = n^2

```javascript
function a(n) {
  let count = 0;
  for (let i = 0; i < n * n; i++) {
    count += 1;
  }
  return count;
}
```
