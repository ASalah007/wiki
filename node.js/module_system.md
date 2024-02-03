# Javascript module systmes

- there are two main module systems in javascript:
  1. commonjs
  2. ecmascript module system (ESM)

## CommonJS

Commonjs specs specifies two main concepts:

1. `require` is a function that allows you to import module from the local file system
2. `exports` and `module.exports` are special variables that are used to export public functionalities

- basic example of how the `require function works:`

```js
function require(moduleName) {
  const id = require.resolve(moduleName);
  if (require.cache[id]) {
    return require.cache[id].exports;
  }

  // module metadata
  const module = {
    exports: {},
    id,
  };

  // update the cache
  require.cache[id] = module;

  // load the module
  loadModule(id, module, require);

  return module.exports;
}

require.cache = {};
require.resolve = (moduleName) => {
  // resolves module id (full path) from the moduleName
};

function loadModule(filename, module, require) {
  const wrappedSrc = `(function(module, exports, require){
    ${fs.readFileSync(filename, "utf8")}
   })(module, module.exports, require)`;
}
```

- as you can see from the loadModule function the src code of any module is just the body of a function
  this function takes three arguments:

  1. **module**: which is object created by the `require` function
  2. **exports**: which is just a reference to module.exports
  3. **require**: the require function so that the module can load its dependencies

- the `require` function is synchronous. As a consequence any assignment to module exports must be synchronous as well. the following code is wrong:

```js
setTimeout(()=>{
  module.exports = function () {...}
}, 0)
```

- **Dependency hell**: when two or more dependencies of your program depend on a shared dependency but each one require different incompatible version.

- there are three types of modules that the `resolve` method consider:

  1. **File Module**: starts with `/` or `./`. i.e `require("./module")`

  2. **Core Module**: if the module name doesn't include `/` or `./`, the resolve algorithm first searches in node.js core modules.

  3. **Packege Module**: if the module is not a core module, the algorithm start searching inside in **node_modules** directories, starting from the current directory of the module navigating up until it reaches the root file system or find the module.

- the resolve algorithm when given the `moduleName` it searches for:
  1. `<moduleName>.js`
  2. `<moduleName>/index.js`
  3. the directory/file specified in the main property of `<moduleName>/package.json`

## EcmaScript Modules

- node.js consider any .js file to be written using commonJs syntax by default,
  to use ESM modules you have to do one of the following:

  1. rename the file to `<filename>.mjs`
  2. add `"type": "module"` in the nearest package.json file

- in ESM you must include js file extenstion:

  1. **WRONG**: `import some from "./some"`
  2. **RIGHT**: `import some from "./some.js"`

- you must include protocol with absolute paths:

  1. **WRONG:** `import any from "/path/to/any.js"`
  2. **RIGHT:** `import any from "file:///path/to/any.js"`

- Dynamic Modules: you can import modules at runtime using the import function

  ```js
  const module_id = `${user_input}`;
  import(module_id).then((module) => {
    module.functionality();
  });
  ```

- in commonjs all the code before the require function is guaranteed to be executed, while in ESM the evaluation of the module and its assignment is independent.
  this means that the whole module might be evaluated before reaching its import statement.

- the imported module in esm is read-only live binding, which means you can't change or modify what references are referring to.

```js
import { cout, incrementCount } from "./couter.js";
console.log(count); // 1
incrementCount();
console.log(count); // 2
count = 10; // Error
```
