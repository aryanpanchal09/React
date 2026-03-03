1. What is `useState`
2. How it works internally
3. Rules & common mistakes
4. What is `useEffect`
5. How it works internally
6. Dependency array deep understanding
7. Cleanup function
8. Common bugs (infinite loops etc.)
9. Real interview examples

Beginner-friendly but deep 🔥

---

# 🟢 PART 1: `useState` in Detail

---

# 🔹 What is `useState`?

`useState` is a Hook that allows functional components to:

👉 Store data
👉 Update data
👉 Trigger re-render

Before Hooks, only class components could use state.

Now functional components can too.

---

# 🔹 Basic Syntax

```jsx
const [state, setState] = useState(initialValue);
```

Example:

```jsx
const [count, setCount] = useState(0);
```

Here:

* `count` → current state value
* `setCount` → function to update state
* `0` → initial value

---

# 🔹 Simple Example

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

When button clicked:

```js
setCount(count + 1);
```

React:

1. Updates state
2. Re-renders component
3. Updates Virtual DOM
4. Updates only changed part in real DOM

---

# 🔹 Important Concept: Re-rendering

When state changes:

* Component function runs again
* JSX is recreated
* Virtual DOM compares
* Real DOM updates minimal part

State = Trigger for re-render.

---

# 🔹 Updating State Correctly

❌ Wrong:

```js
count = count + 1;
```

❌ Direct mutation:

```js
stateObj.name = "John";
```

✅ Correct:

```js
setCount(count + 1);
```

---

# 🔹 Functional Update (Very Important for Interviews)

Sometimes state depends on previous state.

Instead of:

```js
setCount(count + 1);
```

Better:

```js
setCount(prev => prev + 1);
```

Why?

Because state updates are **asynchronous** and may be batched.

---

# 🔹 Multiple State Variables

```jsx
const [name, setName] = useState("");
const [age, setAge] = useState(0);
```

Each state is independent.

Unlike class components, `useState` does NOT merge objects automatically.

---

# 🔹 Object State

```jsx
const [user, setUser] = useState({ name: "", age: 0 });
```

To update:

❌ Wrong:

```js
setUser({ name: "Aryan" });
```

This removes `age`.

✅ Correct:

```js
setUser(prev => ({
  ...prev,
  name: "Aryan"
}));
```

Because `useState` replaces state, not merges it.

---

# 🔹 When Should You Use useState?

* Form inputs
* Toggle UI
* Counters
* UI state (modal open/close)
* Local component state

---

# 🟢 PART 2: `useEffect` in Detail

---

# 🔹 What is `useEffect`?

`useEffect` is used for:

👉 Side effects
👉 API calls
👉 Timers
👉 Subscriptions
👉 DOM manipulation

In class components, we used lifecycle methods.
In functional components, we use `useEffect`.

---

# 🔹 Basic Syntax

```jsx
useEffect(() => {
  // side effect code
}, [dependencies]);
```

---

# 🔹 How useEffect Works Internally

React flow:

```plaintext
Render component
Commit changes to DOM
Then run useEffect
```

Important:

👉 `useEffect` runs AFTER render.

---

# 🔹 3 Important Patterns of useEffect

---

## 1️⃣ Run Once (Component Did Mount)

```jsx
useEffect(() => {
  console.log("Mounted");
}, []);
```

Empty dependency array → run only once.

Used for:

* API call on page load
* Initial setup

---

## 2️⃣ Run When Specific State Changes

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

Runs when:

* count changes

Used for:

* Reacting to state updates
* Fetch new data when ID changes

---

## 3️⃣ Run Every Render

```jsx
useEffect(() => {
  console.log("Runs every time");
});
```

No dependency array → runs on every render.

⚠ Usually not recommended.

---

# 🔹 Cleanup Function (Very Important)

If your effect creates:

* Timer
* Event listener
* Subscription

You must clean it.

Example:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

Return function = cleanup.

This runs when:

* Component unmounts
* Before next effect runs

---

# 🔹 Real Example: API Fetch

```jsx
function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

# 🔴 Common Bugs with useEffect

---

## ❌ Infinite Loop

```jsx
useEffect(() => {
  setCount(count + 1);
}, [count]);
```

This creates infinite loop because:

* count changes
* effect runs
* setCount runs
* count changes again

---

## ❌ Missing Dependency

```jsx
useEffect(() => {
  console.log(name);
}, []);
```

If `name` changes, effect won’t run.

React ESLint warns about missing dependencies.

---

# 🔹 Dependency Array Deep Understanding

```plaintext
[] → run once
[count] → run when count changes
no array → run every render
```

React compares dependencies using shallow comparison.

---

# 🔥 Real Interview Questions on useEffect

1. Why does useEffect run twice in Strict Mode?
   → React intentionally runs twice in development to detect side effects.

2. Difference between useEffect and useLayoutEffect?
   → useLayoutEffect runs before browser paint.

3. When does cleanup run?
   → Before next effect or on unmount.

---

# 🧠 Combined Example (Realistic)

```jsx
function CounterWithAPI() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count updated:", count);
  }, [count]);

  useEffect(() => {
    console.log("Component mounted");

    return () => {
      console.log("Component unmounted");
    };
  }, []);

  return (
    <button onClick={() => setCount(prev => prev + 1)}>
      {count}
    </button>
  );
}
```

---

# 🎯 Final Summary

Explain useState and useEffect.

You can say:

> useState is a hook that allows functional components to manage state. It returns a state value and a setter function. When the setter function is called, React re-renders the component.
>
> useEffect is used to handle side effects such as API calls, timers, and subscriptions. It runs after rendering and can be controlled using a dependency array. It can also return a cleanup function.

---

Master:

* Functional state updates
* Dependency array behavior
* Cleanup logic
* Avoiding infinite loops
* Async API inside useEffect
* Batching behavior
