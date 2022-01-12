## About reduce method

### 개요

- 배열을 가지고 누산기 변수acc와 최근 값 currentValue를 받아서 처리하는 메소드

### 왜 이름이 reduce냐?

    이 reduce는 "감소하다"라는 의미로 쳐다보면 이해가 어렵다.

```txt
reduce에는 다음과 같은 의미들도 있다.

to cause (someone) to be in a specified state or condition
to cause (something) to be in a specified form by breaking it, burning it, etc.
to transpose from one form into another
to become concentrated or consolidated
...

'(뭔가를) 특정한 state, form, 상태 등으로 만든다.'

참고로 redux에서 쓰는 reducer도 이런 의미로 쳐다봐야 이해가 더 쉬울 것이다.
```

- 예시부터 보자.

### 1) 정수 배열의 합을 구하고 싶을 때

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

### 2) 객체 배열의 합을 구하고 싶을 때

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

### Q) 객체 배열에서 key값들이 다르면 어떻게 할까?

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

### 3) 객체 배열에서 특정 조건을 통해서만 출력하고 싶을 때

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

### 추가 예제

```txt
배열들을 가지고 객체를 만들 때에도 유용하다.
```

```javascript
let genres = ["classic", "pop", "classic", "classic", "pop"];
let plays = [500, 600, 150, 800, 2500];

let set = genres.reduce((acc,cur,i)=>acc.concat({'i': i, 'genre': cur, 'play': plays[i]}),[]);
```

### 결과

