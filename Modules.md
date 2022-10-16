# The Module Pattern

Initially, JavaScript only had two scopes; The global and function scopes.
ES6 later introduced two new keywords `let` and `const` which provided Block Scope in JavaScript. And before then, the module pattern was introduced to allow for Module scope.

[Read More about JS Scope](https://www.w3schools.com/js/js_scope.asp)

The module scope is higher up than the function scope so that multiple functions can be combined together and variables can be shared between different functions without polluting the global namespace.

In this way, with module scope, we can be explicit with which variables, classes or functions should be imported or exported in the module.

An example of this old syntax is an <i>[Immediately Invoked Function Expression](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)</i>:

```javascript
var fightModule = (function() {
    var harry = 'potter';
    var voldemort = 'he who must not be named';

    function fight(char1, char2) {
        var attack1 = Math.floor(Math.random() * char1.length);
        var attack2 = Math.floor(Math.random() * char2.length);
        return attack1 > attack2 ? `${char1} wins` : `${char2} wins`;
    }

    return {
        fight: fight
    }
})()
```

This example uses the Module pattern to assign to the `fightModule` variable whatever is returned from the function which gets immediately invoked. 

In this way, you can access the `fight` function by running `fightModule.fight()`, but the `harry` and `voldemort` variables remain private.

I.e whatever we return from the IIFE is our public API, and everything else is private and does not get exported.

This pattern of returning only the code we need is called the <strong>Revealing module pattern</strong>.

The Module pattern was also used to explicitly declare which code from the global scope is to be imported to the function scope, preventing global variables from otherwise being inadvertantly modified.

```javascript
var globalSecret = '1234';

var something = (function(globalSecret) {
    globalSecret = '0';
})(globalSecret)
```

So here, `globalSecret` still equals `'1234'` but `something.globalSecret` equals `'0'`.

# CommonJS

CommonJS and AMD (asynchronous module definition) solved the problem of designing a module in a way that doesn't have interference of global
scope where variables can be overwritten. 

CommonJS used the require syntax which allowed you to import certain files or modules.

```javascript
let module1 = require('module1'); // import a module
let fight = require('module1').fight; // import a specific function
```
CommonJS was created mainly for the server, with Node.js in mind and it contributed to Node's rise in popularity over time. NPM (Node Package Manager) used CommonJS to make it easy for developers to share their modules with eachother.

In CommonJS, modules are loaded synchronously, and considering JavaScript only has one call stack, each module needs to load one after the other before your script can even run. This is obviously not ideal for the dynamic environment of a web browser, which was why it was mainly used on the server side only.

If only CommonJS could work on the client side without compromising performance..

## Asset bundling to the rescue

Asset bundling services like Browserify and Webpack allow you to require modules in the browser by bundling up all of your dependencies into one JavaScript file. This traverses the dependeny tree of your code so only one reference needs to be made, preventing you from having to worry about handling the loading sequence of multiple dependencies. 

# ES6 Modules

```javascript
import module1 from 'module1'
```

JavaScript needed a way to natively support modules in all environments not just the browser, e.g. server, mobile, desktop, iOT devices.

### Named export

```javascript
export const jump = () => {}
export const attack = () => {}

import { jump, attack } from 'module2'
```

### Default export

```javascript
export default const kick = () => {}

import kick from 'module2'
```

# Conclusion

Initially, JavaScript started with simple script tags, but as our programs and web pages got more complex over time, we started to see problems.

We needed a way to have modules, so we used Immediately Invoked Function Expressions to create the module pattern. But over time, this system still needed to be improved.

So libraries like CommonJS and AMD came into play to make our code more reusable and modular, and also allowed us to share our code with other programmers.

Then finally we got native ES6 modules, where JavaScript as a language now has modules built in.

This gives us the ability to separate concerns and divide up our programs into small chunks that work independently.

We avoid global namespace pollution by only exporting specific code, not necessarily the whole file.

We can now compose different modules together to add different functionality to our programs.

We can use third party code from places like NPM.

We now have a way to organize our codebase better, allowing us to build large applications with JavaScript.