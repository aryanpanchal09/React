# 1 What is React and Why is it Popular?

## What is React?

React is a **JavaScript library for building user interfaces**, primarily for web applications.

It was developed by
Meta (formerly Facebook) in 2013.

Important:
👉 React is a **library**, not a full framework.
It focuses only on the **View layer (UI)**.

---

## Core Philosophy of React

React is based on 3 main principles:

### 1 Component-Based Architecture

Everything is built as reusable components.

Instead of writing large monolithic code:

```
Navbar
Sidebar
Dashboard
Card
Button
Modal
```

Each is a separate reusable component.

---

### 2 Declarative Programming

Instead of manually manipulating the DOM:

```js
document.getElementById("root").innerHTML = ...
```

You declare what UI should look like:

```jsx
return <h1>Hello</h1>
```

React handles DOM updates automatically.

---

### 3 Virtual DOM & Reconciliation

React maintains a **Virtual DOM** (in memory copy of actual DOM).

Process:

1. State changes
2. New Virtual DOM is created
3. React compares old vs new (Diffing Algorithm)
4. Updates only changed nodes in real DOM

This process is called **Reconciliation**.

👉 This improves performance significantly.

---

## Why React is Popular?

### ✅ Reusable Components

Reduces duplication.

### ✅ Performance

Virtual DOM + efficient diffing.

### ✅ Large Ecosystem

* React Router
* Redux
* Zustand
* Next.js
* Massive npm ecosystem

### ✅ Hooks

Hooks simplified state and lifecycle logic.

### ✅ Strong Community & Jobs

Huge demand in MERN stack.

---

# 2️⃣ What is a Single Page Application (SPA)?

A **Single Page Application (SPA)** loads a single HTML page and dynamically updates content without full-page reload.

---

## How Traditional Apps Work

1. User clicks link
2. Browser requests new page
3. Server sends full HTML
4. Page reloads

---

## How SPA Works

1. Browser loads one HTML file
2. JavaScript loads app
3. API calls fetch data
4. UI updates dynamically

---

## Example

Instead of:

```
/home.html
/about.html
/contact.html
```

We have:

```
index.html
```

And routing is handled client-side.

---

## Benefits of SPA

* Faster navigation
* Better user experience
* Reduced server load

---

## Downsides

* SEO issues (unless SSR used)
* Large initial bundle size

---

# 3 What is JSX and How Does it Differ from HTML?

## What is JSX?

JSX = JavaScript XML

It allows writing HTML-like syntax inside JavaScript.

Example:

```jsx
const element = <h1>Hello</h1>;
```

But JSX is NOT HTML.

It gets transpiled (by Babel) into:

```js
React.createElement("h1", null, "Hello");
```

---

## How JSX Works Internally

JSX → Babel → JavaScript → React.createElement → Virtual DOM Object

---

## Major Differences Between JSX & HTML

### 🔹 class vs className

```jsx
<div className="box"></div>
```

### 🔹 for vs htmlFor

```jsx
<label htmlFor="email"></label>
```

### 🔹 Self-closing tags required

```jsx
<img />
```

### 🔹 JavaScript inside {}

```jsx
<h1>{name}</h1>
```

### 🔹 Inline styles use objects

```jsx
<div style={{ color: "red" }}></div>
```

---

# 4 Functional vs Class Components

## Class Components (Old Approach)

```jsx
class Counter extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  render() {
    return <h1>{this.state.count}</h1>;
  }
}
```

They use:

* Lifecycle methods

  * componentDidMount
  * componentDidUpdate
  * componentWillUnmount

---

