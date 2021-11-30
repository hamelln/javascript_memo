### Execution context

javaScript Engine은 js코드를 실행하기 전에, 먼저 코드의 맥락을 짚는다.  
그 코드가 말이 되는 코드인지, 실행할 만한 코드인지 살펴본다는 얘기다.  

그러한 맥락을 Execution Context (EC)라 한다.  

### EC에는 세 가지 종류가 있다.  

1. Global Execution Context (GEC)
2. Functional execution context (FEC)
3. Eval

3번은 잘 모르겠고, 주로 1,2번을 다루는 듯하니 1,2번만 살펴보자.  


    GEC는 js를 실행할 때 만들어진다.

GEC는 Global Object를 만들고, 'this'를 제공한다.  
브라우저에 살펴보면 이 this는 window와 같다.
html에 빈 js파일을 연결시킨 다음 실행한 뒤 this를 입력하면 아래와 같이 뜬다.  

![image](https://user-images.githubusercontent.com/39308313/144028698-b18ba814-01b7-41db-a56a-328ecc7e1f9f.png)

    코드가 없다고 일을 안 하는 게 아니다.

EC는 두 가지의 단계(phase)를 거친다.

1. 생성 단계(Creation phase)
2. 실행 단계(Execution phase)

        생성 단계는 변수의 '선언'을 읽고, 실행 단계는 변수의 '값'을 읽는다.

```javascript
let ten = 10;
```

1. 위와 같은 코드가 있으면 GEC는 생성 단계에서 ten이라는 변수를 인식한다.  
2. 생성 단계가 끝나면 실행 단계에서 GEC는 ten이라는 변수에 10이라는 값을 할당한다.   

        FEC는 함수를 '실행'할 때 만들어진다.('선언'할 때가 아니다.)

function 내에서 this는 '자신이 속한 객체'를 가리킨다.  

```javascript
const mainObj = {
    obj:{
        name: 'Da',
        method: function(){
            return console.log(this);
        }
        },
    b:3,
    method: function(){console.log(this)},
};

mainObj.method();
mainObj.obj.method();
```

![image](https://user-images.githubusercontent.com/39308313/144036400-1c4b51e0-3edf-469f-a75e-c2a4e6462278.png)

(단, 화살표 함수의 this는 function으로 선언할 때와 달리 global의 this를 가리킨다.)  

```javascript
const mainObj = {
    obj:{
        name: 'Da',
        method: function(){
            return console.log(this);
        }
        },
    b:3,
    method: () => console.log(this),
};

mainObj.method();
mainObj.obj.method();
```

![image](https://user-images.githubusercontent.com/39308313/144039664-cee3e2c0-d8e4-4ca9-91a9-ea5ace5bf313.png)


```javascript
let first = 1;
function firstMethod(){
    let second = 2;
    function secondMethod(num){
        console.log(num);
    }
    function thirdMethod(){
        let third = 3;
        secondMethod(first * second * third)
    }
    thirdMethod();
}
firstMethod();
```

위와 같은 코드를 짰을 때 Execution Context 스택은   
[[first, firstMethod()], [second, secondMethod(), thirdMethod()], [third], [num]] 식으로 쌓인다.

```javascript
this.x = 9;

const set = {
    x: 81,
    getX: function() { return this.x; },
  };

let func = set.getX;
let funcResult = func();
let result = set.getX();

console.log(`funcResult is ${funcResult}`);
console.log(`result is ${result}`);
```

다음과 같이 했을 때 결과는 아래와 같다.  

![image](https://user-images.githubusercontent.com/39308313/144044165-9af92130-ef88-45d8-8040-793b2be5a080.png)

func는 set의 getX라는 함수만 가져왔을 뿐이고, getX를 실행한 건 아니다.  
함수는 실행할 때 Execution Context를 만든다.  
즉, func()를 실행할 때에 func EC가 만들어지고, 이 때의 this는 global object이다.  

화살표 함수의 this는 호출된 함수를 둘러싼, 선언될 때의 EC를 가리킨다.  

화살표 함수의 this는 한 번 정해지면 못 바꾸고, function의 this는 bind 등으로 바꿀 수 있다.  

```javascript
'use strict'

const set = {
  innerFunc() {
    let f1 = function(){
      return this;
    }

    let f2 = () => {
      return this; 
    }
    
    return [f1(),f2()];
  }
}
let a = set.innerFunc()[0];
let b = set.innerFunc()[1];
console.log(a);
console.log(b);
```

![image](https://user-images.githubusercontent.com/39308313/144050747-8c6e01c2-0340-40ad-a65b-e0a6f8ec0c5e.png)

언뜻 보면 f1을 둘러싼 객체가 set인 것처럼 보이지만 innerFunc()에 감싸져있기 때문에 f1은 this랄 게 없는 상황이다.  
f2는 innerFunc()가 실행될 때 선언된다.  
따라서 f2의 this는 innerFunc라는 set의 메소드 자체를 가리킨다.  
