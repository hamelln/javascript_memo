## reduce()

### 개요

- 누산기 변수acc와 최근 값 currentValue를 받아서 처리하는 함수.

### 뭔 말이냐?

- 예시부터 보자.

### 예제 1

```javascript
let arr = [1,1,2,3];
let sum = arr.reduce((acc, curVal) => acc + curVal, 0);
```
### 해설
1. 맨 끝에 적힌 0은 acc에 담길 초기값이다. 즉, acc = 0으로 초기화된 상태.
2. curVal는 arr에 있는 최근값이다. 즉, curVal = 1 -> 1 -> 2 -> 3으로 차례대로 변한다.

3. 함수가 acc + curVal이므로 아래 순서대로 처리된다.

      acc = 0 + 1
      acc = 1 + 1
      acc = 2 + 2
      acc = 4 + 3

(acc는 이름대로 누산이다. 계산이 계속 누적되는 변수이다. 화살표 함수라 return을 생략했지만 return acc + curVal이라 하면 acc에 acc + curVal이 return되는 것.)

### 예제 2

```javascript
let arr = [1,1,2,3];
let sum = arr.reduce((acc, curVal) => acc + curVal, 0);
```




### 참고 링크

[MDN reduce()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
