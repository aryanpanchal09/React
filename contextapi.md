# 1️⃣ What is Context API in React?

The **Context API** is a built-in feature of React that allows you to **share data between components without passing props manually through every level of the component tree**.

It solves the **prop drilling problem**.

### Simple Definition

> Context API allows global data to be accessed by any component in the component tree without passing props through intermediate components.

---

# 2️⃣ Why Context API is Needed

React follows **unidirectional data flow**:

```text
Parent → Child → Grandchild
```

If a deeply nested component needs data from a top-level component, we must pass it through multiple layers.

Example without Context:

```
App
 └── Layout
      └── Navbar
           └── Profile
```

If `Profile` needs user data:

```jsx
<App user={user} />
<Layout user={user} />
<Navbar user={user} />
<Profile user={user} />
```

Even though **Layout and Navbar don't use the data**, they must pass it.

This is **prop drilling**.

Context solves this problem.

---

# 3️⃣ Key Concepts of Context API

Context API has **three main parts**:

### 1. Context Object

Created using `createContext()`.

### 2. Provider

Provides data to the component tree.

### 3. Consumer

Accesses the data from context.

---

# 4️⃣ Step-by-Step Example

---

# Step 1: Create Context

```jsx
import { createContext } from "react";

export const UserContext = createContext();
```

This creates a **Context object**.

---

# Step 2: Provide Context

Wrap the components with a **Provider**.

```jsx
import { UserContext } from "./UserContext";

function App() {
  const user = "Aryan";

  return (
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}
```

Now every component inside `Dashboard` can access `user`.

---

# Step 3: Consume Context

Use the `useContext` hook.

```jsx
import { useContext } from "react";
import { UserContext } from "./UserContext";

function Profile() {
  const user = useContext(UserContext);

  return <h1>Hello {user}</h1>;
}
```

Now `Profile` can access the data **without prop drilling**.

---

# 5️⃣ Visual Flow

Without Context:

```
App
 ↓
Layout
 ↓
Navbar
 ↓
Profile
```

Props passed through every level.

---

With Context:

```
App (Provider)
 ↓
Any Component
 ↓
Profile (Consumer)
```

Components access the value directly.

---

# 6️⃣ Context with Multiple Values

You can store multiple values in context.

Example:

```jsx
const userData = {
  name: "Aryan",
  role: "Admin"
};
```

Provider:

```jsx
<UserContext.Provider value={userData}>
```

Consumer:

```jsx
const { name, role } = useContext(UserContext);
```

---

# 7️⃣ Using Context with State

Often we combine **Context + useState**.

Example: Theme switcher.

```jsx
import { createContext, useState } from "react";

export const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

Now any component can change the theme.

Consumer:

```jsx
const { theme, setTheme } = useContext(ThemeContext);
```

---

# 8️⃣ Real-World Use Cases

Context is commonly used for:

### Authentication

```
User login state
```

### Theme

```
Dark / Light mode
```

### Language settings

```
English / Spanish
```

### Global UI state

```
Sidebar open/close
```

---

# 9️⃣ Context API vs Props

| Feature          | Props              | Context             |
| ---------------- | ------------------ | ------------------- |
| Data flow        | Parent → Child     | Global              |
| Prop drilling    | Yes                | No                  |
| Setup complexity | Simple             | Slightly more setup |
| Best for         | Small data sharing | Global state        |

---

# 🔟 Context API vs Redux

| Feature     | Context API       | Redux      |
| ----------- | ----------------- | ---------- |
| Built-in    | Yes               | No         |
| Setup       | Simple            | Complex    |
| Performance | Medium            | High       |
| Best for    | Small-medium apps | Large apps |

Context is good for:

* Theme
* Authentication
* Global UI state

Redux is better for:

* Complex state logic
* Large applications
* Many state updates

---

# 1️⃣1️⃣ Performance Problem with Context

One important issue:

**When Context value changes, all consuming components re-render.**

Example:

```
ThemeContext changes
```

All components using that context re-render.

This can cause performance problems in large apps.

Solutions:

* Split contexts
* Use memoization
* Use Redux or Zustand

---

# 1️⃣2️⃣ Multiple Context Example

You can create multiple contexts.

Example:

```jsx
<AuthContext.Provider>
  <ThemeContext.Provider>
    <App />
  </ThemeContext.Provider>
</AuthContext.Provider>
```

Components can use both contexts.

---

# 1️⃣3️⃣ Best Practices

### ✔ Use Context for global data

Examples:

* User authentication
* Theme
* Language

---

### ✔ Keep Context small

Avoid storing huge state.

---

### ✔ Split Contexts

Instead of:

```
AppContext
```

Use:

```
AuthContext
ThemeContext
SettingsContext
```

---

### ✔ Use custom hooks

Example:

```jsx
export const useAuth = () => useContext(AuthContext);
```

Cleaner usage.

---

# 1️⃣4️⃣ Example with Custom Hook

Context:

```jsx
const AuthContext = createContext();
```

Provider:

```jsx
export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      {children}
    </AuthContext.Provider>
  );
}
```

Custom hook:

```jsx
export const useAuth = () => useContext(AuthContext);
```

Usage:

```jsx
const { user } = useAuth();
```

Cleaner code.

---

# 1️⃣5️⃣ Interview Answer (Best Version)

If an interviewer asks:

**What is Context API?**

You can say:

> The Context API is a built-in React feature used for sharing global data between components without passing props manually through every level of the component tree. It helps solve the prop drilling problem and is commonly used for global state such as authentication, themes, and user settings.

---
