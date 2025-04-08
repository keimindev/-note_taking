## Call Stack

The `Call Stack` is a data structure used by the JavaScript engine to keep track of function calls. When a function is called, it's pushed onto the stack. When the function returns, it's popped off the stack. LIFO (Last-In, First-Out) structure.

- Javascript executes synchronously, one operation at a time, using the call stack. 

```javscript
function greet() {
  console.log("Hello");
}
function start() {
  greet();
}
start();
```

then

```scss
start() -> greet() -> console.log()
```

<br/>
<br/>

## Event Loop

The `Event Loop` allows JavaScript to handle asynchronous operations despite being single-threaded.
While the Call Stack runs synchronous code, asynchronous callbacks(like `setTimeout` or `fetch`) are queued and executed later by the Event Loop after the current call stack is empty. 


```javascript
console.log('1');

setTimeout(() => {
  console.log('2 (setTimeout)');
}, 0);

Promise.resolve().then(() => {
  console.log('3 (Promise)');
});

console.log('4');
```

then 
```javascript
1
4
3
2
```

### 🧠 Why?
`1` is printed immediately.

`setTimeout` is asynchronous and goes to the macrotask queue.

`Promise.then` goes to the microtask queue, which is processed before macrotasks.

`4` runs because it's synchronous.

Then the microtask `3` runs.

Finally, the setTimeout `2` runs.


### Work Flow

1. code runs top to bottom using Call Stack 
2. asychronous code is encountered, it's handed off to the Web APIs.
3. After async task completes, its callback is pushed to a Task Queue or Microtask Queue.
4. The Event Loop checks if the call stack is empty. If it is, pushes a task from the queue to the stack.