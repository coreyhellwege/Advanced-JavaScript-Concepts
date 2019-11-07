# Asynchronous JavaScript

Asynchronous programming refers to the occurrence of events independently of the main program flow. It is a means of parallel programming in which a unit of work runs separately from the main application thread and then notifies the calling thread of its completion, failure or progress. An example would be a program making a request to a third-party API over the web and then waiting for it to return some data. Simply put, asynchronous functions are just functions that can be executed later.

In multi-threaded programming languages (like Java or C#) asynchronous code is run on separate threads in parallel with the main program flow. This is not the case with JavaScript. JavaScript is single threaded, meaning all code is executed in a sequence, not in parallel. 

The web browser or NodeJs allows us to use asynchronous code so we can interact with things outside the world of JavaScript. This is handled by using what is called an “asynchronous non-blocking I/O model”. What that means is that while the normal execution of JavaScript is blocking, I/O operations are not. I/O operations can be fetching data over the internet with Ajax requests or over WebSocket connections, querying data from a database such as MongoDB or accessing the filesystem with the NodeJs “fs” module. All these kind of operations are done in parallel to the execution of the main program flow and it is not JavaScript that does these operations; to put it simply, the underlying JS engine does it.

---
<br>

## How Does the Browser Execute Asynchronous Code?

![JavaScript Engine](./Assets/JsEngine.png)

As we know, the JavaScript engine is single-threaded. This means that only one command can be performed at the same time. The design of JavaScript is based on that.

- “Memory Heap” is where functions and variables are allocated.
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


<br>

# Callbacks vs Promises

## Callbacks

For JavaScript to know when an asynchronous operation has a result (a result being either returned data or an error that occurred during the operation), it points to a function that will be executed once that result is ready. This function is what we call a “callback function”. Meanwhile, JavaScript continues its normal execution of code. Registering a middleware in an express web server with “server.use” is an example of a common API that uses callbacks.

Here is an example of fetching data from a URL using a module called “request”:

```javascript
const request = require(‘request’);

request('https://www.example.com', function (error, response, body) {
  if(error){
    // Handle error.
  }
  else {
    // Successful, do something with the result.
  }
});
```

As you can see, `request` takes a function as its last argument. This function is not executed together with the code above. It is saved to be executed later once the underlying I/O operation HTTP request is done. The underlying HTTP request is an asynchronous operation and does not block the execution of the rest of the JavaScript code. The callback function is put on the “event loop" queue until it's ready to be executed with a result from the request.

## Callback hell

Callbacks are a good way to declare what will happen once an I/O operation has a result, but what if you want to use that data in order to make another request? You can only handle the result of the request within the callback function provided. 

In this example the variable “result” will not have a value when printed to the console at the last line:
const request = require(‘request’);
let result;

```javascript
const request = require(‘request’);

let result;

request('http://www.example.com', function (error, response, body) {
    if(error){
        // Handle error.
    }
    else {
        result = body;
    }
});

console.log(result);
```

In this example the variable “result” will not have a value when printed to the console. It will output "undefined" to the console because at the time that line is executed the callback has not yet been called. This is because of the nature of the non-blocking I/O model in JavaScript.

So if we want to do a second request based on the result of the first one, we have to do it inside the callback function of the first request because that is where the result will be available:

```javascript
request('http://www.example.com', function (firstError, firstResponse, firstBody) {
    if(firstError){
        // Handle error.
    }
    else {
        request(`http://www.example.com/${firstBody.someValue}`, function (secondError, secondResponse, secondBody) {
            if(secondError){
                // Handle error.
            }
            else {
                // Use secondBody for something
            }
        });
    }
});
```

When you have a callback inside a callback like this, the code tends to get messy. In some cases you may have a callback in a callback in a callback in a callback, and so on.

One thing to note here is the first argument in every callback function will contain an error if something went wrong, or will be empty if all went well. This pattern is called “error first callbacks” and is very common. It is the standard pattern for callback-based APIs in NodeJs. This means that for every callback declared we need to check if there is an error and that just adds to the mess when dealing with nested callbacks.

This is the anti-pattern that has been aptly named “callback hell”.

---

## Promises

A promise is an object that wraps an asynchronous operation and notifies when it’s done. This sounds exactly like callbacks, but the important differences are in the usage of Promises. Instead of providing a callback, a promise has its own methods which you call to tell the promise what will happen when it is successful or when it fails. The methods a promise provides are `then()` for when a successful result is available and `catch()` for when something went wrong.

A promise may produce a single value sometime in the future, either a resolved value or a reason why it didn't resolve (rejected). A promise may be in one of three possible states: Fulfilled, rejected or pending.

```javascript
// function that returns a promise
someAsyncOperation(someParams)

.then(function(result){
    // Do something with the result
})

