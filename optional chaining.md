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
