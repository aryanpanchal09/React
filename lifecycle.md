1. What lifecycle means
2. Lifecycle phases
3. All major lifecycle methods (Class Components)
4. When they are used
5. How this maps to Hooks (`useEffect`) in modern React
6. Real interview examples

---

# 🌱 What Are React Lifecycle Methods?

Every React component goes through different stages from creation to removal.

Just like a human life:

```
Birth → Growth → Updates → Death
```

Similarly, a React component:

```
Mount → Update → Unmount
```

Lifecycle methods are **special methods in Class Components** that run automatically at different stages of a component’s life.

> Important: Lifecycle methods exist in **class components**.
> In functional components, we use Hooks (mainly `useEffect`) instead.

---

# 🧠 The 3 Main Lifecycle Phases

---

# 1️⃣ Mounting Phase (Component is created and inserted into the DOM)

This happens when:

* Component is rendered for the first time
* It appears on the screen

## Methods in Mounting Phase

### 1. constructor()

Runs first.

Used for:

* Initializing state
* Binding methods

Example:

```jsx
constructor(props) {
  super(props);
  this.state = { count: 0 };
}
```

📌 You rarely need constructor in modern React.

---

### 2. render()

Required method.

* Returns JSX
* Must be pure
* No side effects allowed

```jsx
render() {
  return <h1>Hello</h1>;
}
```

⚠ Never do API calls inside render.

---

### 3. componentDidMount()

🔥 Very Important

Runs after:

* Component is inserted into DOM
* First render is complete

Used for:

* API calls
* Setting timers
* Adding event listeners
* Fetching data

Example:

```jsx
componentDidMount() {
  fetch("https://api.example.com/users")
    .then(res => res.json())
    .then(data => this.setState({ users: data }));
}
```

📌 This is the most commonly used lifecycle method.

---

# 2️⃣ Updating Phase (When props or state changes)

This phase happens when:

* `setState()` is called
* Props change
* Parent re-renders

---

## Methods in Updating Phase

### 1. shouldComponentUpdate(nextProps, nextState)

Used to control re-rendering.

Returns:

* true → re-render
* false → skip re-render

Example:

```jsx
shouldComponentUpdate(nextProps, nextState) {
  return nextState.count !== this.state.count;
}
```

📌 Used for performance optimization.

---

### 2. render()

Runs again when component updates.

---

### 3. componentDidUpdate(prevProps, prevState)

Runs after update is reflected in DOM.

Used for:

* Comparing old vs new values
* Making API calls when certain state changes
* Reacting to prop changes

Example:

```jsx
componentDidUpdate(prevProps) {
  if (prevProps.userId !== this.props.userId) {
    fetchNewUserData();
  }
}
```

⚠ Important:
If you call `setState()` here without condition → infinite loop.

---

# 3️⃣ Unmounting Phase (Component is removed from DOM)

This happens when:

* Component disappears
* Route changes
* Conditional rendering removes it

---

## Method in Unmounting Phase

### componentWillUnmount()

Runs just before component is removed.

Used for:

* Cleaning timers
* Removing event listeners
* Canceling API calls
* Avoiding memory leaks

Example:

```jsx
componentWillUnmount() {
  clearInterval(this.timer);
}
```

Very important in large apps.

---

# 🧩 Full Lifecycle Order

When component loads:

```
constructor()
render()
componentDidMount()
```

When state updates:

```
shouldComponentUpdate()
render()
componentDidUpdate()
```

When component is removed:

```
componentWillUnmount()
```

---

# ⚡ What About Functional Components?

Modern React uses Hooks instead of lifecycle methods.

Main hook:

## useEffect()

It replaces:

* componentDidMount
* componentDidUpdate
* componentWillUnmount

---

# 🔁 Mapping Lifecycle to useEffect

---

## 🔹 componentDidMount Equivalent

```jsx
useEffect(() => {
  console.log("Mounted");
}, []);
```

Empty dependency array → runs once.

---

## 🔹 componentDidUpdate Equivalent

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

Runs when `count` changes.

---

## 🔹 componentWillUnmount Equivalent

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

---

# 🔥 Real Interview Example

## Example: API Fetch Component

Class Component:

```jsx
class Users extends React.Component {
  state = { users: [] };

  componentDidMount() {
    fetch("/api/users")
      .then(res => res.json())
      .then(data => this.setState({ users: data }));
  }

  componentWillUnmount() {
    console.log("Cleanup if needed");
  }

  render() {
    return (
      <ul>
        {this.state.users.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    );
  }
}
```

---

# 🚨 Common Interview Mistakes

1. Doing API calls inside render()
2. Calling setState inside componentDidUpdate without condition
3. Forgetting cleanup in timers
4. Not understanding mounting vs updating difference

---
