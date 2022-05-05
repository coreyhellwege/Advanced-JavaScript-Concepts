<div id="top"></div>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]

<br />

<div align="center">
  <a href="https://github.com/coreyhellwege/Advanced-JavaScript-Concepts">
    <img src="./images/javascript.png" alt="Logo" width="80" height="80">
  </a>

<h1 align="center">JavaScript: The Advanced Concepts</h1>

  <p align="center">
    Research to gain a deeper understanding of how JavaScript works under the hood.
    <br />
    <br />
    <a href="https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/issues">Report Bug</a>
    ·
    <a href="https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/issues">Request Feature</a>
  </p>
</div>

<br />

<!-- TABLE OF CONTENTS -->
<details open>
    <summary>Table of Contents</summary>
    <ol>
        <li>
            <h3><a href="/Foundations.md">JavaScript Foundations</a></h3>
            <ul>
                <li><a href="/Foundations.md/#javascript-engine">JS Engine</a></li>
                <li><a href="/Foundations.md/#interpreter">Interpreter</a></li>
                <li><a href="/Foundations.md/#compiler">Compiler</a></li>
                <li><a href="/Foundations.md/#ecmascript">ECMAScript</a></li>
                <li><a href="/Foundations.md/#writing-optimised-code">Writing optimised code</a></li>
                <li><a href="/Foundations.md/#inline-caching">Inline Caching</a></li>
                <li><a href="/Foundations.md/#hidden-classes">Hidden Classes</a></li>
                <li><a href="/Foundations.md/#call-stack">Call Stack</a></li>
                <li><a href="/Foundations.md/#memory-heap">Memory Heap</a></li>
                <ul>
                    <li>Garbage Collection</li>
                    <li>Memory Leaks</li>
                </ul>
                <li><a href="/Foundations.md/#javascript-runtime">JavaScript Runtime</a></li>
                <ul>
                    <li>Web Browser API</li>
                    <li>The Heap</li>
                    <li>The Stack</li>
                    <li>The Web API Container</li>
                    <li>The Callback Queue</li>
                    <li>The Event Loop</li>
                </ul>
                <li><a href="/Foundations.md/#node.js">Node.js</a></li>
                <li><a href="/Foundations.md/#lexical-environment">Lexical Environment</a></li>
                <li><a href="/Foundations.md/#scope">Scope</a></li>
                <li><a href="/Foundations.md/#execution-context">Execution Context</a></li>
                <ul>
                    <li>Global Execution Context</li>
                    <li>Functional execution context</li>
                </ul>
                <li><a href="/Foundations.md/#hoisting">Hoisting</a></li>
                <li><a href="/Foundations.md/#scope-chain">Scope Chain</a></li>
                <li><a href="/Foundations.md/#this">This</a></li>
                <li><a href="/Foundations.md/#function-currying">Function Currying</a></li>
                <li><a href="/Foundations.md/#context-vs-scope">Context vs Scope</a></li>
            </ul>
        </li>
        <li>
            <h3><a href="/Types.md">Types</a></h3>
            <ul>
                <li><a href="/Types.md/#primitive-types">Primitive Types</a></li>
                <ul>
                    <li>Number</li>
                    <li>String</li>
                    <li>Boolean</li>
                    <li>Null</li>
                    <li>Undefined</li>
                    <li>Symbol</li>
                </ul>
                <li><a href="/Types.md/#non-primitive-types">Non Primitive Types</a></li>
                <ul>
                    <li>Object</li>
                </ul>
                <li><a href="/Types.md/#pass-by-value">Pass By Value (primitives)</a></li>
                <li><a href="/Types.md/#pass-by-reference">Pass by Reference (objects)</a></li>
                <li><a href="/Types.md/#type-coercion">Type Coercion</a></li>
            </ul>
        </li>
        <li>
            <h3><a href="/ClosuresPrototypalInheritance.md">Closures and Prototypal Inheritance</a></h3>
            <ul>
                <li><a href="/ClosuresPrototypalInheritance.md/#higher-order-functions">Higher Order Functions</a></li>
                <li><a href="/ClosuresPrototypalInheritance.md/#closures">Closures</a></li>
                <ul>
                    <li>Memory efficiency</li>
                    <li>Encapsulation</li>
                </ul>
                <li><a href="/ClosuresPrototypalInheritance.md/#prototypal-inheritance">Prototypal Inheritance</a></li>
                <ul>
                    <li>Manually creating a prototype chain</li>
                    <li>Inheritance using Object.create()</li>
                    <li>Only functions have the .prototype property</li>
                </ul>
            </ul>
        </li>
        <li>
            <h3><a href="/ObjectOrientedProgramming.md">Object Oriented Programming</a></h3>
            <ul>
                <li><a href="/ObjectOrientedProgramming.md/#class-based-vs-prototype-based">Class-based vs Prototype-based</a></li>
                <li><a href="/ObjectOrientedProgramming.md/#factory-functions">Factory Functions</a></li>
                <ul>
                    <li>Using Object.create()</li>
                    <li>Using Constructor Functions</li>
                    <li>Using ES6 Classes</li>
                </ul>
                <li><a href="/ObjectOrientedProgramming.md/#more-of-this">More of 'This'</a></li>
                <ul>
                    <li>Implicit Binding</li>
                    <li>Explicit Binding</li>
                    <li>New Binding</li>
                    <li>Lexical Binding</li>
                    <li>Window Binding</li>
                </ul>
                <li><a href="/ObjectOrientedProgramming.md/#inheritance">Inheritance</a></li>
                <li><a href="/ObjectOrientedProgramming.md/#public-&-private">Public & Private - Protected properties and methods</a></li>
                <ul>
                    <li>Internal and external interface</li>
                    <li>Protected properties</li>
                    <li>Read-only properties</li>
                    <li>Private properties</li>
                </ul>
                <li><a href="/ObjectOrientedProgramming.md/#the-four-pillars-of-oop">The Four Pillars of OOP</a></li>
                <ul>
                    <li>1. Encapsulation</li>
                    <li>2. Abstraction</li>
                    <li>3. Inheritance</li>
                    <li>4. Polymorphism</li>
                </ul>
            </ul>
        </li>
        <li>
            <h3><a href="/FunctionalProgramming.md">Functional Programming</a></h3>
            <ul>
                <li><a href="/FunctionalProgramming.md/#pure-functions">Pure Functions</a></li>
                <li><a href="/FunctionalProgramming.md/#idempotence">Idempotence</a></li>
                <li><a href="/FunctionalProgramming.md/#imperative-vs-declarative">Imperative vs Declarative</a></li>
                <li><a href="/FunctionalProgramming.md/#immutability">Immutability</a></li>
                <li><a href="/FunctionalProgramming.md/#higher-order-functions">Higher Order Functions</a></li>
                <li><a href="/FunctionalProgramming.md/#currying">Currying</a></li>
                <li><a href="/FunctionalProgramming.md/#partial-application">Partial Application</a></li>
            </ul>
        </li>
        <li>
            <h3><a href="/OOPvsFP.md">Object Oriented Programming vs Functional Programming</a></h3>
            <ul>
                <li><a href="/OOPvsFP.md/#key-differences">Key Differences</a></li>
                <li><a href="/OOPvsFP.md/#inheritance-vs-composition">Inheritance vs Composition</a></li>
            </ul>
        </li>
        <li>
            <h3><a href="/AsyncJS.md">Asynchronous JavaScript</a></h3>
            <ul>
                <li><a href="/AsyncJS.md/#how-does-the-browser-execute-asynchronous-code?">How Does the Browser Execute Asynchronous Code?</a></li>
                <li><a href="/AsyncJS.md/#javascript's-execution">JavaScript's Execution</a></li>
                <ul>
                    <li>The thread of execution</li>
                    <li>Deferred code execution</li>
                    <li>Web APIs</li>
                </ul>
                <li><a href="/AsyncJS.md/#callbacks">Callbacks</a></li>
                <ul>
                    <li>Callback hell</li>
                </ul>
                <li><a href="/AsyncJS.md/#promises">Promises</a></li>
                <li><a href="/AsyncJS.md/#async/await">Async/Await</a></li>
                <li><a href="/AsyncJS.md/#es9">ES9</a></li>
                <ul>
                    <li>Array Destructuring</li>
                    <li>Array Literals</li>
                    <li>Object Destructuring</li>
                    <li>Object Literals</li>
                    <li>Finally</li>
                    <li>For await of</li>
                    <li>Job Queue</li>
                    <li>Parallel, Sequence, Race</li>
                    <li>Threads</li>
                    <li>Concurrency and Parallelism</li>
                </ul>
            </ul>
        </li>
        <li>
            <h3><a href="/Modules.md">The Module Pattern</a></h3>
        </li>
    </ol>
</details>

<br />

<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Andrei Neagoie](https://www.udemy.com/course/advanced-javascript-concepts/)

<p align="right"><a href="#top">back to top</a></p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/coreyhellwege/Advanced-JavaScript-Concepts.svg?style=for-the-badge
[contributors-url]: https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/coreyhellwege/Advanced-JavaScript-Concepts.svg?style=for-the-badge
[forks-url]: https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/network/members
[stars-shield]: https://img.shields.io/github/stars/coreyhellwege/Advanced-JavaScript-Concepts.svg?style=for-the-badge
[stars-url]: https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/stargazers
[issues-shield]: https://img.shields.io/github/issues/coreyhellwege/Advanced-JavaScript-Concepts.svg?style=for-the-badge
[issues-url]: https://github.com/coreyhellwege/Advanced-JavaScript-Concepts/issues
[license-shield]: https://img.shields.io/github/license/coreyhellwege/Advanced-JavaScript-Concepts.svg?style=for-the-badge