## Functional Components (Modern)

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <h1>{count}</h1>;
}
```

They use Hooks:

* useState
* useEffect
* useContext
* useMemo
* useCallback

---

## Major Differences

| Functional | Class             |
| ---------- | ----------------- |
| No `this`  | Uses `this`       |
| Hooks      | Lifecycle methods |
| Cleaner    | More boilerplate  |
| Preferred  | Legacy            |

👉 Interview tip: Today 99% of production uses functional components.

---

# 5 Stateless vs Stateful Components

## Stateless Component

* No state
* Only receives props
* Pure function

```jsx
function Greeting({ name }) {
  return <h1>Hello {name}</h1>;
}
```

---

## Stateful Component

* Manages internal state
* UI changes over time

```jsx
function Counter() {
  const [count, setCount] = useState(0);
}
```

---

💡 Important:

Earlier:

* Functional = Stateless
* Class = Stateful

Now:
Functional can also be stateful (because of Hooks).

---

# 6 What are Props in React?

Props = Read-only inputs to components.

Used to pass data from parent → child.

---

## Example

Parent:

```jsx
<User name="Aryan" age={22} />
```

Child:

```jsx
function User({ name, age }) {
  return <p>{name} is {age} years old</p>;
}
```

---

## Important Characteristics

* Immutable (cannot modify)
* Passed top-down
* Helps create reusable components

---

## Advanced Concept: Prop Drilling

When props are passed through multiple layers unnecessarily.

Solution:

* Context API
* Redux

---

# 7 Difference Between State and Props

| Props                  | State                     |
| ---------------------- | ------------------------- |
| Passed from parent     | Managed internally        |
| Immutable              | Mutable                   |
| Used for configuration | Used for dynamic behavior |
| External               | Internal                  |

---

## Real Interview Answer

> Props are external, read-only data passed into a component, while state is internal, mutable data that controls component behavior.

---

# 8 Controlled vs Uncontrolled Components

This concept mainly applies to form inputs.

---

## Controlled Component

React controls the value.

```jsx
const [email, setEmail] = useState("");

<input 
  value={email}
  onChange={(e) => setEmail(e.target.value)}
/>
```

React state = single source of truth.

Advantages:

* Easy validation
* Predictable
* Better debugging

---

## Uncontrolled Component

DOM controls input value.

```jsx
const inputRef = useRef();

<input ref={inputRef} />
```

Value accessed via:

```js
inputRef.current.value
```

---

## Comparison

| Controlled            | Uncontrolled     |
| --------------------- | ---------------- |
| Uses state            | Uses ref         |
| More React way        | More traditional |
| Better for validation | Quick & simple   |

---

# 9 Purpose of `key` Attribute in Lists

When rendering lists:

```jsx
{users.map(user => (
  <li key={user.id}>{user.name}</li>
))}
```

---

## Why Key is Important?

React needs to:

* Identify elements uniquely
* Compare old vs new list
* Decide what changed

Without keys:

* Wrong re-renders
* Performance issues
* UI bugs

---

## Why Not Use Index as Key?

If items reorder:

* React gets confused
* Wrong element reused

Use stable unique IDs.

---

# 10 What are Fragments in React?

Fragments let you group multiple elements without adding extra DOM nodes.

---

## Problem Without Fragment

```jsx
return (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
);
```

Unnecessary div added.

---

## Solution: Fragment

```jsx
return (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
);
```

Equivalent to:

```jsx
<React.Fragment>
```

---

## Why Use Fragments?

* Avoid extra DOM nodes
* Cleaner HTML
* Better performance
* Required when returning multiple elements

---

## What is Virtual DOM?

The **Virtual DOM** is:

👉 A lightweight JavaScript object
👉 A copy of the real DOM
👉 Stored in memory

React does NOT directly update the real DOM.

Instead:

```
State changes
    ↓
New Virtual DOM created
    ↓
Compare with old Virtual DOM
    ↓
