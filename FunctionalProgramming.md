# Functional Programming

Functional programming (often abbreviated FP) is the process of building software by composing pure functions, avoiding shared state, mutable data, and side-effects. Functional programming is declarative rather than imperative, and application state flows through pure functions. Contrast with object oriented programming, where application state is usually shared with methods in objects.

<i>[Reference Article](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)</i>

## Pure Functions

![Pure Functions](./Assets/PureFunctions.png)

If you want to break things down in functional programming it all comes down to this concept of pure functions. The idea is that there's a separation between data over a program and the behavior of a program. All objects created in functional programming are immutable, so after it has been created it cannot be changed.

Rules:

- The function has to always return the same output, given the same input
- The function cannot modify anything outside of itself
- No side effects

<i>Example:</i>

```javascript
const array = [1,2,3] // in the outside world (don't modify)

function removeLastItem(arr) {
    const newArray = [].concat(arr); // make a copy of the input instead of directly modifying it
    newArray.pop()
    return newArray
}

function multiplyByTwo(arr) {
    return arr.map(item => item * 2) // using .map() will return a new array
}

const array2 = removeLastItem(array);
const array3 = multiplyByTwo(array);

console.log(array, array2, array3) // ->  [1, 2, 3] , [1, 2] , [2, 4, 6]
```

---
<br>

![Perfect Function](./Assets/PerfectFunction.png)

#### The perfect function should:

- Do one task and one task only
- Have a return statement. If we give it an input we expect an output
- Be pure (see above rules)
- Have no shared state with other functions
- Have immutable state. Never modify global state, always return a new copy of an input
- Be composable
- Be predictable

---
<br>

## Idempotence

The idea of Idempotence is a function that always returns or does what we expect it to do.

<i>Example:</i>

```javascript
function notGood(num) {
    console.log(num)
}

notGood(5) // -> 5
```

This function is idempotent because it returns the same result when called multiple times. It is not pure however as it interacts with the global scope. Practical examples of idempotent functions can be HTTP requests to an API such as deleting a user. Idempotence is useful because it helps keep code predictable.

---
<br>

## Imperative Vs. Declarative

<b>Imperative</b> code is code that tells the machine what to do and how to do it. <b>Declarative</b> code tells it what to do and what should happen.

A useful analogy to think of is that computers are better at being imperative and humans are better at being declarative. 

![Imperative Vs. Declarative](./Assets/ImperativeDeclarative.png)

Machine code is imperative. When we declare a variable the computer receives specific instructions related to where it should be stored in memory space, when to modify it and so on. Its very descriptive about how to do things. In contrast, as we go higher up the chain to higher level languages it becomes more declarative. Instead of giving specific instructions, we just declare the variable with some sort of data and tell it what we need to achieve but not how to do it. The computer takes care of that for us.

<i>JQuery is an example of a fairy imperative language, and the React framework operates in a fairly declarative fashion.</i>

<i>Example:</i>

`for` loops can be considered an imperative style of writing code

```javascript
for (let i = 0; i < 1000; i++) {
    console.log(i) // -> 1,2,3,4...1000
}
```

One way of making a `for` loop more declarative is to use `forEach()` instead

```javascript
[1,2,3].forEach(item => console.log(item)) // -> 1,2,3
```
<br>

### <i>Functional programming teaches us be more declarative.</i>
---
<br>

## Immutability

In functional programming, immutability relates to not changing data or state but instead making copies of it and returning a new state every time. 

Doesn't that just fill up our memory? That's where structural sharing comes in.

### Structural Sharing

![Structural Sharing](./Assets/StructuralSharing.png)

When a new copy of a datatype (object, array etc) is created instead of copying everything only the changes made to the state are copied. This saves memory. 

---
<br>

## Higher Order Functions

A higher order function is a function that does one of two things. It either (1) takes one or more functions as arguments, or (2) returns a function as a result, often called a callback.

<i>Example 1:</i>

```javascript
const hof = () => () => 'hello';

hof() // -> Function () => 'hello'

hof()() // -> hello
```

<i>Example 2:</i>

```javascript
const hof = (fn) => fn('hello');

hof(function(x){ console.log(x) }) // -> hello
```

---
<br>

## Currying

Currying is when you break down a function that takes multiple arguments into a series of functions that each take only one argument.

<i>Example</i>

```javascript
const multiply = (a,b) => a * b;
```

Instead of this function taking two parameters, we're going to give the first function one parameter which returns another function, and that function will take another parameter which will multiply `a` with `b`. Because of closures we can access the `a` variable inside of the `b` function. 

```javascript
const curriedMultiply = (a) => (b) => a * b;

curriedMultiply(5)(4); // -> 20
```

### Why is this useful?

You can now create additional utility functions ontop of this function. So you can see that in this example we're essentially saving the first function with a set argument passed into the parameter to a new variable. Then when we can use that variable as a new function which only takes an input for the second function. 

```javascript
const curriedMultiplyBy5 = curriedMultiply(5);

curriedMultiplyBy5(6) // -> 30
curriedMultiplyBy5(10) // -> 50
```



