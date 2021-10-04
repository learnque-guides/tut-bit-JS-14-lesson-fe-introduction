# Let's understand how TS works by live example

* Let's create npm project by using `npm init`
* Let's install typescript compiler with `npm install -g typescript`
* Add main script in your `package.json`:

```json
{
  "name": "ts-intro",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "compile": "tsc index.ts",
    "exec": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```