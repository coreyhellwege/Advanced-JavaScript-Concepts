# Errors in JavaScript

In JavaScript we have a native error constructor function, `Error`

Create an `Error` instance and pass it a message:

```JavaScript
new Error('oops')
```

This error logs a message but doesn't do anything else, so it's not really an error.

## Throw

In JavaScript, the `throw` syntax is used to define errors. 

```JavaScript
throw new Error() // -> Uncaught error at line ..
```

In JavaScript we can actually `throw` anything..

```JavaScript
throw 'hello' // -> Uncaught hello
throw true // -> Uncaught true
```

During runtime, when a throw statement is encountered the execution of the current function will stop and control will be passed to the next part of the call stack.

```JavaScript
throw new Error()
1 + 1 // This will not run
```

## Error properties

An instance of the `Error` constructor function has three built-in properties for us to use.

```JavaScript
const myError = new Error('oops')
myError.name // -> 'Error'
myError.message // -> 'oops'
myError.stack // -> 'Error: oops\n at <anonymous>:1:17'
```

The `.stack` property reveals the error's stack trace, which is just a string that shows where the error took place. 

## Types of errors

```JavaScript
new SyntaxError // syntactically invalid code
new ReferenceError // when a variable that doesn't exist (or hasn't yet been initialized) in the current scope is referenced
new TypeError // when a variable or parameter is not of a valid type
```

## Error handling

As soon as an error occurs on the call stack the execution context checks if there's a `catch` to handle the error. 

### Runtime catch

If there's no `catch` to handle the error in the call stack, the browser will run the `onerror` function within it's built-in runtime catch. This displays the error message in a red banner in the UI. And in node.js, `process.on('uncaughtException')` runs.

### Try/Catch

Obviously our programs need to be able to handle errors and continue running. Ony way to do so is using try/catch blocks.

The parameter provided to the `catch` block is whatever gets thrown from the `try` block as an `Error` object.

```JavaScript
function fail () {
    try {
        // Run some code.
        console.log('This runs.')
        throw new Error('whoops')
        console.log('This wont run.')
    } catch (error) {
        // Handle any errors encountered.
        console.log(error) // -> Error: whoops at fail (<anonymous>:5:15)
    } finally {
        console.log('No matter what happened above, this will run.')
    }
}
```

#### Try/Catch runs synchronously

```JavaScript
function fail () {
    try {
        setTimeout(function() {
            sfhdkn
        }, 1000)
    } catch (error) {
        console.log('I wont run', error)
    }
}
```

The `catch` block in the above example will never run because the code in the `try` block is asynchronous. The `setTimeout()` function will exit the current callstack and go to the Web API, callback queue and event loop before being pushed onto the stack after the original synchronous code has already finished executing.

## Async error handling

Let's use the shorthand syntax to mock a promise.

### Promise error handling

```JavaScript
Promise.resolve('asyncfail')
    .then(response => {
        console.log(response) // -> asyncfail
        return response
    })
    .then(response => {
        console.log(response) // -> asyncfail
    })
```

If we write a promise without adding a `catch` block, we run the risk of encountering silent failures.

```JavaScript
Promise.resolve('asyncfail')
    .then(response => {
        throw new Error('fail')
        return response
    })
    .then(response => {
        console.log(response)
    })
```

Depending on the runtime, this code will be handled differently. When executed in a browser it will fail silently and nothing will be logged to the console. In node.js you will receive an 'Unhandled promise rejection warning'.

Therefore it's important to always add `catch` blocks to your promises.

```JavaScript
Promise.resolve('asyncfail')
    .then(response => {
        throw new Error('fail')
        return response
    })
    .catch(error => {
        console.log(error) // -> Error: fail at <anonymous>:3:15
    })
```

### Async/await error handling

Let's start off by creating an immediately invoked function expression.
When using async/await, we can also use try/catch blocks to handle asynchronous exceptions, in the same we would handle synchronous code.

```JavaScript
(async function () {
    try {
        await Promise.reject('whoops')
    } catch(error) {
        console.log(error)
    }
    console.log('I will run second')
})()

// -> whoops
// -> I will run second
```

If we fail to provide a try/catch block when using async/await, we will have a similar experience to the previous Promise example. 

```JavaScript
(async function () {
    await Promise.reject('whoops')
    console.log('Will I run?')
})()
```

When executed in a browser, this will fail silently and nothing will be logged to the console. But in node.js you will receive an 'Unhandled promise rejection warning'.

## Extending errors

In JavaScript, the `Error` constructor is an object which we can extend from. So using object oriented programming we can create our own custom error objects which inherit the `Error` object properties and add to it or change it.

```JavaScript
    class AuthenticationError extends Error {
        constructor(message)
        super(message)
        this.name = 'Authentication Error'
        this.errorCode = 401
    }

    class DatabaseError extends Error {
        constructor(message)
        super(message)
        this.name = 'Database Error'
        this.errorCode = 500
    }

    const err = new AuthenticationError('Access denied')

    err.message // -> Access denied
    err.errorCode // -> 401
    err instanceof AuthenticationError // -> true
```