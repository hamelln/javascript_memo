## at()

```js
let arr = [1, 2, 3, 4, 5];
console.log(arr.at(-1));

결과 : 5
```

## &&=

```js
let x = 5;
let y = 6;
x &&= y;
```

```txt
x &&=는 x && (x = y);
라는 의미이다.
x가 참이면 x = y로 처리하겠단 의미.
```

## ??=

```js
let x = null;
let y = 6;
x ??= y;
```

```txt
x?는 x가 true인지 보겠다는 것이다.
x??는 x가 null, undefined 중 하나인지 확인하겠다는 것.
```
