## setIntervel


### 개요

일정 시간마다 작동하는 함수

- 

### 구조

- **x**


### 용법

### 용례(code)

```txt

```

### code

```javascript
let inter;
let n = 1;
let m = 2;

const func = () => {
    console.log(n);
    n += m;
}

inter = setInterval(func , 1000, n, m);
```

### 참고 링크
        https://developer.mozilla.org/en-US/docs/Web/API/setInterval
