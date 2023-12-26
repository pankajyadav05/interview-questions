### Table of Contents

| No. | Questions                                                                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|     | **React**                                                                                                                                                    |
| 1   | [What is the difference between Element and Component?](#what-is-the-difference-between-element-and-component)                                               |
| 2   | [What are Pure Components?](#what-are-pure-components)                                                                                                       |
| 3   | [Why should we not update the state directly?](#why-should-we-not-update-the-state-directly)                                                                 |
| 4   | [What is Virtual DOM?](#what-is-virtual-dom)                                                                                                                 |
| 5   | [What is "key" prop and what is the benefit of using it in arrays of elements?](#what-is-key-prop-and-what-is-the-benefit-of-using-it-in-arrays-of-elements) |
|     | **Node.js**                                                                                                                                                  |
| 6   | [What do you mean by Asynchronous API?](#what-do-you-mean-by-asynchronous-api)                                                                               |
| 7   | [Is Node a single threaded application or multi-threaded?](#is-node-a-single-threaded-application-or-multi-threaded)                                         |
| 8   | [What is Callback Hell?](#what-is-callback-hell)                                                                                                             |
| 9   | [What is the purpose of setTimeout function?](#what-is-the-purpose-of-settimeout-function)                                                                   |
| 10  | [What's the difference between operational and programmer errors?](#whats-the-difference-between-operational-and-programmer-errors)                          |

1. ### What is the difference between Element and Component?

   An _Element_ is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. _Elements_ can contain other _Elements_ in their props. Creating a React element is cheap. Once an element is created, it cannot be mutated.

   The JavaScript representation(Without JSX) of React Element would be as follows:

   ```javascript
   const element = React.createElement("div", { id: "login-btn" }, "Login");
   ```

   and this element can be simiplified using JSX

   ```html
   <div id="login-btn">Login</div>
   ```

   The above `React.createElement()` function returns an object as below:

   ```javascript
   {
     type: 'div',
     props: {
       children: 'Login',
       id: 'login-btn'
     }
   }
   ```

   Finally, this element renders to the DOM using `ReactDOM.render()`.

   Whereas a **component** can be declared in several different ways. It can be a class with a `render()` method or it can be defined as a function. In either case, it takes props as an input, and returns a JSX tree as the output:

   ```javascript
   const Button = ({ handleLogin }) => (
     <div id={"login-btn"} onClick={handleLogin}>
       Login
     </div>
   );
   ```

   Then JSX gets transpiled to a `React.createElement()` function tree:

   ```javascript
   const Button = ({ handleLogin }) =>
     React.createElement(
       "div",
       { id: "login-btn", onClick: handleLogin },
       "Login"
     );
   ```

   **[⬆ Back to Top](#table-of-contents)**

2. ### What are Pure Components?

   Pure components are the components which render the same output for the same state and props. In function components, you can achieve these pure components through memoized `React.memo()` API wrapping around the component. This API prevents unnecessary re-renders by comparing the previous props and new props using shallow comparison. So it will be helpful for performance optimizations.

   But at the same time, it won't compare the previous state with the current state because function component itself prevents the unnecessary rendering by default when you set the same state again.

   The syntactic representation of memoized components looks like below,

   ```jsx
   const MemoizedComponent = memo(SomeComponent, arePropsEqual?);
   ```

   Below is the example of how child component(i.e., EmployeeProfile) prevents re-renders for the same props passed by parent component(i.e.,EmployeeRegForm).

   ```jsx
   import { memo, useState } from "react";

   const EmployeeProfile = memo(function EmployeeProfile({ name, email }) {
     return (
       <>
         <p>Name:{name}</p>
         <p>Email: {email}</p>
       </>
     );
   });
   export default function EmployeeRegForm() {
     const [name, setName] = useState("");
     const [email, setEmail] = useState("");
     return (
       <>
         <label>
           Name:{" "}
           <input value={name} onChange={(e) => setName(e.target.value)} />
         </label>
         <label>
           Email:{" "}
           <input value={email} onChange={(e) => setEmail(e.target.value)} />
         </label>
         <hr />
         <EmployeeProfile name={name} />
       </>
     );
   }
   ```

   In the above code, the email prop has not been passed to child component. So there won't be any re-renders for email prop change.

   In class components, the components extending _`React.PureComponent`_ instead of _`React.Component`_ become the pure components. When props or state changes, _PureComponent_ will do a shallow comparison on both props and state by invoking `shouldComponentUpdate()` lifecycle method.

   **Note:** `React.memo()` is a higher-order component.

   **[⬆ Back to Top](#table-of-contents)**

3. ### Why should we not update the state directly?

   If you try to update the state directly then it won't re-render the component.

   ```javascript
   //Wrong
   this.state.message = "Hello world";
   ```

   Instead use `setState()` method. It schedules an update to a component's state object. When state changes, the component responds by re-rendering.

   ```javascript
   //Correct
   this.setState({ message: "Hello World" });
   ```

   **Note:** You can directly assign to the state object either in _constructor_ or using latest javascript's class field declaration syntax.

   **[⬆ Back to Top](#table-of-contents)**

4. ### What is Virtual DOM?

   The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.

   **[⬆ Back to Top](#table-of-contents)**

5. ### What is "key" prop and what is the benefit of using it in arrays of elements?

   A `key` is a special attribute you **should** include when mapping over arrays to render data. _Key_ prop helps React identify which items have changed, are added, or are removed.

   Keys should be unique among its siblings. Most often we use ID from our data as _key_:

   ```jsx harmony
   const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
   ```

   When you don't have stable IDs for rendered items, you may use the item _index_ as a _key_ as a last resort:

   ```jsx harmony
   const todoItems = todos.map((todo, index) => (
     <li key={index}>{todo.text}</li>
   ));
   ```

   **Note:**

   1. Using _indexes_ for _keys_ is **not recommended** if the order of items may change. This can negatively impact performance and may cause issues with component state.
   2. If you extract list item as separate component then apply _keys_ on list component instead of `li` tag.
   3. There will be a warning message in the console if the `key` prop is not present on list items.
   4. The key attribute accepts either string or number and internally convert it as string type.

   **[⬆ Back to Top](#table-of-contents)**

6. ### What do you mean by Asynchronous API?

   All APIs of Node.js library are aynchronous that is non-blocking. It essentially means a Node.js based server never waits for a API to return data. Server moves to next API after calling it and a notification mechanism of Events of Node.js helps server to get response from the previous API call.

   **[⬆ Back to Top](#table-of-contents)**

7. ### Is Node a single threaded application or multi-threaded?

   Node uses a single threaded model with event looping.

   **[⬆ Back to Top](#table-of-contents)**

8. ### What is Callback Hell?

   The asynchronous function requires callbacks as a return parameter. When multiple asynchronous functions are chained together then callback hell situation comes up.

   **[⬆ Back to Top](#table-of-contents)**

9. ### What is the purpose of setTimeout function?

   The `setTimeout(cb, ms)` global function is used to run callback `cb` after at least `ms` milliseconds. The actual delay depends on external factors like OS timer granularity and system load. A timer cannot span more than 24.8 days.

   **[⬆ Back to Top](#table-of-contents)**

10. ### What's the difference between operational and programmer errors?

    Operation errors are not bugs, but problems with the system, like _request timeout_ or _hardware failure_. On the other hand programmer errors are actual bugs.

    **[⬆ Back to Top](#table-of-contents)**
