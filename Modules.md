# The Module Pattern

Initially, JavaScript only had two scopes; The global and function scopes.
ES6 later introduced two new keywords `let` and `const` which provided Block Scope in JavaScript. And before then, the module pattern was introduced to allow for Module scope.

[Read More about JS Scope](https://www.w3schools.com/js/js_scope.asp)

The module scope is higher up than the function scope so that multiple functions can be combined together and variables can be shared between different functions without polluting the global namespace.

In this way, with module scope, we can be explicit with which variables, classes or functions should be imported or exported in the module.

An example of this old syntax is an <i>Immediately Invoked Function Expression</i>:

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
