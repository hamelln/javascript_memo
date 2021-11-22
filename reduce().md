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

```txt
1. 맨 끝에 적힌 0은 acc에 담길 초기값이다. 즉, acc = 0으로 초기화된 상태.
2. curVal는 arr에 있는 최근값이다. 즉, curVal = 1 -> 1 -> 2 -> 3으로 차례대로 변한다.
3. 함수가 acc + curVal이므로 아래 순서대로 처리된다.

      acc = 0 + 1
      acc = 1 + 1
      acc = 2 + 2
      acc = 4 + 3

(acc는 이름대로 누산이다. 계산이 계속 누적되는 변수이다. 
화살표 함수라 return을 생략했지만 return acc + curVal이라 하면 acc에 acc + curVal이 return되는 것.)
```

### 예제 2

```javascript
let arr2 = [{x: 1}, {x:2}, {x:3}];
let sum2 = arr2.reduce((acc, curVal) => acc + curVal.x), 0);
```

### 해설

```txt
reduce는 객체 배열도 처리할 수 있다.
acc = 0이고,
curVal은 arr2의 원소 {x:1}, {x:2}, {x:3}이다.
curVal의 key가 x이므로 curVal.x = 1 -> 2 -> 3이다.
따라서 acc + curVal.x를 하면 0+1+2+3 = 6이 return된다.
```

### Q) key값이 다르면 어떻게 할까?

```javascript
let arr2 = [{x: 1}, {x:2}, {x:3}, {y:4}];
let sum2 = arr2.reduce((acc, curVal) => acc + curVal.x), 0);
```

### 해설

```txt
객체의 key값이 x,y로 나뉘어져 있다. 
curVal.x는 {y:4} 객체 원소에서 key값 x를 못 찾고 undefined를 return
위의 코드는 최종적으로는 6 + undefined로 계산한 뒤 return하므로 NaN이 출력된다.
이를 해결하려면 다음과 같이 처리한다.
```

```javascript
let arr2 = [{x: 1}, {x:2}, {x:3}, {y:4}];
let sum2 = arr2.reduce((acc, curVal) => acc + Number(Object.values(curVal)), 0);
```

### 추가 설명 Object

```txt
Object.values()를 이용하면 객체 내에 있는 '모든' value를 추출한다.
그러나 이 때는 curVal.x와 달리 정수 1이 추출되지 않는다. '1'도 아니다. object [ 1 ] 이 추출된다.
Number로 형변환을 처리하자.
```

### Q) 아래와 같은 코드는 어떻게 할까?

      이름 없는 파티원 4명이 있습니다. 파티원 모두 힘 str이 각각 입력되어 있어야 합니다. 
      1. 입력이 없는 사람은 str = 1로 처리합니다. 
      2. str이 입력된 사람들은 힘을 모두 합친 값을 return합니다.

```javascript
let arr2 = [{str: 1}, {str:2}, {str:3}, {int:4, dex:1, job:'wizard'}];
```

### 해설

```txt
key값이 존재하는지 검사하고, 없는 사람은 curVal.str = 1로 지정한다. 즉, 해당 객체에 {str : 1}이라는 key, value값을 추가하겠단 뜻.
그리고 acc + curVal.str을 처리해서 파티원들의 str을 총합한다.
```

```javascript
let arr2 = [{str: 1}, {str:2}, {str:3}, {int:4, dex:1, job:'wizard'}];
let sum2 = arr2.reduce((acc, curVal) => {
  if(curVal.str === undefined) curVal.str = 1;
  return acc + curVal.str}, 0);
```

### 예제 3

```javascript
let arr3 = [[0, 1], [2, 3], [4, 5]];
let sum3 = arr3.reduce((acc, curVal) => acc = [...acc, ...curVal], []);

let arr4 = [[0, 1], [2, 3], [4, 5]];
let sum4 = arr3.reduce((acc, curVal) => acc.concat(curVal), []);
```

### 해설

```txt
reduce는 이중 배열을 풀어서 처리할 수도 있다. 둘의 결과는 모두 [0,1,2,3,4,5]가 출력된다. 입맛에 맞는 방법을 쓰자.
```

### 참고 링크

[MDN reduce()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
