## js에서 최댓값을 어떻게 구하는가?

### 개요

- 어떤 함수를 사용하면 최댓값을 적절히 구할 수 있을까?

### 용례(code)

```javascript
// 4가 나오는 코드
Math.max(1,2,3,4);

// NaN이 나오는 코드. Math.max의 인자는 배열 자체를 넣으면 안 된다.
let arr = [1,2,3,4];
Math.max(arr);

// 배열인 변수의 최댓값을 원할 땐 spread operator를 사용한다.
Math.max(...arr);

//Math.max()와 spread operator는 길이가 짧은 배열일 때에만 사용할 수 있다. 큰 범위(1만, 10만 이상 단위)는 reduce를 이용해야 한다.
let arr = Array.from({length: 1000000}, (v, i) => i);
let max = arr.reduce((a,b) => Math.max(a,b));
```

### 참고 링크
[Math.max()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/max)  
[spread operator문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)  
[reduce()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)  
[Array.from()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
