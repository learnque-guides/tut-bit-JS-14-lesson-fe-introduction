# JS modules implemantation by using RequireJS

RequireJS is a JavaScript file and module loader. It is optimized for in-browser use, but it can be used in other JavaScript environments, like Rhino and Node. Using a modular script loader like RequireJS will improve the speed and quality of your code.

---

Let's assumes that we will keep all our JavaScript files in a *scripts* directory in our project. For example, if we have a project that has a project.html page, with some scripts, the directory layout might look like so:

* project-directory/
  * project.html
  * scripts/
    * main.js
    * helper/
      * util.js

Let's add [require.js](https://requirejs.org/docs/release/2.3.6/minified/require.js) to the scripts directory, so it looks like so:

* project-directory/
  * project.html
  * scripts/
    * require.js 
    * main.js
    * helper/
      * util.js

To take full advantage of the optimization tool, it is suggested to keep all inline script out of the HTML, and only reference require.js with a requirejs call like so to load your script:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>My Sample Project</title>
        <script data-main="scripts/main" src="scripts/require.js"></script>
    </head>
    <body>
        <h1>My Sample Project</h1>
    </body>
</html>
```

Inside of main.js, we can use requirejs() to load any other scripts you need to run. This ensures a single entry point, since the data-main script you specify is loaded asynchronously.

*main.js*
```js
requirejs(["helper/util"], function(util) {
    
});
```
---

*util.js*

```js
define(function () {
    return {
        getHello: function () {
            return 'Hello World';
        }
    };
});
```
