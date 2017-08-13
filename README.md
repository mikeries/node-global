# Node Global Object

## Overview

This lesson will cover the global object, its properties, differences between browser JavaScript and Node when it comes to globals and scoping.

## Objectives

1. Describe the global object
2. Describe the global object properties: process, global API, etc.
3. Describe the global scoping

## Intro

Node is JavaScript, right? Not exactly. While both Node and browser JavaScript are implementations of ECMAScript, they differ just as different flavors of browser JavaScript implementation can differ. For example, there might be some methods and functions in Internet Explorer or Firefox which are lacking in Safari or vice versa.

So the bottom line is that while most of the browser JavaScript implementations and Node are similar, for example, `console.log()`, `setTimeout()`, Array and String functions, they differ drastically when it comes to global methods and properties (a.k.a. interfaces). There's no `window` in Node!

## Global Object

Why and what exactly is the difference? You see, in browsers we don't have the ability to import modules or work with a file system (we're primarily talking about ES5). We are also limited in what information we can get from the environment. The server or Node code can do much more than the browser, so we need to introduce some global interfaces. They live on the `global` object. So you can print them with this statement:

```js
console.log(global)
```

Or you can type `global` in Node REPL. The output would be similar to this:

```
> global
{ DTRACE_NET_SERVER_CONNECTION: [Function],
  ...
  global: [Circular],
  process: {...},
  GLOBAL: [Circular],
  root: [Circular],
  Buffer:
   { [Function: Buffer]
     poolSize: 8192,
     isBuffer: [Function: isBuffer],
     compare: [Function: compare],
     isEncoding: [Function],
     concat: [Function],
     byteLength: [Function: byteLength] },
  clearImmediate: [Function],
  clearInterval: [Function],
  clearTimeout: [Function],
  setImmediate: [Function],
  setInterval: [Function],
  setTimeout: [Function],
  console: [Getter],
  module:
   Module {
     id: 'repl',
     exports:
      { writer: [Object],
        _builtinLibs: [Object],
        REPLServer: [Object],
        REPL_MODE_SLOPPY: Symbol(repl-sloppy),
        REPL_MODE_STRICT: Symbol(repl-strict),
        REPL_MODE_MAGIC: Symbol(repl-magic),
        start: [Function],
        repl: [Object] },
     parent: undefined,
     filename: '/Users/azat/Documents/Code/learn-co/node-debugger/repl',
     loaded: false,
     children: [],
     paths:
      [ '/Users/azat/Documents/Code/learn-co/node-debugger/repl/node_modules',
        '/Users/azat/Documents/Code/learn-co/node-debugger/node_modules',
        '/Users/azat/Documents/Code/learn-co/node_modules',
        '/Users/azat/Documents/Code/node_modules',
        '/Users/azat/Documents/node_modules',
        '/Users/azat/node_modules',
        '/Users/node_modules',
        '/node_modules' ] },
  require: {...}
```

Let's cover the most important of them in more detail.

Note: Another name for `global` is `GLOBAL`. They are aliases. Also, `global.user` and `GLOBAL.user` are the same.

## Global Object Properties

So what are the Node-specific `global` object properties (a.k.a. interfaces)? Here's the list of Node global interfaces which come with Node.js and do not exist in browser JavaScript:

* `process`: Contains the information about the system and environment, e.g., node version (`process.versions.node`)
* `module`: Exports the functionality to be used by other programs/files, i.e., utilized to create modules
* `exports`: Exports the functionality to be used by other programs. Alias of `module.exports`.
* `require`: Imports the functionality from another file/module/package, i.e., utilizes modules
* `Buffer`: Binary data type
* `__dirname`: Path and folder name of the current script
* `_filename`: Filename of the current script

Know that `global` object has interfaces specific to Node. You can also define your own global properties (object or functions). Also, there are interfaces that are the same as in browser JavaScript:

* `setInterval()`: Executes a function at a certain interval
* `setTimeout()`: Executes a function with a certain delay
* `console`: Print data in the terminal
* `clearTimeout(t)`: Removes the function of the `setTimeout()`
* `clearInterval(t)`: Removes the function of the `setInterval()`

Note: As developers, you can access them with or without referring to the `global` object. For example, both `global.process` and `process` work the same.

`Process`, `modules` and `Buffer` require their own lessons, so we'll cover them one-by-one later.

## Explicit and Implicit Global Scoping

Let's talk about scoping for a moment. We can attach any arbitrary property (i.e we come up with a name)to a `global` object explicitly. For example: 

```js
global.name = 'React Quickly'
console.log(name) // React Quickly
```

This is explicit global scoping because we wrote `global.name`. This variable becomes available not only in the current script, but in all other scripts which this instance uses. For example you can set the global name variable in the main script and it will be accessible in imported modules. Let's explore implicit global scoping.

When it comes to scoping, browser JavaScript was notorious for its "buggy" behavior of leaking variables into a global scope. For example, if `var _user = {admin: false}` code is run in DevTools `var user` will create a global object `window._user`.

Note: If we don't use `var` the variable will be a `window` as well.

So if you run this code in the DevTools console:

```js
user = {admin: false}
var _user = {admin: false}

console.log(_user, window._user)
console.log(user, window.user)
```

You would get these results which illustrate that global window references were created:

```
Object {admin: false} Object {admin: false}
Object {admin: false} Object {admin: false}
```

In other words `_user`, `window._user`, `user` and `window.user` will return `{admin: false}`.

Now let's replace `window` with global for Node. What would the result of this snippet be if you run it as a separate file (`node main.js`)?

```js
user = {admin: false}
var _user = {admin: false}

console.log(_user, global._user, GLOBAL._user)
console.log(user, global.user, GLOBAL.user)
```

The result will signify that the `var _user` did not create a global reference, only a local one.

```
{ admin: false } undefined undefined
{ admin: false }  { admin: false } { admin: false }
```

In other words,

* `console.log(_user)` returns `{ admin: false}`
* `console.log(global._user)` and `console.log(GLOBAL._user)` return `undefined`

While,

* `console.log(user)` returns `{ admin: false}`
* `console.log(global.user)` and `console.log(GLOBAL.user)` return { admin: false }

`var _user = {admin: false}` did not create a global reference because we run the code in Node and it was a file. This is one of the differences between Node and browser JavaScript.

Note: If you run the Node code in REPL, the result will be similar to browser JavaScript, i.e., the `global._user` will be created, because REPL works in a global scope.

The conclusion: In Node, if you omit `var`, the global reference will be created implicitly. This can cause confusion so therefore, avoid doing implicit declarations. If you need to create a global reference, use explicit declaration `global.NAME = VALUE`.


## Resources

1. [Official Global Object Documentation](https://nodejs.org/api/globals.html)
1. [Global Variables in Node.js](http://www.hacksparrow.com/global-variables-in-node-js.html)
1. [Variables: Scopes, Environments, and Closures in Browser JavaScript](http://speakingjs.com/es5/ch16.html)
2. [Node.js Global Namespace video](https://egghead.io/lessons/node-js-node-js-global-namespace)


---

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/node-global'>Node Global Object</a> on Learn.co and start learning to code for free.</p>
