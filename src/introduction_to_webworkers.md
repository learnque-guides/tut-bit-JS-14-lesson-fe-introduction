# Introduction to JavaScript workers

* JavaScript workers let for us to solve problem - JavaScript Concurrency
* JavaScript workers brings Threading to JavaScript

*The Web Workers specification defines an API for spawning background scripts in your web application. Web Workers allow you to do things like fire up long-running scripts to handle computationally intensive tasks, but without blocking the UI or other scripts to handle user interactions.*

Due to their multi-threaded behavior, web workers only has access to a subset of JavaScript's features:

* The navigator object
* The location object (read-only) 
* XMLHttpRequest
* setTimeout()/clearTimeout() and setInterval()/clearInterval()
* The Application Cache
* Importing external scripts using the importScripts() method
* Spawning other web workers

Workers do NOT have access to:

* The DOM (it's not thread-safe)
* The window object
* The document object
* The parent object

Let's look at simple example if we want to understand what workers are?