![image](https://user-images.githubusercontent.com/39308313/143067116-1299014c-f547-4b85-8e3b-35b957f8ad9a.png)

### 4) 이중 배열을 풀어내고 싶을 때

```javascript
let arr3 = [[0, 1], [2, 3], [4, 5]];
let sum3 = arr3.reduce((acc, curVal) => [...acc, ...curVal], []);

let arr4 = [[0, 1], [2, 3], [4, 5]];
let sum4 = arr3.reduce((acc, curVal) => acc.concat(curVal), []);
```

### 해설

```txt
reduce는 이중 배열을 풀어서 처리할 수도 있다. 둘의 결과는 모두 [0,1,2,3,4,5]가 출력된다. 입맛에 맞는 방법을 쓰자.
```

### 4-1) 객체 배열 안에 있는 특정 배열 값을 추출할 때

```javascript
let friends = [{
    name: 'Anna',
    books: ['Bible', 'Harry Potter'],
    age: 21
  }, {
    name: 'Bob',
    books: ['War and peace', 'Romeo and Juliet'],
    age: 26
  }, {
    name: 'Alice',
    books: ['The Lord of the Rings', 'The Shining'],
    age: 18
  }];
  
let allbooks = friends.reduce((acc, curVal) => [...acc, ...curVal.books], ['Alphabet', 'Test of math']);
```

### 해설

```txt
spread operator를 쓰면 배열은 빼고 배열 내의 원소들만 나열된다.
1. 초기값 acc = ['Alphabet', 'Test of math']
2. 현재 curVal = { name: 'Anna', books: ['Bible', 'Harry Potter'], age: 21 }
3. 현재 curVal.books = ['Bible', 'Harry Potter']

4. return [...acc, ...curVal.books]이 의미하는 바는
   acc = ['Alphabet', 'Test of math', 'Bible', 'Harry Potter']라는 뜻이다.

5. 따라서 최종적으로 모든 books의 string값만 모아 배열로 만들어서 allbooks 변수로 넘긴다.
```

### 5) 배열 원소들의 갯수를 세서 객체로 표현하고 싶을 때

```javascript
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

let countedNames = names.reduce((allNames, name) => {
    if (name in allNames) allNames[name]++;
    else allNames[name] = 1;
    return allNames;
}, {});

```

### 해설

```txt
1. allNames의 초기값은 빈 객체 {}로 지정됐다. name의 첫 값은 string타입 'Alice'이다.

2. allNames 안에 name 'Alice'가 있는지 검사하고, 있으면 allNames['Alice'] += 1로 처리한다. 
처리된다면 {'Alice' : 1} => {'Alice' : 2}로 될 것

3. 만약에 allNames 안에 name 'Alice'가 없다면 allNames['Alice'] = 1이라고 처리한다. 
처리된다면 {} => {'Alice' : 1}로 될 것.

4. allNames를 return한다. 따라서 첫 과정이 끝나면 allNames는 {} => {'Alice' : 1}로 바뀐다.

5. 두 번 돌고나면 allNames는 {'Alice' : 1} => {'Alice' : 1, 'Bob': 1}로 바뀐다.

6. 최종적으로 allNames는 객체 { Alice: 2, Bob: 1, Tiff: 1, Bruce: 1 }가 된다. 

7. 이 결과는 변수 countedNames에 들어간다.
```

### 6) 특정 key값을 기준으로 객체들을 재정리하고 싶을 때

```javascript
let people = [
    { name: 'Alice', age: 21 },
    { name: 'Max', age: 20 },
    { name: 'Jane', age: 20 }
  ];
  
  function groupBy(objectArray, property) {
    return objectArray.reduce((acc, obj) => {
      let key = obj[property];
      if (!acc[key]) acc[key] = [];
      acc[key].push(obj);
      return acc;
    }, {});
  }
```

### 해설

```txt
1. people이라는 객체 배열이 있다. 특정 조건이 같은 사람끼리만 따로 묶어서 정리하고 싶다.

2. people에 있는 객체들을 'age' 기준으로 정리하게 groupBy(people, 'age')라는 함수를 만든다.

3. groupedPeople은 groupBy()함수가 이뤄진 people들을 담을 변수다.

4. 누산기 acc는 초기값 {}인 빈 객체, 매개 변수 objectArray는 객체 배열 people이다.

5. 현재 obj는 { name: 'Alice', age: 21 }, property는 'age'이다.

6. 따라서 key = obj['age']를 하면 key = 21이다.

7. 현재 acc가 빈 객체 {}이므로 acc[21]이란 건 없다. 따라서 acc[21] = [];로 만든다.
acc의 상태는 { '21': [] }가 된다.

8. 그리고 acc[21].push({ name: 'Alice', age: 21 })를 실행한뒤 acc를 return.
acc의 상태는 { '21': [ { name: 'Alice', age: 21 } ] }가 된다.
※acc가 누산기이므로 이런 작업을 할 땐 항상 return acc를 해줘야 결과값이 쌓인다.

9. 그 다음엔 acc[20] = []로 선언하고, acc[20].push({ name: 'Max', age: 20 });

10. 그 다음엔 acc[20]이 있으므로 acc[20]에 바로 { name: 'Jane', age: 20 }를 push

11. 결과는 아래와 같은 object로 return되어 groupedPeople에 저장된다.

{
  '20': [ { name: 'Max', age: 20 }, { name: 'Jane', age: 20 } ],
  '21': [ { name: 'Alice', age: 21 } ]
}
```

### 7) 파이프 함수를 쓸 때

```javascript
const double = x => x + x;
const makeString = (x,y) => `입력된 값은 ${y}이고 2배는 ${x}입니다.`;
const pipe = (...functions) => (input1, input2) => functions.reduce((acc, fn) => fn(acc, input2), input1);
const myfunc = pipe(double, makeString);

const result = myfunc(2,2);
```

### 해설

```txt
참고 : double, makeString, pipe, myfunc는 전부 함수다. 값을 저장하는 변수는 result 뿐이다.

1. double은 정수 인자 x를 2배로 만들어 return

2. makeString은 정수 인자 x, y를 받아 "입력된 값은 2이고 2배는 4입니다."라는 string을 받고 싶다.

3. myfunc는 double, makeString 함수를 인자로 전달 받는다.

4. pipe는 인자로 전달된 함수 double, makeString을 처리한다.

4-1. myfunc의 인자로 2가 전달됐고, 이 2는 double에 input1이란 매개변수로 전달됐다. 

4-2. acc의 초기값을 input1로 지정한다. 즉, acc = 2인 상태다.

4-3. 현재 fn은 double이다. fn(acc, input2)는 double(2, 2)다.

4-4. double(2, 2)의 결과를 acc에 return한다.
※ double은 원래 인자를 하나만 받는 함수다. js가 아니라 다른 곳에서 이런 짓을 하면 error가 날 것.

4-5. 다음 fn은 makeString이다. fn(acc, input2)는 makeString(4, 2) = `입력된 값은 2이고 2배는 4입니다.`를 return

5. 모든 과정이 끝났으므로 result에 `입력된 값은 2이고 2배는 4입니다.`이 저장된다.
```

### 8) 배열의 중복값을 제거할 때

```javascript
let arr = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4];
let result = arr.sort().reduce((acc, curVal) => {
    const length = acc.length;
    if (length === 0 || acc[length - 1] !== curVal) acc.push(curVal);
    return acc;
}, []);
```

### 해설

```txt
1. arr.sort()로 정렬한다.

2. 정렬된 arr에 reduce를 실행한다.

3. acc 초기값은 빈 배열 [], current는 1

4. 반복할 때마다 acc의 length를 구한다.

5. 만약 acc가 비어있으면 curVal을 넣는다.

5-1. acc가 비어있지 않으면, acc의 마지막 값이 curVal과 다를 때에만 acc.push(curVal)을 한다.
(이유 : sort를 했기 때문에 acc 마지막 값만 검사해도 된다.)

6. return acc를 하고 계속 반복한다. 

7. arr를 오름차순으로 정렬하고, 중복값을 제거한 배열이 result에 저장된다.

결과 : [1,2,3,4,5]
```

### 8-1) reduce 말고 중복 제거하는 법

```javascript
let myArray = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4];
let orderedArray = Array.from(new Set(myArray));
```

```txt
MDN 문서에서는 set과 Array.from을 활용하는 것도 권장한다.
이 경우에는 sort()처리 없이 중복값만 제거한다.

결과 : [1,2,3,5,4]
```


### 참고 링크

[MDN reduce()문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
