# 1. Hoisting에 관해

```txt
ES6 이후로 var를 내치고 let, const는 'hoisting이 일어나지 않는다'고 알고 있다.
하지만 MDN 문서에서는 이렇게 말하고 있다.
```

    In ECMAScript 2015, 'let and const are hoisted' but not initialized
    

## Hoisting은 일어난다. 초기화가 안 될 뿐이다.

	var는 undefined로 초기화가 일어나는 것이고 let, const는 uninitialized가 될 뿐이다.

## 함수도 Hoisting이 일어난다.

```javascript
/* Function declaration */

foo(); // "bar"

function foo() {
	console.log("bar");
}

/* Function expression */

baz(); // TypeError: baz is not a function

const baz = function () {
	console.log("bar2");
};
```

## baz()는 에러가 난다.

```txt
당연하다.
위에서 방금 말했다. 

결국 baz는 const다. 호이스팅이 되더라도 uninitialized다.

'함수 표현식'이지 '함수'가 아니다. 
```

# 2. const에 관하여.

```javascript

const num = 5;
num = 4;

// 안 되는 게 뻔하다. 하지만 아래 같은 건 된다.

const obj = { name: "hamel" };
obj.name = "ams";

const arr = [1, 2, 3];
arr.push(1);
arr.shift();
```

## Object, array는 선언하면 주소값을 받는다.

```txt
const arr = [1,2,3];
const obj = {name: 'hj'};

arr, obj는 지정해준 주소에 값을 넣었을 뿐이다.

주소에서 1,2,3을 퇴거시키고 'a','b','c'를 이사시키든 뭘 하든 그건 자유다.
'주소 자체'만 통째로 못 바꿀 뿐이다.
```

## 3. js에는 primitive 타입이 7개 있다.

1. String
2. Number
3. BigInt
4. boolean
5. undefined
6. symbol
7. null

- primitive 타입은 '불변immutable' 이다.

```txt
5는 5다. 
적어도 1 = 3 = 5 = 6이라고 주장하는 미친 과학자는 없다.
s = s다. s = d = z라고 주장하는 미친 언어학자는 없다.

let str = "abc"
str.toUpperCase();을 해도 str은 불변이다.
str = str.toUpperCase();를 해서 str 변수에 다시 값을 재지정하는 것이다.

불변은 아니지만, react에서 props, state 등을 다룰 때에도 함부로 원본을 바꾸진 않게 한다.
```

## 4. js는 이상하다.

```javascript
'37' - 7 // 30
'37' + 7 // "377"
```

## 5. parseInt는 x진법을 제공한다.

![image](https://user-images.githubusercontent.com/39308313/144715883-93ccfe5d-1417-4d00-b8e3-af1c7f5603f3.png)

```txt
String을 2진법~36진법까지 바꿔주는 친절한 기능이 있다.
아무 입력 없이 하면 10진법으로 바꿔준다.
```

## 6. toString도 x진법을 제공한다.

![image](https://user-images.githubusercontent.com/39308313/144716403-6d4954fa-d01c-417e-8283-b78c52e90390.png)

```txt
Number 타입을 2진법~36진법까지 바꿔준다.
아무 입력 없이 하면 10진법으로 바꾼다.
```

## 7. 숫자 리터럴 (Numeric literals)

```txt
난 Number => Number로 진법 바꾸고 싶은데?
숫자 리터럴로 제한적인 변환이 가능하다.
```

```javascript
// 앞에 0b를 붙이면 2진법
let binary = 0b10 // 2

// 앞에 0을 붙이면 8진법
let octar = 010 // 8

// 앞에 0x 붙이면 16진법
let hexar = 0x10 // 16

// 뒤에 n 붙이면 BigInt. 매우 큰 숫자 다룰 때 좋다. 단, 그냥 Number와 BigInt는 서로 연산 불가다.
let Big = 102n // BigInt
```

### 7-1. 매우 큰, 매우 작은 숫자

```javascript
Number.MAX_SAFE_INTEGER = 2^53 - 1 = 9007199254740991
Number.EPSILON = 2.220446049250313e-16

Math.pow(Number.EPSILON, 20) * Number.MAX_VALUE = 0.000015258789062499998
MAX_VALUE가 매우 크지만 ε^20만 곱해도 엄청 작아진다.

```

## 8. for in, for of에 대해

```javascript
const arr = [3, 5, 7];
arr.foo = 'hello';

// for in은 key값을 가져온다.
for (i in arr) {
   console.log(i); // logs "0", "1", "2", "foo"
}

// for of는 '숫자 인덱스'를 가진 value만 가져온다.
for (i of arr) {
   console.log(i); // logs 3, 5, 7
}

arr = [3,5,7, foo: 'hello']이다.

arr[4] = 5; 라고 하면?
arr = [3,5,7, foo: 'hello', 5]....
가 되어야할 거 같지만 유감스럽게도
[ 3, 5, 7, <1 empty item>, 9, foo: 'hello' ]이다.
```

## 9. Set에 대해

```txt
array에서 어떤 값을 찾을 때 includes를 쓴다.
하지만 MDN에선 이런 말을 한다.
```
### *The Set 'has method' checks if a value is in a Set object, using an approach that is, on average, quicker than testing most of the elements that have previously been added to the Set object. In particular, it is, on average, 'faster than the Array.prototype.includes' method*

```javascript
// Set은 Unique한 value만 가지기 때문에 중복값을 제거할 때에도 탁월하다.

const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]
console.log([...new Set(numbers)])

// [2, 3, 4, 5, 6, 7, 32]
```

## 10. 메소드 효율이 좋다 == 메모리 효율이 좋다?

```txt
그렇지는 않다.
'메모리 효율을 따져야 할 정도'의 프로젝트를 할 때는 주의하자.
```

## 11. 멱등성(Idempotent)에 대해 생각해보자.

```txt
멱등성이란 어떤 함수의 결과물을 그 함수에 다시 넣어도 결과가 똑같이 유지되는 성질을 말한다.
```
```js
Math.abs(Math.abs(10))
```
```txt
알아둘 이유: 
RESTful 웹 서비스를 할 때처럼, POST, DELETE 등의 똑같은 요청이 동시에 잔뜩 들어와도 똑같은 결과 하나만 반환해야 한다.
```
