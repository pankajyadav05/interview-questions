# Interview Questions Guide

## Table of Contents

1. [React Lifecycle Methods](#1-explain-the-lifecycle-methods-in-react-components)
2. [Optimizing Performance in React](#2-how-would-you-optimize-performance-in-a-react-application)
3. [React Context API](#3-what-is-the-context-api-in-react-and-when-would-you-use-it)
4. [Controlled vs Uncontrolled Components in React](#4-what-is-the-difference-between-controlled-and-uncontrolled-components-in-react)
5. [Suspense Component in React](#5-what-is-suspense-component)
6. [Redux and Its Core Principles](#6-what-is-redux-and-what-are-its-core-principles)
7. [Redux Data Flow](#7-explain-the-redux-data-flow-and-the-role-of-actions-reducers-and-the-store)
8. [Asynchronous Actions in Redux](#8-how-do-you-handle-asynchronous-actions-in-redux)
9. [Handling Side Effects in Redux](#9-how-do-you-handle-side-effects-in-redux-such-as-api-calls-or-subscriptions)
10. [Redux DevTools](#10-what-are-redux-devtools-and-how-do-you-use-them)

---

### 1. Explain the lifecycle methods in React components.

The main lifecycle methods are:

- `constructor()` - For initializing state and binding methods
- `render()` - Required method for rendering the component
- `componentDidMount()` - Invoked after the component mounts
- `componentDidUpdate()` - Invoked after updates happen
- `componentWillUnmount()` - Invoked before the component unmounts

[↑ Scroll to Top](#interview-questions-guide)

---

### 2. How would you optimize performance in a React application?

Some ways to optimize performance include:

- Using `shouldComponentUpdate` or `React.memo` for controlling re-renders
- Code-splitting and lazy loading for better initial load times
- Memoizing expensive computations with `useMemo` or `useCallback`
- Using immutable data structures to optimize re-renders
- Virtualized lists for rendering large lists efficiently

[↑ Scroll to Top](#interview-questions-guide)

---

### 3. What is the Context API in React and when would you use it?

The Context API allows you to pass data through the component tree without manually passing props at every level. It's useful for sharing global state, themes, or other data that needs to be accessed by multiple components.

[↑ Scroll to Top](#interview-questions-guide)

---

### 4. What is the difference between Controlled and Uncontrolled Components in React?

Controlled components are those where the component's state is fully managed by React, usually through props. Uncontrolled components manage their own state internally, and you need to query the DOM to get their values when needed.

[↑ Scroll to Top](#interview-questions-guide)

---

### 5. What is suspense component?

If the module containing the dynamic import is not yet loaded by the time parent component renders, you must show some fallback content while you’re waiting for it to load using a loading indicator. This can be done using **Suspense** component.

For example, the below code uses suspense component,

```javascript
const OtherComponent = React.lazy(() => import("./OtherComponent"));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

As mentioned in the above code, Suspense is wrapped above the lazy component.

[↑ Scroll to Top](#interview-questions-guide)

---

### 6. What is Redux and what are its core principles?

Redux is a predictable state management library for JavaScript applications. Its core principles are:

- Single source of truth (the store)
- State is read-only
- Changes are made with pure functions (reducers)

[↑ Scroll to Top](#interview-questions-guide)

---

### 7. Explain the Redux data flow and the role of actions, reducers, and the store.

The Redux data flow follows these steps:

- An action is dispatched with `store.dispatch(action)`
- The root reducer function is called with the current state and the dispatched action
- The root reducer delegates work to other reducers based on the action type
- The new state is calculated by the reducers and returned to the store
- The store updates its state and notifies subscribers (e.g., React components)

[↑ Scroll to Top](#interview-questions-guide)

---

### 8. How do you handle asynchronous actions in Redux?

Redux itself is synchronous. To handle asynchronous actions, you typically use middleware like `redux-thunk` or `redux-saga`. With `redux-thunk`, you can dispatch functions instead of actions, which can then perform async operations and dispatch actions when complete. With `redux-saga`, you use generator functions to handle side effects and asynchronous flows.

[↑ Scroll to Top](#interview-questions-guide)

---

### 9. How do you handle side effects in Redux, such as API calls or subscriptions?

To handle side effects in Redux, you typically use middleware like `redux-thunk` or `redux-saga`. With `redux-thunk`, you can dispatch functions that perform side effects and dispatch actions when done. With `redux-saga`, you use generator functions to manage side effects and async flows.

[↑ Scroll to Top](#interview-questions-guide)

---

### 10. What are Redux DevTools and how do you use them?

Redux DevTools is a browser extension that provides powerful debugging capabilities for Redux applications. It allows you to inspect the state tree, view dispatched actions, and even travel back in time by "canceling" actions.

[↑ Scroll to Top](#interview-questions-guide)
