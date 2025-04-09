## Closures

A `closures` is a function that "remembers" the variables from its lexical scope even when the function is executed outside that scope.

In simple terms: 
```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2 (it remembers `count`)

```
This is possible because functions are first-class citizens in JavaScript.


## Why are Closures useful?
- Data privacy (private variables)
- Maintain internal state
- Memory efficiency
- Used in callbacks, timers, event handlers, and more


### Execution Context + Lexical Scope
➤ Execution Context <br/>
The environment where JavaScript code is evaluated. Each function call creates a new execution context with its own variables.

➤ Lexical Scope <br/>
The scope is determined at the time of writing code, not at runtime.
A function has access to variables defined in the scope where it was declared, not necessarily where it's called.

### Closure in Action: Memoization Cache


- Function factory
```javascript
function memoize(fn) {
  const cache = {}; // Closure keeps this cache alive

   return function(...args) {
    const key = JSON.stringify(args);
    
    if (cache[key] !== undefined) {
      console.log('Fetching from cache:', key);
      return cache[key];
    }

    console.log('Calculating:', key);
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}
```

- Function
```javascript
function slowAdd(a, b) {
  // Simulate slow computation
  for (let i = 0; i < 1e8; i++) {}
  return a + b;
}

const memoizedAdd = memoize(slowAdd);

console.log(memoizedAdd(2, 3)); // Calculating: [2,3]
console.log(memoizedAdd(2, 3)); // Fetching from cache: [2,3]
```

<br/>


## Summary
| Concept | Description |
|---|---|
| Closure | A function that remembers variables from its outer scope
| Execution Context | The environment where code runs (variables, scope, etc.)
| Lexical Scope | Scope is defined based on where functions are written
| Use Case | Memoization, private data, keeping state in callbacks, etc.