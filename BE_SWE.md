### Table of Contents

| No. | Questions                                                                                                                          |
| --- | ---------------------------------------------------------------------------------------------------------------------------------- |
|     | **Python**                                                                                                                         |
| 1   | [Explain the difference between a mutable and immutable object?](#explain-the-difference-between-a-mutable-and-immutable-object)   |
| 2   | [What is a lambda function, and where would you use it?](#what-is-a-lambda-function,-and-where-would-you-use-it)                   |
| 3   | [How do you copy an object in Python?](#how-do-you-copy-an-object-in-python)                                                       |
| 4   | [What is PYTHONPATH in Python?](#what-is-pythonpath-in-python)                                                                     |
| 5   | [Explain how to delete a file in Python?](#explain-how-to-delete-a-file-in-python)                                                 |
|     | **Golang**                                                                                                                         |
| 6   | [What are goroutines, and how are they different from threads?](#what-are-goroutines-and-how-are-they-different-from-threads)      |
| 7   | [What is the purpose of the `go mod` command?](#what-is-the-purpose-of-the-go-mod-command)                                         |
| 8   | [Explain defer, panic, and recover in Go?](#how-do-you-copy-an-object-in-python)                                                   |
|     | **Java**                                                                                                                           |
| 9   | [What is a Thread?](#what-is-a-thread)                                                                                             |
| 10  | [Difference between HashSet and TreeSet?](#difference-between-hashset-and-treeset)                                                 |
| 11  | [What is the life-cycle of a servlet?](#what-is-the-life-cycle-of-a-servlet)                                                       |
|     | **Node.js**                                                                                                                        |
| 12  | [Is Node a single threaded application or multi-threaded?](#is-node-a-single-threaded-application-or-multi-threaded)               |
| 13  | [What is Callback Hell?](#what-is-callback-hell)                                                                                   |
| 14  | [What are streams in Node.js and what types are available?](#what-are-streams-in-nodejs-and-what-types-are-available)              |
| 15  | [How can you listen on port 80 with Node?](#how-can-you-listen-on-port-80-with-node)                                               |
| 16  | [What is an Event Emitter in Node.js?](#what-is-an-event-emitter-in-nodejs)                                                        |
|     | **AWS**                                                                                                                            |
| 17  | [Brief about S3 service in AWS?](#brief-about-s3-service-in-aws)                                                                   |
| 18  | [What is CloudFront?](#what-is-cloudfront)                                                                                         |
| 19  | [How do you safeguard your EC2 instances running in a VPC?](#how-do-you-safeguard-your-ec2-instances-running-in-a-vpc)             |
| 20  | [List the two native AWS security logging capabilities?](#list-the-two-native-aws-security-logging-capabilities)                   |
| 21  | [List the tools to minimize DDoS attacks on your AWS services?](#list-the-tools-to-minimize-ddos-attacks-on-your-aws-services)     |
| 22  | [What is the use of AWS WAF in monitoring your AWS applications?](#what-is-the-use-of-aws-waf-in-monitoring-your-aws-applications) |

1. ### Explain the difference between a mutable and immutable object?

   ### Key Distinctions

   - **Mutable Objects**: Can be modified after creation.
   - **Immutable Objects**: Cannot be modified after creation.

   ### Common Examples

   - **Mutable**: Lists, Sets, Dictionaries
   - **Immutable**: Tuples, Strings, Numbers

   **[⬆ Back to Top](#table-of-contents)**

2. ### What is a lambda function, and where would you use it?

   A **Lambda function**, or **lambda**, for short, is a small anonymous function defined using the `lambda` keyword in Python.

   While you can certainly use named functions when you need a function for something in Python, there are places where a lambda expression is more suitable.

   #### Distinctive Features

   - **Anonymity**: Lambdas are not given a name in the traditional sense, making them suited for one-off uses in your codebase.
   - **Single Expression Body**: Their body is limited to a single expression. This can be an advantage for brevity but a restriction for larger, more complex functions.
   - **Implicit Return**: There's no need for an explicit `return` statement.
   - **Conciseness**: Lambdas streamline the definition of straightforward functions.

   #### Common Use Cases

   - **Map, Filter, and Reduce**: Functions like `map` can take a lambda as a parameter, allowing you to define simple transformations on the fly. For example, doubling each element of a list can be achieved with `list(map(lambda x: x*2, my_list))`.
   - **List Comprehensions**: They are a more Pythonic way of running the same `map` or `filter` operations, often seen as an alternative to lambdas and `map`.
   - **Sorting**: Lambdas can serve as a custom key function, offering flexibility in sort orders.
   - **Callbacks**: Often used in events where a function is needed to be executed when an action occurs (e.g., button click).
   - **Simple Functions**: For functions that are so basic that giving them a name, especially in more procedural code, would be overkill.

   #### Notable Limitations

   - **Lack of Verbose Readability**: Named functions are generally preferred when their intended use is obvious from the name. Lambdas can make code harder to understand if they're complex or not used in a recognizable pattern.
   - **No Formal Documentation**: While the function's purpose should be apparent from its content, a named function makes it easier to provide direct documentation. Lambdas would need a separate verbal explanation, typically in the code or comments.

   **[⬆ Back to Top](#table-of-contents)**

3. ### How do you copy an object in Python?

   In Python, the assignment statement (= operator) does not copy objects. Instead, it creates a binding between the existing object and the target variable name. To create copies of an object in Python, we need to use the copy module. Moreover, there are two ways of creating copies for the given object using the copy module -

   Shallow Copy is a bit-wise copy of an object. The copied object created has an exact copy of the values in the original object. If either of the values is a reference to other objects, just the reference addresses for the same are copied.
   Deep Copy copies all values recursively from source to target object, i.e. it even duplicates the objects referenced by the source object.

   ```python
    from copy import copy, deepcopy

    list_1 = [1, 2, [3, 5], 4]

    ## shallow copy
    list_2 = copy(list_1)
    list_2[3] = 7
    list_2[2].append(6)
    list_2    # output => [1, 2, [3, 5, 6], 7]
    list_1    # output => [1, 2, [3, 5, 6], 4]

    ## deep copy
    list_3 = deepcopy(list_1)
    list_3[3] = 8
    list_3[2].append(7)
    list_3    # output => [1, 2, [3, 5, 6, 7], 8]
    list_1    # output => [1, 2, [3, 5, 6], 4
   ```

   **[⬆ Back to Top](#table-of-contents)**

4. ### What is PYTHONPATH in Python?

   PYTHONPATH is an environment variable which you can set to add additional directories where Python will look for modules and packages. This is especially useful in maintaining Python libraries that you do not wish to install in the global default location.

   **[⬆ Back to Top](#table-of-contents)**

5. ### Explain how to delete a file in Python?

   Use command os.remove(file_name)

   **[⬆ Back to Top](#table-of-contents)**

6. ### What are goroutines, and how are they different from threads?

   Goroutines are lightweight threads managed by the Go runtime. They are designed for concurrency and allow functions to be executed concurrently with other functions. Goroutines are more lightweight than traditional threads because they are multiplexed onto a smaller number of OS threads. They have a smaller stack size and are managed more efficiently by the Go runtime.

   **[⬆ Back to Top](#table-of-contents)**

7. ### What is the purpose of the `go mod` command?

   The `go mod` command is used to initialize, maintain, and build modules. It allows developers to specify dependencies and their versions, enabling reproducible builds and better dependency management.

   **[⬆ Back to Top](#table-of-contents)**

8. ### Explain defer, panic, and recover in Go.

   - `defer` is a keyword used to schedule a function call to be executed after the surrounding function returns.
   - `panic` is a built-in function that stops the ordinary flow of control and begins panicking.
   - `recover` is a built-in function used to regain control of a panicking goroutine and can only be called within the deferred function.

   **[⬆ Back to Top](#table-of-contents)**

9. ### What is a Thread?

   In Java, the flow of an execution is called Thread. Every java program has at least one thread called main thread, the Main thread is created by JVM. The user can define their own threads by extending Thread class (or) by implementing Runnable interface. Threads are executed concurrently.

   Example:

   ```java
   public static void main(String[] args){//main thread starts here

   }
   ```

   **[⬆ Back to Top](#table-of-contents)**

10. ### Difference between HashSet and TreeSet?

    | HashSet                               | TreeSet                                    |
    | ------------------------------------- | ------------------------------------------ |
    | Inserted elements are in random order | Maintains the elements in the sorted order |
    | Can store null objects                | Couldn’t store null objects                |
    | Performance is fast                   | Performance is slow                        |

    **[⬆ Back to Top](#table-of-contents)**

11. ### What is the life-cycle of a servlet?

    There are 5 stages in the lifecycle of a servlet:

    1. Servlet is loaded
    2. Servlet is instantiated
    3. Servlet is initialized
    4. Service the request
    5. Servlet is destroyed

    ![image](https://user-images.githubusercontent.com/649439/167629455-326556a3-d24c-4c28-88de-c16a40b946de.png)

    **[⬆ Back to Top](#table-of-contents)**

12. ### Is Node a single threaded application or multi-threaded?

    Node uses a single threaded model with event looping.

    **[⬆ Back to Top](#table-of-contents)**

13. ### What is Callback Hell?

    The asynchronous function requires callbacks as a return parameter. When multiple asynchronous functions are chained together then callback hell situation comes up.

    **[⬆ Back to Top](#table-of-contents)**

14. ### What are streams in Node.js and what types are available?

    **Node.js** utilizes **streams** for efficient handling of input/output data, offering two main varieties: readable and writable.

    ### Categories of Streams

    1. **Standard Streams**: Represent standard input, output, and error. These are instances of Readable or Writable streams.

    2. **Duplex Streams**: Facilitate both reading and writing. They can be connected to processes or handling pipelines.

    3. **Transform Streams**: A special type that acts as an intermediary, modifying the data as it passes through.

    ### Practical Implementations

    - **HTTP Transactions**: HTTP clients use readable and writable streams for sending requests and receiving responses. HTTP servers also apply these streams for similar actions in the opposite direction.

    - **File System**: Reading and writing files in Node.js utilizes these streams. For instance, the `fs.createReadStream()` method generates a readable stream whereas `fs.createWriteStream()` creates a writable one.

    **[⬆ Back to Top](#table-of-contents)**

15. ### How can you listen on port 80 with Node?

    Run the application on any port above 1024, then put a reverse proxy like [nginx](http://nginx.org/) in front of it.

    **[⬆ Back to Top](#table-of-contents)**

16. ### What is an Event Emitter in Node.js?

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

17. ### Brief about S3 service in AWS?

    S3, a Simple Storage Service from Amazon. You can move your files TO and FROM S3. Its like a FTP storage. You can keep your SNAPSHOTS in S3. You can also ENCRYPT your sensitive data in S3.

    **[⬆ Back to Top](#table-of-contents)**

18. ### What is CloudFront?

    Amazon CloudFront is a service that speeds up transfer of your static and dynamic web content such as HTML files, IMAGE files., etc., CloudFront delivers your particulars thru worldwide data centers named Edge Locations.

    **[⬆ Back to Top](#table-of-contents)**

19. ### How do you safeguard your EC2 instances running in a VPC?

    Security Groups can be used to protect your EC2 instances in a VPC. We can configure both INBOUND and OUTBOUND traffic in a Security Group which enables secured access to your EC2 instances. Security Group automatically denies any unauthorized access to your EC2 instances.

    **[⬆ Back to Top](#table-of-contents)**

20. ### List the two native AWS security logging capabilities?

    Two popular AWS services that provide security log data to provide insight into how the service is operating are:

    1. AWS CloudTrail
    2. AWS Config

    Besides this, AWS Security Hub and AWS GuardDuty can also be used for insights into your security.

    **[⬆ Back to Top](#table-of-contents)**

21. ### List the tools to minimize DDoS attacks on your AWS services?

    The following tools can be used to minimize DDoS attacks on AWS services:

    - AWS Shield
    - AWS Waf
    - Amazon CloudFront
    - ELB
    - Virtual Private Cloud (VPC)

    **[⬆ Back to Top](#table-of-contents)**

22. ### What is the use of AWS WAF in monitoring your AWS applications?

    AWS Web Application Firewall protects your web applications from any web exploitations and bots that can affect availability, security and consume excessive resources. It filters web traffic and prevents account takeover fraud. It creates and maintains rules by itself and incorporates them into the design and development process.

    **[⬆ Back to Top](#table-of-contents)**
