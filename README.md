# Node Global Object

## Overview

This lesson will cover the 

## Objectives

1. Describe the global object
1. Describe the global object properties: process, global API, etc.
1. Describe the global scoping

## Global Object

Node is JavaScript, right? Not exactly. While both Node and browser JavaScript are implementations of ECMAScript, they differ just as different flavors of browser JavaScript implementation can differ. For example, there might be some methods and functions in Internet Explorer or Firefox which are lacking in Safari or vice versa. 

So the bottom line is while most of the browser JavaScript implementations and Node are similar, for example, `console.log()`, `setTimeout()`, Array and String functions, they differ drastically when it comes to global methods and properties (a.k.a. interfaces). There's no `window` in Node!

Why and what exactly is the difference? You see, in browsers we don't have the ability to import modules or work with file system (I'm writing about ES5 mostly). We also limited in what information we can get from the environment. The server or Node code can do much more than the browser, so we need to introduce some global interfaces. They live on the `global` object. So you can print them with this statement:

```js
console.log(global)
```

Or you can type `global` in Node REPL. The output would be similar to this:

```
> global
{ DTRACE_NET_SERVER_CONNECTION: [Function],
  DTRACE_NET_STREAM_END: [Function],
  DTRACE_HTTP_SERVER_REQUEST: [Function],
  DTRACE_HTTP_SERVER_RESPONSE: [Function],
  DTRACE_HTTP_CLIENT_REQUEST: [Function],
  DTRACE_HTTP_CLIENT_RESPONSE: [Function],
  global: [Circular],
  process:
   process {
     title: 'node',
     version: 'v5.1.0',
     moduleLoadList:
      [ 'Binding contextify',
        'Binding natives',
        'NativeModule events',
        ...
        'NativeModule os',
        'Binding os',
        'NativeModule string_decoder' ],
     versions:
      { http_parser: '2.6.0',
        node: '5.1.0',
        v8: '4.6.85.31',
        uv: '1.7.5',
        zlib: '1.2.8',
        ares: '1.10.1-DEV',
        icu: '56.1',
        modules: '47',
        openssl: '1.0.2d' },
     arch: 'x64',
     platform: 'darwin',
     release:
      { name: 'node',
        sourceUrl: 'https://nodejs.org/download/release/v5.1.0/node-v5.1.0.tar.gz',
        headersUrl: 'https://nodejs.org/download/release/v5.1.0/node-v5.1.0-headers.tar.gz' },
     argv: [ '/usr/local/bin/node' ],
     execArgv: [],
     env:
      { PATH: '/usr/local/var/rbenv/shims:/usr/local/var/rbenv/shims:/Applications/SenchaSDKTools-2.0.0-beta3:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/azat/.rvm/bin:/Users/azat/bin',
        TMPDIR: '/var/folders/q5/0zn95nld30b7fnhz5yywb52m0000gn/T/',
        LOGNAME: 'azat',
        XPC_FLAGS: '0x0',
        HOME: '/Users/azat',
        Apple_PubSub_Socket_Render: '/private/tmp/com.apple.launchd.byOyjyCo2f/Render',
        LANG: 'en_US.UTF-8',
        COLORFGBG: '7;0',
        USER: 'azat',
        ...
        RBENV_ROOT: '/usr/local/var/rbenv',
        _: '/usr/local/bin/node' },
     pid: 74409,
     features:
      { debug: false,
        uv: true,
        ipv6: true,
        tls_npn: true,
        tls_alpn: true,
        tls_sni: true,
        tls_ocsp: true,
        tls: true },
     _needImmediateCallback: false,
     execPath: '/usr/local/bin/node',
     debugPort: 5858,
     _startProfilerIdleNotifier: [Function: _startProfilerIdleNotifier],
     _stopProfilerIdleNotifier: [Function: _stopProfilerIdleNotifier],
     _getActiveRequests: [Function: _getActiveRequests],
     _getActiveHandles: [Function: _getActiveHandles],
     reallyExit: [Function: reallyExit],
     abort: [Function: abort],
     chdir: [Function: chdir],
     cwd: [Function: cwd],
     umask: [Function: umask],
     getuid: [Function: getuid],
     geteuid: [Function: geteuid],
     setuid: [Function: setuid],
     seteuid: [Function: seteuid],
     setgid: [Function: setgid],
     setegid: [Function: setegid],
     getgid: [Function: getgid],
     getegid: [Function: getegid],
     getgroups: [Function: getgroups],
     setgroups: [Function: setgroups],
     initgroups: [Function: initgroups],
     _kill: [Function: _kill],
     _debugProcess: [Function: _debugProcess],
     _debugPause: [Function: _debugPause],
     _debugEnd: [Function: _debugEnd],
     hrtime: [Function: hrtime],
     dlopen: [Function: dlopen],
     uptime: [Function: uptime],
     memoryUsage: [Function: memoryUsage],
     binding: [Function: binding],
     _linkedBinding: [Function: _linkedBinding],
     _events:
      { newListener: [Function],
        removeListener: [Function],
        SIGWINCH: [Object] },
     _rawDebug: [Function],
     domain: [Getter/Setter],
     _maxListeners: undefined,
     EventEmitter:
      { [Function: EventEmitter]
        EventEmitter: [Circular],
        usingDomains: true,
        defaultMaxListeners: 10,
        init: [Function],
        listenerCount: [Function] },
     _fatalException: [Function],
     _exiting: false,
     assert: [Function],
     config: { target_defaults: [Object], variables: [Object] },
     nextTick: [Function: nextTick],
     _tickCallback: [Function: _tickDomainCallback],
     _tickDomainCallback: [Function: _tickDomainCallback],
     stdout: [Getter],
     stderr: [Getter],
     stdin: [Getter],
     openStdin: [Function],
     exit: [Function],
     kill: [Function],
     _eventsCount: NaN },
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
  require:
   { [Function: require]
     resolve: [Function],
     main: undefined,
     extensions: { '.js': [Function], '.json': [Function], '.node': [Function] },
     cache: {} },
  _: [Circular],
```

