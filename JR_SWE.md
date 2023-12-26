| No. | Questions                                                                                                                                                                                                                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     | **React**                                                                                                                                                                                                                   |
| 1   | [What is the difference between Element and Component?](#what-is-the-difference-between-element-and-component)
                                                                                         |
| 2   | [What are Pure Components?](#what-are-pure-components)      

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

2.  ### What are Pure Components?

    Pure components are the components which render the same output for the same state and props. In function components, you can achieve these pure components through memoized `React.memo()` API wrapping around the component. This API prevents unnecessary re-renders by comparing the previous props and new props using shallow comparison. So it will be helpful for performance optimizations. 
    
    But at the same time, it won't compare the previous state with the current state because function component itself prevents the unnecessary rendering by default when you set the same state again.

    The syntactic representation of memoized components looks like below,

    ```jsx
    const MemoizedComponent = memo(SomeComponent, arePropsEqual?);
    ```

    Below is the example of how child component(i.e., EmployeeProfile) prevents re-renders for the same props passed by parent component(i.e.,EmployeeRegForm).

    ```jsx
      import { memo, useState } from 'react';

      const EmployeeProfile = memo(function EmployeeProfile({ name, email }) {
        return (<>
              <p>Name:{name}</p>
              <p>Email: {email}</p>
              </>);
      });
      export default function EmployeeRegForm() {
        const [name, setName] = useState('');
        const [email, setEmail] = useState('');
        return (
          <>
            <label>
              Name: <input value={name} onChange={e => setName(e.target.value)} />
            </label>
            <label>
              Email: <input value={email} onChange={e => setEmail(e.target.value)} />
            </label>
            <hr/>
            <EmployeeProfile name={name}/>
          </>
        );
      }
    ```
    In the above code, the email prop has not been passed to child component. So there won't be any re-renders for email prop change.

    In class components, the components extending _`React.PureComponent`_ instead of  _`React.Component`_ become the pure components. When props or state changes, _PureComponent_ will do a shallow comparison on both props and state by invoking `shouldComponentUpdate()` lifecycle method. 

    **Note:** `React.memo()` is a higher-order component.

    **[⬆ Back to Top](#table-of-contents)**