Update only changed parts in Real DOM
```

This comparison process is called:

### 🔹 Reconciliation

React uses a **diffing algorithm** to find differences.

---

## Example

Suppose we have:

```jsx
<h1>Hello Aryan</h1>
```

Now state changes:

```jsx
<h1>Hello John</h1>
```

React:

* Creates new Virtual DOM
* Compares old vs new
* Sees only text changed
* Updates only text node

Instead of re-rendering entire page.

---

## Why is it Faster?

Because:

* React batches updates
* Only updates necessary nodes
* Avoids full page re-render
* Works in memory first (cheap)

---

## Important Interview Line:

> Virtual DOM is a lightweight JavaScript representation of the real DOM. React uses it to compare changes efficiently and update only the necessary parts of the actual DOM, improving performance.

---

# 12 What are React Lifecycle Methods and when are they used?

Lifecycle methods describe:

👉 Different stages of a component’s life.

Like a human life cycle:

* Born
* Grow
* Update
* Die

Similarly, a component has 3 main phases:

---

## 🔹 1. Mounting Phase (Component is created)

When component appears on screen.

Important lifecycle methods (Class Components):

* `constructor()`
* `render()`
* `componentDidMount()`

### componentDidMount()

Used for:

* API calls
* Setting timers
* Initializing data

Example:

```jsx
componentDidMount() {
  fetch("https://api.example.com")
}
```

---

## 🔹 2. Updating Phase (When state or props change)

Methods:

* `render()`
* `componentDidUpdate()`

Used for:

* Reacting to state changes
* Re-fetching data
* Running side effects

---

## 🔹 3. Unmounting Phase (Component removed)

Method:

* `componentWillUnmount()`

Used for:

* Clearing timers
* Cleaning event listeners
* Preventing memory leaks

Example:

```jsx
componentWillUnmount() {
  clearInterval(this.timer);
}
```

---

## Important

Lifecycle methods are mostly used in:

👉 Class Components

In modern React (Functional Components), we use:

👉 `useEffect()` instead.

---

# 13 Explain `useState` and `useEffect` Hooks

Hooks allow functional components to:

* Use state
* Use lifecycle features

---

# 🔹 useState Hook

Used to create and manage state.

---

## Basic Syntax

```jsx
const [state, setState] = useState(initialValue);
```

---

## Example: Counter

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

---

## What Happens Internally?

* React stores state value
* When `setCount()` is called:

  * Component re-renders
  * Virtual DOM updates

---

## Important Points

* State updates are asynchronous
* Updating state causes re-render
* Do not modify state directly

❌ Wrong:

```js
count = count + 1;
```

✅ Correct:

```js
setCount(count + 1);
```

---

# 🔹 useEffect Hook

Used for:

* Side effects
* API calls
* Timers
* Subscriptions
* DOM updates

---

## Basic Syntax

```jsx
useEffect(() => {
  // side effect
}, [dependencies]);
```

---

## Example: Run Once (like componentDidMount)

```jsx
useEffect(() => {
  console.log("Component Mounted");
}, []);
```

Empty array = run only once.

---

## Example: Run on State Change

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

Runs whenever `count` changes.

---

## Example: Cleanup (like componentWillUnmount)

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

Return function = cleanup.

---

## Interview Summary:

* `useState` → manages state
* `useEffect` → handles side effects and lifecycle logic

---

# 14 What is Props Drilling?

Props drilling means:

👉 Passing props through multiple intermediate components just to reach a deeply nested child.

---

## Example

```jsx
App
 └── Parent
       └── Child
             └── GrandChild
```

If `App` has data:

```jsx
<App user="Aryan" />
```

We pass it like:

```jsx
<Parent user={user} />
<Child user={user} />
<GrandChild user={user} />
```

Even if Parent and Child don’t use it.

---

## Problem

* Unnecessary prop passing
* Hard to maintain
* Messy code

---

## Solution

* Context API
* Redux
* Zustand

---

## Interview Line

> Props drilling is the process of passing data through multiple nested components via props, even when intermediate components do not use that data.

---

# 15 What is the Context API and how is it used?

Context API is a way to:

👉 Share global data
👉 Without passing props manually at every level

---

## When to Use Context?

* User authentication
* Theme (dark/light)
* Language preference
* Global settings

---

## Step 1: Create Context

```jsx
import { createContext } from "react";

const UserContext = createContext();
```

---

## Step 2: Provide Value

```jsx
<UserContext.Provider value="Aryan">
  <Child />
</UserContext.Provider>
```

---

## Step 3: Consume Value

```jsx
import { useContext } from "react";

const user = useContext(UserContext);
```

Now any component inside Provider can access value.

---

## Visual Structure

```
Provider
   ↓
Any nested component
```

---

## Why Context is Better than Props Drilling?

Instead of:

```jsx
<Parent user={user} />
<Child user={user} />
<GrandChild user={user} />
```

We just use:

```jsx
useContext(UserContext)
```

---

## Important Limitation

Context is good for:

* Small to medium global state

For large apps:

* Redux is better
