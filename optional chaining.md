```javascript
const adventurer = {
    name: 'Alice',
    cat: { name: 'Dinah' },
    dog: { name: 'JSON', tail: 'nope' },
    testMethod : (name) => `good job, ${name}!`,
  };
  
  const dogName = adventurer.dog?.name;
  const method = adventurer.testMethod?.(dogName);
  console.log(dogName);
  console.log(method);
```

![image](https://user-images.githubusercontent.com/39308313/143674720-f910db4c-7207-4347-9058-ffa110cf2a3f.png)
