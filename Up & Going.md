# Up & Going

## Compound assignment
`+=`, `-=`, `*=` and `/=` <br>
ej: `a += 2` (same as `a = a + 2`)

## Types
* `string`
* `number`
* `boolean`
* `object`
* `function`
* `null` and `undefined`
* `symbol` ( new to ES6 )

## Objects 
```js
let obj = {
  a: 1,
  b: 2
}
```
`obj.a // 1`<br>
`obj.b // 2` <br>
`obj['a'] // 1` <br>
`obj['b'] // 2` <br>

## Comparations

When to use `===`
- If either value (sides) in a comparation could be `true` or `false` value 
- If either value (sides) in a comparation could be `0`, `''` or `[]` <br>

In all others cases your are safe to use `==`

## Arrays comparation Strings
`var a = [1, 2, 3]`<br>
`var b = [1, 2, 3]`<br>
`var c = '1, 2, 3'`<br>
<br>
`a == c; //true`<br>
`b == c; //true`<br>
`a == b; //false`<br>

## Numbers comparation Strings
`var a = 41`<br>
`var b = '42'`<br>
`var c = '43'`<br>
<br>
`a < b; //true`<br>
`b < c; //true`<br>
<br>
If both values in a comparations are string the comparison is made lexicographically (`'z'` > `'a'`), but if one of them is a number they both coerced to numbers

## Hoisting
```js
var a = 2;
foo() //works because foo() declaration is hoisted
function foo() {
console.log('hola');
}
```

## Use Strict
`'use strict'`<br>
The purpose of "use strict" is to indicate that the code should be executed in "strict mode".
With strict mode, you can not, for example, use undeclared variables.

## Functions
```js
function foo(){};
var foo = function(){};
var foo = () => {};
```

## Immediately invoked function
```js
(function IIFE(){
  console.log('Hello!');
})();
```

## Closure
A closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
To use a closure, simply define a function inside another function and expose it. To expose a function, return it or pass it to another function.
The inner function will have access to the variables in the outer function scope, even after the outer function has returned.
```js
function makeAdder(x) {
  
  function add(y) {
    return y + x;
  }
  
  return add;
}

var plusTen = makeAdder(10);
plusTen(13); // 23 ---> 13 + 10
```
## Modules 
The most common usage of closure is the module pattern. Modules let you define private implementation details (variables, functions) that are hidden from the outside world, as well as a public API that is accessible from outside.
```js
function User() {
  var username, password;
  
  function dologin(user, pw) {
    username = user;
    password = pw;
    //do the rest of the logic
  }
  
  var publicAPI = {
    login: doLogin
  }
  
  return publicAPI;
}

// Create a `User` module instance
var fred = User();
fred.login('fred', '1234');
```
## This
```js
function foo() {
  console.log(this.bar);
}

var bar = "global";

var obj1 = {
  bar: "obj1",
  foo: foo
};

var obj2 = {
  bar: "obj2"
};

//----------------------
foo();          // "global"
obj1.foo();     // "obj1"
foo.call(obj2)  // "obj2"
new foo()       // undefined
```
There are four rules for how this gets set
  - 1- `foo()` ends up setting this to the global object in non-strict mode, in strict mode, this would be undefined and you'd get an error in accessing the bar property - so `"global"` is the value found for `this.bar`.
  - 2- `obj.foo()` sets `this` to the `obj1`object.
  - 3- `foo.call(obj2)` sets `this` to the `obj2` object.
  - 4- `new foo()` sets `this` to a brand new empty object.
  
## Object.create()
```js
var foo = {
  a: 42
}
//Create `bar` and link it to `foo`
var bar = Object.create( foo );
bar.b = 'hello, world'

bar.b;    // 'hello, world'
bar.a;    // 42  <--- delegated to `foo`
```
## Polyfilling
Is an invented term to refer to taking the definition of a newer feature and producing a piece of code that is equivalent to the behavior but is able to run in older JS envioronments.
Consider:

```js
if(!Number.isNaN) {
  Number.isNaN = function(x) {
    return x !== x;
  }
}
```

## Transpiling
There is no way to polyfill new syntax that has been added to the language. The new syntax would throw an error in the old JS engine as unrecognized/invalid.

Example:
```js
function foo(a = 2){
  console.log( a );
}

foo(); // 2
foo(42); // 42
```
```js
function foo() {
  var a = arguments[0] !== (void 0) ? arguments[0] : 2;
  console.log(a);
}
```