Let's cover the most important of them in more details.

Note: Another name for `global` is `GLOBAL`. They are aliases. So `global.user` and `GLOBAL.user` are the same.

## Global Object Properties

So what are the Node-specific global interfaces? Here's the list of Node global interfaces which do not exist in browser JavaScript:

* `process`: Contains the information about the system and environment, e.g., node version (`process.versions.node`)
* `module`: Exports the functionality to be used by other programs/files, i.e., utilized to create modules
* `exports`: Exports the functionality to be used by other programs. Alias of `module.exports`.
* `require`: Imports the functionality from another file/module/package, i.e., utilizes modules
* `Buffer`: Binary data type 
* `__dirname`: Path and folder name of the current script
* `_filename`: Filename of the current script 

Know that `global` object has interfaces specific to Node. Others are the same as in browser JavaScript:

* `setInterval()`
* `setTimeout()`
* `console`
* `clearTimeout(t)`
* `clearInterval(t)`

Note: Developers you can access them with or without referring to the `global` object. For example, both `global.process` and `process` work the same. 

Modules and Buffer requires their own lessons, so we'll cover them one-by-one later. For now let's look more into `process`. 

## Process

`process` has a lengthy number of properties related to the currently running Node instance and the environment. 

* `process.env`: Environmental variables
* `process.pid`: Process ID 
* `process.platform`: Platform, e.g., `darwin`
* `process.cwd()`: Current working directory. Not always the same as `__dirname`.
* `process.versions`: Versions of node, V8, zlib and other Node internal components
* `process.features`: Features of this Node instance, e.g., `debug`p
* `process.arch`: Architecture of this system, e.g., `x64`
* `process.uptime()`: Time this process runs in seconds
* `process.memoryUsage()`: The heap total and used numbers

It also has methods to terminate the process:

* `process.exit(1)`: Exit the current process with errors
* `process.exit(0)`: Exit the current process with no errors
* `process.kill(pid)`: Terminate a process with ID `pid`, e.g., to kill self is `process.kill(process.pid)`

If this was a mouthful of information, refrain from worrying. Instead use this page when you need it and know that the system information can be found in `process`.

## Explicit and Implicit Global Scoping

Let's talk about scoping for a moment. We can attach any arbitrary (meaning we come up with a name) property to a `global` object explicitly, e.g., 

```js
global.name = 'React Quickly'
console.log(name) // React Quickly
```

This is explicit global scoping because we wrote `global.name`. This variable become available not only in the current script, but in all other scripts which this instance uses. For example you can set the global name variable in the main script and it will be accessible in imported modules. More on modules later. Let's explore implicit global scoping.

When it comes to scoping, browser JavaScript was notorious for it's "buggy" behavior of leaking variables into a global scope. For example, if `var _user = {admin: false}` code is run in DevTools `var user` will create a global object `window._user`. 

Note: If we don't use `var` the variable will be a `window` as well. 

So if you run this code in the DevTools console:

```js
user = {admin: false}
var _user = {admin: false}

console.log(_user, window._user, window._user)
console.log(user, window.user, window.user)
```

You would get these results which illustrate that global window references were created:

```
Object {admin: false} Object {admin: false} Object {admin: false}
Object {admin: false} Object {admin: false} Object {admin: false}
```

Now let's replace `window` with global for Node. What the result of this snippet would be if you run it as a separate file (`$ node main.js`)?

```js
user = {admin: false}
var _user = {admin: false}

console.log(_user, global._user, GLOBAL._user)
console.log(user, global.user, GLOBAL.user)
```

The result will signify that the `var _user` did not create a global reference, only a local one.

```
{ admin: false } undefined undefined
{ admin: false } { admin: false } { admin: false }
```

The conclusion: In Node, if you omit `var`, the global reference will be created implicitly. This can cause confusion; therefore, avoid doing implicit declarations. If you need to create a global reference, use explicit declaration `global.NAME = VALUE`.

Note: If you run the Node code in REPL, the result will be similar to browser JavaScript, i.e., the `global._user` will be created, because REPL works in a global scope.

## Resources

1. [Official Global Object Documentation](https://nodejs.org/api/globals.html)
1. [Global Variables in Node.js](http://www.hacksparrow.com/global-variables-in-node-js.html)
1. [Variables: Scopes, Environments, and Closures in Browser JavaScript](http://speakingjs.com/es5/ch16.html)


---

<a href='https://learn.co/lessons/node-global' data-visibility='hidden'>View this lesson on Learn.co</a>
