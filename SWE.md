### Table of Contents

| No. | Questions                                                                                                            |
| --- | -------------------------------------------------------------------------------------------------------------------- |
|     | **React**                                                                                                            |
| 1   | [What is Virtual DOM?](#what-is-virtual-dom)                                                                         |
| 2   | [What is React lazy function?](#what-is-react-lazy-function)                                                         |
| 3   | [Why does strict mode render twice in React?](#why-does-strict-mode-render-twice-in-react)                           |
| 4   | [What is the difference between useState and useRef hook?](#what-is-the-difference-between-usestate-and-useref-hook) |
| 5   | [What is state mutation and how to prevent it?](#what-is-state-mutation-and-how-to-prevent-it)                       |
| 6   | [What is suspense component?](#what-is-suspense-component)                                                           |
|     | **Node.js**                                                                                                          |
| 7   | [Is Node a single threaded application or multi-threaded?](#is-node-a-single-threaded-application-or-multi-threaded) |
| 8   | [What is Callback Hell?](#what-is-callback-hell)                                                                     |
| 9   | [What is the purpose of setTimeout function?](#what-is-the-purpose-of-settimeout-function)                           |
| 10  | [How can you listen on port 80 with Node?](#how-can-you-listen-on-port-80-with-node)                                 |

1. ### What is Virtual DOM?

   The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.

   **[⬆ Back to Top](#table-of-contents)**

2. ### What is React lazy function?

   The `React.lazy` function lets you render a dynamic import as a regular component. It will automatically load the bundle containing the `OtherComponent` when the component gets rendered. This must return a Promise which resolves to a module with a default export containing a React component.

   ```jsx
   const OtherComponent = React.lazy(() => import("./OtherComponent"));

   function MyComponent() {
     return (
       <div>
         <OtherComponent />
       </div>
     );
   }
   ```

   **Note:**
   `React.lazy` and `Suspense` is not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we still recommend React Loadable.

**[⬆ Back to Top](#table-of-contents)**

3. ### Why does strict mode render twice in React?

   StrictMode renders components twice in development mode(not production) in order to detect any problems with your code and warn you about those problems. This is used to detect accidental side effects in the render phase. If you used `create-react-app` development tool then it automatically enables StrictMode by default.

   ```js
   ReactDOM.render(
     <React.StrictMode>{App}</React.StrictMode>,
     document.getElementById("root")
   );
   ```

   If you want to disable this behavior then you can remove `strict` mode.

   ```js
   ReactDOM.render({ App }, document.getElementById("root"));
   ```

   To detect side effects the following functions are invoked twice:

   1. Class component constructor, render, and shouldComponentUpdate methods
   2. Class component static getDerivedStateFromProps method
   3. Function component bodies
   4. State updater functions
   5. Functions passed to useState, useMemo, or useReducer (any Hook)

**[⬆ Back to Top](#table-of-contents)**

4. ### What is the difference between useState and useRef hook?

   1. useState causes components to re-render after state updates whereas useRef doesn’t cause a component to re-render when the value or state changes.
      Essentially, useRef is like a “box” that can hold a mutable value in its (.current) property.
   2. useState allows us to update the state inside components. While useRef allows referencing DOM elements.

5. ### What is state mutation and how to prevent it?

   `State mutation` happens when you try to update the state of a component without actually using `setState` function. This can happen when you are trying to do some computations using a state variable and unknowingly save the result in the same state variable. This is the main reason why it is advised to return new instances of state variables from the reducers by using Object.assign({}, ...) or spread syntax.

   This can cause unknown issues in the UI as the value of the state variable got updated without telling React to check what all components were being affected from this update and it can cause UI bugs.

   Ex:

   ```javascript
   class A extends React.component {
     constructor(props) {
       super(props);
       this.state = {
         loading: false
       }
    }

   componentDidMount() {
     let { loading } = this.state;
     loading = (() => true)(); // Trying to perform an operation and directly saving in a state variable
   }

   ```

   **How to prevent it:** Make sure your state variables are immutable by either enforcing immutability by using plugins like Immutable.js, always using `setState` to make updates, and returning new instances in reducers when sending updated state values.

**[⬆ Back to Top](#table-of-contents)**

6. ### What is suspense component?

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

7. ### Is Node a single threaded application or multi-threaded?

   Node uses a single threaded model with event looping.

   **[⬆ Back to Top](#table-of-contents)**

8. ### What is Callback Hell?

   The asynchronous function requires callbacks as a return parameter. When multiple asynchronous functions are chained together then callback hell situation comes up.

   **[⬆ Back to Top](#table-of-contents)**

9. ### What is the purpose of setTimeout function?

   Run the application on any port above 1024, then put a reverse proxy like [nginx](http://nginx.org/) in front of it.

**[⬆ Back to Top](#table-of-contents)**
