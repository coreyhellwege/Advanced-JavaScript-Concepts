# Asynchronous JavaScript

Asynchronous programming is a means of parallel programming in which a unit of work runs separately from the main application thread and then notifies the calling thread of its completion, failure or progress. For example, a program making a request to a third-party API over the web and waiting for it to return some data.

JavaScript is just a single threaded programming language and has no idea what the worldwide web or the internet is. On the other hand the web browser or Node.js allow us to use asynchronous code so we can interact with things outside the world of JavaScript.

So, simply put asynchronous functions are just functions that we can execute later.

---
<br>

## How Does the Browser Execute Asynchronous Code?

![JavaScript Engine](./Assets/JsEngine.png)

As we know, the JavaScript engine is single-threaded. This means that only one command can be performed at the same time. The design of JavaScript is based on that.

- “Memory” is where functions and variables are allocated.
- “Call stack” is used by the JavaScript engine to know what code to execute next. Whatever is on the top of the stack is what is currently being executed.
- The “Event Loop” checks on the job queues and, whenever the call stack is empty, pops the code from them and pushes it onto the call stack to be executed.

The two queues that handle asynchronous code:
- The callback queue.
- The micro-task queue - which is used by promises.

## JavaScript's Execution

There are two parts to the code’s execution process.

### The thread of execution

<i>Also called the first half of the program.</i>

It's the first parsing and executing the code line-by-line, as the code appears. It allocates variables and functions, and the code is executed in an execution context. (This part is executed synchronously)

### Deferred code execution

<i>Also called the second half of the program.</i>

This code is executed at some point in time after we have gone through the normal thread of execution. This happens, for example, if we call `setTimeout`, or wait for API request data to come back from a server. We shouldn't block the JavaScript thread of execution in the time we wait.

### Web APIs

The browser provides some features that contribute to the execution of asynchronous code without blocking the thread. These features are known as web APIs (browser). You might recognize several of them, like the timer, where the `setTimeout` and `setInterval` methods live, the `XMLHttpRequest` which is used by the fetch method, the Console API, the DOM, and the web storage API. 

### Summary

So once our JavaScript engine sees something that is asynchronous it sends it over to the Web API which deals with it in the background. When it's done with whatever it is processing it will add the callback or the function that needs to be invoked to the callback queue. The event loop will then check to see if the call stack is empty, and the entire JavaScript file has been read. If it's empty it then pushes the asynchronous code onto the call stack.

---
<br>