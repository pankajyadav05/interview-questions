# ATLYS FRONTEND VUE

## Table of Contents

1. [Vue Instance Lifecycle Hooks](#1-explain-the-vue-instance-lifecycle-hooks)
2. [Optimizing Performance in Vue](#2-how-would-you-optimize-performance-in-a-vue-application)
3. [Vue Provide/Inject](#3-what-is-the-provideinject-in-vue-and-when-would-you-use-it)
4. [Vue Computed Properties vs Watchers](#4-what-is-the-difference-between-computed-properties-and-watchers-in-vue)
5. [Vue Async Components](#5-what-are-async-components-in-vue)
6. [Vuex and Its Core Principles](#6-what-is-vuex-and-what-are-its-core-principles)
7. [Vuex Data Flow](#7-explain-the-vuex-data-flow-and-the-role-of-actions-mutations-and-the-store)
8. [Asynchronous Actions in Vuex](#8-how-do-you-handle-asynchronous-actions-in-vuex)
9. [Handling Side Effects in Vuex](#9-how-do-you-handle-side-effects-in-vuex-such-as-api-calls-or-subscriptions)
10. [Vuex DevTools](#10-what-are-vuex-devtools-and-how-do-you-use-them)

---

### 1. Explain the Vue Instance Lifecycle Hooks

The main lifecycle hooks in a Vue instance are:

- `beforeCreate` - Fired before the instance is initialized
- `created` - Fired after the instance is created
- `beforeMount` - Fired before the instance is mounted to the DOM
- `mounted` - Fired after the instance is mounted to the DOM
- `beforeUpdate` - Fired before the instance data is updated
- `updated` - Fired after the instance data is updated
- `beforeUnmount` - Fired before the instance is unmounted
- `unmounted` - Fired after the instance is unmounted

[↑ Scroll to Top](#interview-questions-guide)

---

### 2. How would you optimize performance in a Vue application?

Some ways to optimize performance in Vue include:

- Using `v-once` or `v-memo` for static content
- Code-splitting and lazy loading for better initial load times
- Avoiding unnecessary watchers and computed properties
- Using `Object.freeze` for immutable data structures
- Virtualized lists for rendering large lists efficiently

[↑ Scroll to Top](#interview-questions-guide)

---

### 3. What is the Provide/Inject in Vue and when would you use it?

Provide/Inject is a way to pass data from a parent component down to nested child components without having to pass props manually at every level. It's useful for sharing global state, services, or other data that needs to be accessed by multiple components.

[↑ Scroll to Top](#interview-questions-guide)

---

### 4. What is the difference between Computed Properties and Watchers in Vue?

Computed properties are cached based on their reactive dependencies and will only re-evaluate when some of their dependencies have changed. They are primarily used for complex data transformations and are more efficient than using methods.

Watchers are used to perform side effects or asynchronous operations in response to data changes. They are imperative and run on every change of the watched property.

[↑ Scroll to Top](#interview-questions-guide)

---

### 5. What are Async Components in Vue?

Async components are a way to lazily load Vue components when they are needed. Instead of importing the component upfront, you provide a function that returns a Promise resolving to the component definition. This can help improve initial load times and optimize performance.

[↑ Scroll to Top](#interview-questions-guide)

---

### 6. What is Vuex and what are its core principles?

Vuex is a state management pattern and library for Vue.js applications. Its core principles are:

- Single source of truth (the store)
- State is read-only
- Changes are made with mutations (synchronous)
- Asynchronous logic is handled with actions

[↑ Scroll to Top](#interview-questions-guide)

---

### 7. Explain the Vuex data flow and the role of actions, mutations, and the store.

The Vuex data flow follows these steps:

- A component dispatches an action with `store.dispatch(action)`
- The action handler (asynchronous) executes and commits a mutation
- The mutation handler (synchronous) updates the state in the store
- The store notifies subscribers (e.g., Vue components) of state changes
- Components re-render with the new state

[↑ Scroll to Top](#interview-questions-guide)

---

### 8. How do you handle asynchronous actions in Vuex?

In Vuex, asynchronous operations are handled with actions. Actions are dispatched from components and can contain asynchronous logic, such as API calls. Once the async operation is complete, the action commits a mutation to update the state.

[↑ Scroll to Top](#interview-questions-guide)

---

### 9. How do you handle side effects in Vuex, such as API calls or subscriptions?

Side effects in Vuex, such as API calls or subscriptions, are typically handled within actions. Actions can contain asynchronous logic, and once the side effect is complete, they commit a mutation to update the state.

[↑ Scroll to Top](#interview-questions-guide)

---

### 10. What are Vuex DevTools and how do you use them?

Vuex DevTools is a browser extension that provides debugging capabilities for Vuex applications. It allows you to inspect the state tree, view dispatched actions and mutations, and even time-travel through state changes.

[↑ Scroll to Top](#interview-questions-guide)
