# Closures and Prototypal Inheritance

## Functions are first class citizens

- Functions can be assigned to variables and properties of objects.

```javascript
const stuff = function() {};
```

- You can pass functions as arguments into a function.

```javascript
function something(fn) {
  fn();
}

something(function() {
  console.log("hi");
}); // => 'hi'
```

- You can return functions as values from other functions.

```javascript
function a() {
  return function b() {
    console.log("bye");
  };
}

a()(); // => 'bye'
```

## Higher Order Functions

Higher order functions are simply functions that can take a function as an argument, or a function that returns another function.
