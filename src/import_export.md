# JS modules by using native approach (import/export)

* JavaScript now has standardized syntax for exactly that. Within a module, you can use the export keyword to export just about anything. You can export a const, a function, or any other variable binding or declaration. Just prefix the variable statement or declaration with export and you’re all set:

```js
// 📁 lib.mjs
export const repeat = (string) => `${string} ${string}`;
export function shout(string) {
  return `${string.toUpperCase()}!`;
}
```

You can then use the import keyword to import the module from another module. Here, we’re importing the repeat and shout functionality from the lib module, and using it in our main module:

```js
// 📁 main.mjs
import {repeat, shout} from './lib.mjs';
repeat('hello');
// → 'hello hello'
shout('Modules in action');
// → 'MODULES IN ACTION!'
```

You could also export a default value from a module:

```js
// 📁 lib.mjs
export default function(string) {
  return `${string.toUpperCase()}!`;
}
```

Such default exports can be imported using any name:

```js
// 📁 main.mjs
import shout from './lib.mjs';
//   
```

On the web, you can tell browsers to treat a <script> element as a module by setting the type attribute to module.

```html
<script type="module" src="main.mjs"></script>
<script nomodule src="fallback.js"></script>
```