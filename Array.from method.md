## About Array.from method

### 개요

- 배열을 인자로 받아 처리하거나, 인자를 받아 배열로 만들거나, 배열을 만드는 메소드

### 언제 쓰나?

- Array를 편하게 만들 때 썼다. 아직까진.

### code

```javascript
let arr = Array.from({length: 3}, (_, i) => i+1);
```

### 참고 링크
[MDN 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from#array_from_a_map)
