# Chapter 1 Block Binding

- Block scope or lexical scopes are created inside:
  1. function
  2. a block(indicated by {})
- let declarations are not hoisted at all

```js
const funcs = [];
for (var i = 0; i < 10; i++) {
  funcs.push(function () {
    console.log(i);
  });
}
funcs.forEach(function (func) {
  func(); // outputs the number 10 ten times
});
```

- the reason for the above problem is that all functions encloses the variable i which will become 10 at the end
- the solution to this is Immediately Invoked Function Expression **IIFE**, to force a **new copy** (in function arguments)

```js
for (var i = 0; i < 10; i++) {
  funcs.push(
    (function (value) {
      return function () {
        console.log(value);
      };
    })(i)

    // const tempFunc = function(value){
    //     return function(){console.log(value)}
    // }
    // tempFunc(i)
  );
}
```

- let solves the above problem by making a new variable withe the next value in the iteration with the same name (i)
- this behvior is specific to loops only.

- the take from the above is the for loop variable is a new variable in each iteration and has nothing to do with the previous iteration.

- you cannot overwrite a global variable using let or const you can only shadow it

```js
var RegExp = 12; // this overwrites window.RegExp
let RegExp = 13; // this doesn't overwrite window.RegExp
```

- tag templates are when you put a function in front of template string `` tag`prestring${variable1}string${variable2}poststring` ``
- now the function `tag` will be invoked like this tag(['prestring', 'string', 'poststring'], variable1, variable2)
