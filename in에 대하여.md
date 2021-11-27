### in은 언제 쓸까?

## '객체' 안을 검사할 때 쓴다.

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
