## babel-preset-env [![npm](https://img.shields.io/npm/v/babel-preset-env.svg)](https://www.npmjs.com/package/babel-preset-env) [![travis](https://img.shields.io/travis/babel/babel-preset-env/master.svg)](https://travis-ci.org/babel/babel-preset-env)

> Babel preset for all envs.

## Install

```sh
$ npm install --save-dev babel-preset-env
```

## Usage via `.babelrc`

### Options

* `targets` - an object of browsers/environment versions to support (ex: chrome, node, etc).

The data for this is currently at: [/data/plugins.json](/data/plugins.json) and being generated by [/scripts/build-data.js](/scripts/build-data.js) using https://kangax.github.io/compat-table.

> We would like help to make the data is correct! This just means usage/testing!

Currently: "chrome, edge, firefox, safari, node"

> Some node features are > `6.5`.

*browsers* (array/string) - an query to select browsers (ex: last 2 versions, > 5%).  
Note, browsers' results are overridden by explicit items from `targets`.

* `loose` (boolean) - Enable "loose" transformations for any plugins in this preset that allow them (Disabled by default).
* `modules` - Enable transformation of ES6 module syntax to another module type (Enabled by default to `"commonjs"`).
  * Can be `false` to not transform modules, or one of `["amd", "umd", "systemjs", "commonjs"]`.
* `debug` (boolean) - `console.log` out the targets and plugins being used as well as the version specified in `/data/plugins.json`.

```js
{
  "presets": [
    ["env", {
      "targets": {
        "chrome": 52,
        "browsers": "last 2 safari versions"
      },
      "loose": true,
      "modules": false
    }]
  ]
}
```

### Example

```js
// src
export class A {}
```

```js
// default is to run all transforms
{
  "presets": [
    ["env", {}]
  ]
}

// ...

var A = exports.A = function A() {
  _classCallCheck(this, A);
};
```

```js
// target chrome 52
{
  "presets": [
    ["env", {
      "targets": {
        "chrome": 52
      }
    }]
  ]
}

// ...

class A {}
exports.A = A;
```

```js
// target chrome 52 with webpack 2/rollup
{
  "presets": [
    ["env", {
      "targets": {
        "chrome": 52
      },
      "modules": false
    }]
  ]
}

// ...

export class A {}
```

```js
// using browserslist
{
  "presets": [
    ["env", {
      "targets": {
        "chrome": 52,
        "browsers": ["last 2 versions", "safari 7"]
      }
    }]
  ]
}

// ...

export class A {}
```

### Example with `debug: true`

```js
Using targets: {
  "node": 6.5
}

Using plugins:

module: false
transform-exponentiation-operator {}
transform-async-to-generator {}
syntax-trailing-function-commas {}
```
