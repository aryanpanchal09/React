# 1️⃣ What is a Higher-Order Function?

A **Higher-Order Function (HOF)** is a function that:

1. **Takes another function as an argument**, OR
2. **Returns another function as its result**, OR
3. **Both**

### Simple Definition

> A Higher-Order Function is a function that works with other functions.

In JavaScript, functions are treated as **first-class citizens**, meaning they can be:

* Stored in variables
* Passed as arguments
* Returned from other functions

This allows higher-order functions to exist.

---

# 2️⃣ Example: Function as a Parameter

Example:

```javascript
function greet(name) {
  return "Hello " + name;
}

function processUserInput(callback) {
  const name = "Aryan";
  console.log(callback(name));
}

processUserInput(greet);
```

### What happens?

1. `processUserInput` receives a function (`greet`)
2. It calls that function
3. `greet` executes

Here:

```javascript
processUserInput
```

is a **Higher-Order Function**.

---

# 3️⃣ Example: Function Returning Another Function

Example:

```javascript
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5));
```

Output:

```text
10
```

### Explanation

1. `multiplier(2)` returns a function
2. That returned function multiplies numbers by 2

So:

```javascript
multiplier
```

is a **Higher-Order Function** because it **returns a function**.

---

# 4️⃣ Why Higher-Order Functions Are Important

Higher-order functions help with:

### 1️⃣ Code Reusability

You write generic functions that work with different logic.

### 2️⃣ Cleaner Code

Functional programming style.

### 3️⃣ Abstraction

Separate logic from behavior.

### 4️⃣ Flexibility

Functions become dynamic.

---

# 5️⃣ Common Built-in Higher-Order Functions in JavaScript

JavaScript has many built-in higher-order functions.

---

# 1️⃣ map()

Transforms array elements.

Example:

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(function(num) {
  return num * 2;
});

console.log(doubled);
```

Output:

```text
[2,4,6,8]
```

Here:

* `map()` is a **higher-order function**
* It receives a callback function.

---

# 2️⃣ filter()

Filters array values.

Example:

```javascript
const numbers = [1,2,3,4,5];

const evenNumbers = numbers.filter(function(num){
  return num % 2 === 0;
});
```

Output:

```text
[2,4]
```

---

# 3️⃣ reduce()

Reduces array into a single value.

Example:

```javascript
const numbers = [1,2,3,4];

const sum = numbers.reduce(function(acc, curr){
  return acc + curr;
},0);
```

Output:

```text
10
```

---

# 6️⃣ Higher-Order Functions with Arrow Functions

Modern JavaScript uses arrow functions.

Example:

```javascript
const numbers = [1,2,3];

const squared = numbers.map(num => num * num);
```

Cleaner and shorter.

---

# 7️⃣ Real-World Example

Imagine logging functionality.

Instead of repeating code:

```javascript
function add(a,b){
  console.log("Adding numbers");
  return a+b;
}
```

We create a higher-order function.

```javascript
function logger(fn){
  return function(...args){
    console.log("Function called");
    return fn(...args);
  }
}

function add(a,b){
  return a+b;
}

const loggedAdd = logger(add);

loggedAdd(2,3);
```

Output:

```text
Function called
5
```

This is **function wrapping**.

---

# 8️⃣ Higher-Order Functions in React

React uses HOFs frequently.

Example: Rendering lists.

```jsx
const users = ["Aryan", "Rahul", "Priya"];

return (
  <ul>
    {users.map(user => (
      <li key={user}>{user}</li>
    ))}
  </ul>
);
```

Here:

```javascript
map()
```

is a **higher-order function**.

---

# 9️⃣ Higher-Order Components (HOC)

In React, a **Higher-Order Component** is inspired by higher-order functions.

A **Higher-Order Component** is:

> A function that takes a component and returns a new enhanced component.

Example:

```jsx
function withLogger(Component){
  return function(props){
    console.log("Component rendered");
    return <Component {...props} />;
  }
}
```

Usage:

```jsx
const EnhancedComponent = withLogger(MyComponent);
```

---

# 🔟 Real Interview Explanation

If interviewer asks:

**What is a Higher-Order Function?**

Best answer:

> A Higher-Order Function is a function that either takes another function as an argument or returns another function as a result. It is a fundamental concept in functional programming and is commonly used in JavaScript with functions like map, filter, and reduce.

---

# 1️⃣1️⃣ Real Benefits

Higher-order functions help with:

* Functional programming
* Code reuse
* Separation of concerns
* Cleaner code
* React component abstraction

---

# 1️⃣2️⃣ Difference Between HOF and Callback

| Concept               | Description                                |
| --------------------- | ------------------------------------------ |
| Callback              | Function passed as argument                |
| Higher-Order Function | Function that accepts or returns functions |

Example:

```javascript
array.map(callback)
```

* `map` → Higher-Order Function
* `callback` → Function passed inside

---

# 1️⃣3️⃣ Advanced Example (Closure + HOF)

```javascript
function createCounter(){
  let count = 0;

  return function(){
    count++;
    return count;
  }
}

const counter = createCounter();

console.log(counter());
console.log(counter());
```

Output:

```text
1
2
```

Here:

* Function returns another function
* Inner function remembers outer variable (closure)

---

# 🎯 Final Summary

A **Higher-Order Function**:

✔ Accepts functions as arguments
✔ Returns functions
✔ Enables functional programming
✔ Used heavily in JavaScript and React

Examples include:

```text
map()
filter()
reduce()
forEach()
setTimeout()
```

---