.catch(function(error){
    // Handle error
});
```

The true power of promises is revealed when you have several asynchronous operations that depend on the results of each other. "Axios" is a model which is similar to "request", but it uses promises instead of callbacks. 

Using axios, our callback hell example would look like this:

```javascript
const axios = require(‘axios’);


axios.get(‘http://www.example.com')

.then(function (response) { // Reponse being the result of the first request
    // Returns another promise to the next .then() in the chain
    return axios.get(`http://www.example.com/${response.someValue}`);
})

.then(function response { // Reponse being the result of the second request
    // Handle response
})

.catch(function (error) {
    // Handle error.
});
```

Instead of nesting callbacks inside callbacks inside callbacks, you chain `.then()` calls together making it more readable and easier to follow. Every `.then()` should either return a new Promise or just a value or object which will be passed to the next `.then()` in the chain. Another important thing to notice is that even though we are doing two different asynchronous requests we only have one `.catch()` where we handle our errors. That’s because any error that occurs in the Promise chain will stop further execution and an error will end up in the next `.catch()` in the chain.

It is important to remember that promises are still asynchronous operations, so subsequent `.then()` calls are only executed when the request has finished. This means you cannot access any variables passed to or declared in the Promise chain outside the Promise. The same goes for errors thrown in the Promise chain. You must also have at least one `.catch()` at the end of your Promise chain for you to be able to handle errors that occur. If you do not have a `.catch()`, any errors will silently go un-noticed and you will have no idea why your Promise does not behave as expected.

## Creating promises

Callbacks are not interchangeable with Promises. This means that callback-based APIs cannot be used as Promises. The main difference with callback-based APIs is that they do not return a value, they just execute the callback with the result. A Promise-based API, on the other hand, immediately returns a Promise that wraps the asynchronous operation. Then the caller uses the returned Promise object and calls `.then()` and `.catch()` on it to declare what will happen when the operations has finished.

The process of wrapping a callback based asynchronous function inside a Promise and returning that promise instead is called “promisification”. We are “promisifying” a callback-based function. Since NodeJs version 8 there is a built in a helper called “util.promisify” for doing exactly that:

```javascript
const { promisify } = require(‘util’);

const getAsyncData = promisify(getData);

getAsyncData(“someValue”)
.then(function(result){
    // Do stuff
})
.catch(function(error){
    // Handle error
});
```

---

## Async/Await

Async/Await is the next step in the evolution of handling asynchronous operations in JavaScript. It gives you two new keywords to use in your code: `async` and `await`. Async is for declaring that a function will handle asynchronous operations and await is used to declare that we want to await the result of an asynchronous operation inside a function that has the async keyword.

A basic example of using async/await looks like this:

```javascript
async function getSomeAsyncData(value){
    const result = await fetchTheData(someUrl, value);
    return result;
}
```

A function call can only have the `await` keyword if the function being called is “awaitable”. A function is “awaitable” if it has the `async` keyword or if it returns a Promise. Functions with the `async` keyword are interchangeable with functions that return Promises:

```javascript
function fetchTheData(someValue){
    return new Promise(function(resolve, reject){
        getData(someValue, function(error, result){
            if(error) {
                reject(error);
            }
            else {
                resolve(resutl);
            }
        })
    });
}

async function getSomeAsyncData(value){
    const result = await fetchTheData(value);
    return result;
}
```

## Error handling with async/await

Inside the scope of an async function you can use try/catch for error handling and even though you await an asynchronous operation, any errors will end up in that catch block:

```javascript
async function getSomeData(value){
    try {
        const result = await fetchTheData(value);
        return result;
    }
    catch(error){
        // Handle error
    }
}
```

As with a Promise chain, where you only need one `.catch()` even if you are doing several asynchronous calls, with async/await you only need to surround the code in the “first” async function with try catch. That function can await one or more other async functions which in return does their own asynchronous calls by awaiting one or more other async functions etc.

```javascript
async function fetchTheFirstData(value){
    return await get("someUrl", value);
}

async function fetchTheSecondData(value){
    return await getFromDatabase(value);
}

async function getSomeData(value){
    try {
        const firstResult = await fetchTheFirstData(value);
        const result = await fetchTheSecondData(firstResult.someValue);
        return result;
    }
    catch(error){
        // Every error thrown in the whole “awaitable” chain will end up here.
    }
}
```

It is important to remember that although async/await may make your asynchronous calls look more synchronous, it is still executed with asynchronous I/O operations. Therefore the code handling the responses in the async functions will not be executed until that asynchronous operation has a result. 

Also, async/await still resolves as a Promise in the top level of your program, because `async` and `await` are just syntactical sugar for automatically creating, returning and resolving Promises.

[Resource](https://medium.com/codebuddies/getting-to-know-asynchronous-javascript-callbacks-promises-and-async-await-17e0673281ee)

---

<br>
