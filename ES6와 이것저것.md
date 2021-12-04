# 1. Hoisting에 관해

```txt
흔히들 ES6 이후로 var를 내치고 let, const를 씀으로 인해 'hoisting이 일어나지 않는다'고 알고 있다.
하지만 MDN 문서에서는 이렇게 말하고 있다.
```

    In ECMAScript 2015, 'let and const are hoisted' but not initialized
    
```txt
호이스팅은 일어난다. 하지만 초기화가 안 될 뿐이다.
var는 undefined로 초기화가 일어나는 것이고, let, const는 uninitialized가 될 뿐이다.
```

## 함수는 Hoisting이 일어난다.

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
let, const는 호이스팅이 되더라도 uninitialized다.
baz는 결국 let, const다. 
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
주소지 자체만 통째로 못 바꿀 뿐이다.
```

## js에는 primitive 타입이 7개 있다.

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
```
