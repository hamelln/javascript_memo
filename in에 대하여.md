## in은 언제 쓸까?

### '객체' 안의 'key'값을 찾을 때 쓴다.

### "문자열"(key) in Object

```javascript
let array = [10,20,30,40,50];
let obj = {js : "weird", html : "hard", css : "ha~~rd"};
let objArr = [
    {js : "weird", html : "hard", css : "ha~~rd"},
    {ts : "hare", algorithm : "hard", reacr : "what..."},
]

console.log(`10 in array: ${10 in array}`);
console.log(`'10' in array ${'10' in array}`);
console.log(`0 in array: ${0 in array}`);
console.log(`6 in array: ${6 in array}`);

console.log(`'js' in obj: ${'js' in obj}`);
console.log(`'js' in objArr: ${'js' in objArr}`);

console.log(`"length" in Object: ${"length" in Object}`);
console.log(`"floor" in Math: ${"floor" in Math}`);
console.log(`"fromCharCode" in String: ${"fromCharCode" in String}`); 

```

![image](https://user-images.githubusercontent.com/39308313/143670246-8a115ff7-ac60-4a99-a14c-f7bd1efca220.png)

```
array는 배열이지만 타입은 객체로 분류된다. 하지만 key값이랄 게 없는 상태이므로 in으로 찾을 수 있는 건 인덱스, 내장 메소드 뿐이다.

obj는 key, value가 있는 객체다. 따라서 "key" in obj로 찾을 수 있다.

objArr는 객체 배열이다. 객체마다의 key은 없는 상태라서 'js'로 검색하면 찾을 수 없다.

Math, Object, String 등은 객체이므로 내장된 메소드를 찾을 수 있다.
```
