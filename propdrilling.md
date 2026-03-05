# 1️⃣ What is Prop Drilling?

**Prop Drilling** is the process of passing data (props) from a **parent component to a deeply nested child component through multiple intermediate components**, even if those intermediate components do not use the data.

In simple words:

> Data is passed through many components just to reach the component that actually needs it.

---

# 2️⃣ Why Does Prop Drilling Happen?

React follows a **one-way data flow**:

```
Parent → Child → Grandchild → ...
```

A child component **cannot directly access parent data unless it is passed via props**.

So if a deeply nested component needs data from the top-level component, we must pass it through every level.

---

# 3️⃣ Example of Prop Drilling

Imagine this component structure:

```
App
 └── Parent
      └── Child
           └── GrandChild
```

The **GrandChild** component needs the `user` data.

---

## Step 1: App Component

```jsx
function App() {
  const user = "Aryan";

  return <Parent user={user} />;
}
```

---

## Step 2: Parent Component

Parent does not use `user`, but must pass it down.

```jsx
function Parent({ user }) {
  return <Child user={user} />;
}
```

---

## Step 3: Child Component

Child also does not use `user`, but must pass it.

```jsx
function Child({ user }) {
  return <GrandChild user={user} />;
}
```

---

## Step 4: GrandChild Component

Finally, the component that actually needs the data.

```jsx
function GrandChild({ user }) {
  return <h1>Hello {user}</h1>;
}
```

---

# 4️⃣ Visualization

Data flow looks like this:

```
App
 │
 ▼
Parent
 │
 ▼
Child
 │
 ▼
GrandChild
```

Even though **Parent and Child don't use the data**, they must pass it.

This unnecessary passing is **Prop Drilling**.

---

# 5️⃣ Problems Caused by Prop Drilling

## 1️⃣ Unnecessary Complexity

Many components pass props they don't use.

```
App → Parent → Child → GrandChild
```

Only **GrandChild** needs the data.

---

## 2️⃣ Hard to Maintain

If you add or remove components, you must update props everywhere.

Example:

```
App → Layout → Parent → Wrapper → Child → GrandChild
```

Now props must be passed through **5 components**.

---

## 3️⃣ Reduces Code Readability

Developers must track props across multiple files.

This makes debugging difficult.

---

## 4️⃣ Tight Coupling Between Components

Intermediate components become dependent on props they don't need.

---

# 6️⃣ Real Example (Common in Apps)

Suppose we have user authentication.

```
App
 └── Dashboard
      └── Sidebar
           └── Profile
```

User data comes from the top:

```jsx
const user = {
  name: "Aryan",
  role: "Admin"
};
```

We must pass it through every level:

```jsx
<Dashboard user={user} />
```

```jsx
<Sidebar user={user} />
```

```jsx
<Profile user={user} />
```

This is prop drilling.

---

# 7️⃣ How to Solve Prop Drilling

React provides **multiple solutions**.

---

# Solution 1️⃣ Context API (Most Common)

Instead of passing props through multiple components, we use **Context**.

Context allows data to be accessed directly by any component inside the provider.

---

## Step 1: Create Context

```jsx
import { createContext } from "react";

const UserContext = createContext();
```

---

## Step 2: Provide Context

```jsx
function App() {
  const user = "Aryan";

  return (
    <UserContext.Provider value={user}>
      <Parent />
    </UserContext.Provider>
  );
}
```

---

## Step 3: Use Context

```jsx
import { useContext } from "react";

function GrandChild() {
  const user = useContext(UserContext);

  return <h1>Hello {user}</h1>;
}
```

Now:

```
GrandChild directly accesses data
```

No prop drilling required.

---

# 8️⃣ Visualization With Context

Instead of:

```
App → Parent → Child → GrandChild
```

We get:

```
App (Provider)
     ↓
GrandChild (Consumer)
```

Intermediate components are skipped.

---

# 9️⃣ Other Solutions (Large Applications)

For large applications we use state management libraries:

### Popular ones include

* Redux
* Zustand
* Recoil
* MobX

These store global state outside the component tree.

---

# 🔟 When Prop Drilling is NOT a Problem

Prop drilling is acceptable when:

* Only 1–2 component levels
* Small application
* Data only needed by few components

Example:

```
Parent → Child
```

Passing props here is perfectly fine.

---

# 1️⃣1️⃣ Interview Answer (Best Way to Say It)

If interviewer asks:

**What is Prop Drilling?**

You can answer:

> Prop drilling is the process of passing data through multiple nested components using props, even when intermediate components do not need that data. It happens because React follows a unidirectional data flow. Prop drilling can make code difficult to maintain, so it is often solved using Context API or state management libraries like Redux.

---
