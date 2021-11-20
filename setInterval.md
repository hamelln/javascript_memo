## setIntervel이란?

### 개요

- 일정 시간마다 작동하는 함수

### 언제 쓰나?

- 어떤 동작을 주기적으로 반복해서 실행할 때 사용. 한 번만 쓰고 끝내려면 setTimeout를 사용.
- 동작을 끝낼 때는 clearInterval()을 사용.

### 용법

```txt
var intervalID = setInterval(func, [delay, arg1, arg2, ...]);
var intervalID = setInterval(function[, delay]);
var intervalID = setInterval(code, [delay]);
```

### 용례(code)

```javascript
let inter;
let n = 1;
let m = 2;

const func = () => {
    console.log(n);
    n += m;
    if(n > 10) {
        clearInterval(inter);
        inter = null;
    }
}

inter = setInterval(func , 1000, n, m);
```

### 결과

![image](https://user-images.githubusercontent.com/39308313/142716068-4e027e46-6aaa-47b7-ade9-8e3a565c7046.png)

### 참고 링크
(ttps://developer.mozilla.org/en-US/docs/Web/API/setInterval){:target="_blank"}
