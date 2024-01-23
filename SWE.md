### Table of Contents

| No. | Questions                                                                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|     | **React**                                                                                                                                                    |
| 1   | [What is Virtual DOM?](#what-is-virtual-dom)                                                                                                                 |
| 2   | [What is React lazy function?](#what-is-react-lazy-function)                                                                                                 |
| 3   | [Why does strict mode render twice in React?](#why-does-strict-mode-render-twice-in-react)                                                                   |
| 4   | [What is the difference between useState and useRef hook?](#what-is-the-difference-between-usestate-and-useref-hook)                                         |
| 5   | [What is state mutation and how to prevent it?](#what-is-state-mutation-and-how-to-prevent-it)                                                               |
| 6   | [What is suspense component?](#what-is-suspense-component)                                                                                                   |
|     | **Node.js**                                                                                                                                                  |
| 7   | [Is Node a single threaded application or multi-threaded?](#is-node-a-single-threaded-application-or-multi-threaded)                                         |
| 8   | [What is Callback Hell?](#what-is-callback-hell)                                                                                                             |
| 9   | [What is the purpose of setTimeout function?](#what-is-the-purpose-of-settimeout-function)                                                                   |
| 10  | [How can you listen on port 80 with Node?](#how-can-you-listen-on-port-80-with-node)                                                                         |
| 11  | [What is an Event Emitter in Node.js?](#what-is-an-event-emitter-in-nodejs)                                                                                  |
|     | **AWS**                                                                                                                                                      |
| 12  | [Brief about S3 service in AWS?](#brief-about-s3-service-in-aws)                                                                                             |
| 13  | [What is CloudFront?](#what-is-cloudfront)                                                                                                                   |
| 14  | [How do you safeguard your EC2 instances running in a VPC?](#how-do-you-safeguard-your-ec2-instances-running-in-a-vpc)                                       |
|     | **GCP**                                                                                                                                                      |
| 15  | [What is the Function of a Bucket in Google Cloud Storage?](#what-is-the-function-of-a-bucket-in-google-cloud-storage)                                       |
| 16  | [What is "Virtual Private Cloud" (VPC) when referring to Google Cloud Platform?](#what-is-virtual-private-cloud-vpc-when-referring-to-google-cloud-platform) |
| 17  | [What does it mean to have "binary authorization" in the Google cloud?](#what-does-it-mean-to-have-binary-authorization-in-the-google-cloud)                 |

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

   The `setTimeout(cb, ms)` global function is used to run callback `cb` after at least `ms` milliseconds. The actual delay depends on external factors like OS timer granularity and system load. A timer cannot span more than 24.8 days.

   **[⬆ Back to Top](#table-of-contents)**

10. ### How can you listen on port 80 with Node?

    Run the application on any port above 1024, then put a reverse proxy like [nginx](http://nginx.org/) in front of it.

    **[⬆ Back to Top](#table-of-contents)**

11. ### What is an Event Emitter in Node.js?

    EventEmitter is a Node.js class that includes all the objects that are basically capable of emitting events. This can be done by attaching named events that are emitted by the object using an eventEmitter.on() function. Thus whenever this object throws an even the attached functions are invoked synchronously.

    ```javascript
    const EventEmitter = require("events");

    class MyEmitter extends EventEmitter {}

    const myEmitter = new MyEmitter();

    myEmitter.on("event", () => {
      console.log("an event occurred!");
    });

    myEmitter.emit("event");
    ```

    **[⬆ Back to Top](#table-of-contents)**

12. ### Brief about S3 service in AWS?

    S3, a Simple Storage Service from Amazon. You can move your files TO and FROM S3. Its like a FTP storage. You can keep your SNAPSHOTS in S3. You can also ENCRYPT your sensitive data in S3.

    **[⬆ Back to Top](#table-of-contents)**

13. ### What is CloudFront?

    Amazon CloudFront is a service that speeds up transfer of your static and dynamic web content such as HTML files, IMAGE files., etc., CloudFront delivers your particulars thru worldwide data centers named Edge Locations.

    **[⬆ Back to Top](#table-of-contents)**

14. ### How do you safeguard your EC2 instances running in a VPC?

    Security Groups can be used to protect your EC2 instances in a VPC. We can configure both INBOUND and OUTBOUND traffic in a Security Group which enables secured access to your EC2 instances. Security Group automatically denies any unauthorized access to your EC2 instances.

    **[⬆ Back to Top](#table-of-contents)**

15. ### What is the Function of a Bucket in Google Cloud Storage?

    "Buckets" are the most straightforward containers that may be used to hold information. Any data that is stored in Cloud Storage must first be organized into a bucket. There is no restriction on the number of buckets that can be added.

    **[⬆ Back to Top](#table-of-contents)**

16. ### What is "Virtual Private Cloud" (VPC) when referring to Google Cloud Platform?

    Through the use of a Virtual Private Cloud, Google Cloud Platform (GCP) virtual machine (VM) instances, Google Kubernetes Engine (GKE) clusters, and other resources will be able to connect with one another. The VPC gives users a great deal of wiggle room in terms of regulating regional and global workload connectivity. Without having to rely on the public internet, virtual private networks (VPCs) make it possible for multiple regions to communicate with one another.

    **[⬆ Back to Top](#table-of-contents)**

17. ### What does it mean to have "binary authorization" in the Google cloud?

    The Binary Authorization is utilized by both Google Kubernetes Engine (GKE) and Cloud Run to verify that only legitimate container images are deployed. This is done to prevent any errors from occurring. Binary Authorization enables us to enforce signature validation during the deployment phase.

    **[⬆ Back to Top](#table-of-contents)**
