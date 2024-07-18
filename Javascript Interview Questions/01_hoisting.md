## Hoisting

### What will be output of below code ?

#### Question 1

```js
console.log(a);

var a = 10;

// Output: undefined
// Reason: var a will be hoisted on top with undefined value.
```

#### Question 2

```js
var a = 5;

(function () {
  console.log(a);

  var a = 10;
})();

// Output: undefined
// Reason: var a which is indside IIFE will be hoisted inside function only because of functional level scoping.
```

#### Question 3

```js
function test() {
  console.log(a);

  var a = 10;

  console.log(a);
}
test();

// Output: undefined (first console)
// Output: 10 (second console)
// Reason: var a will be hoisted inside function with undefined value so first console will print undefined.
// While before printing value of second console value 10 will be assigned to var a.
```

#### Question 4

```js
var a = 1;
function b() {
  // Hoisted  function a() {}
  a = 10;
  return;
  function a() {}
}
b();
console.log(a);

// Output: 1
// Reason: Because we are printing outside of function it will print gloabl variable a.
```

#### Question 5

```js
function foo() {
  function bar() {
    return 3;
  }
  return bar();
  function bar() {
    return 8;
  }
}
console.log(foo());

// Output: 8
// Reason: Initially first bar function will be hoisted then second bar function will be hoisted, which will override first one.
```

#### Question 6 (important)

```js
function parent() {
  var hoisted = "I'm a variable";
  function hoisted() {
    return "I'm a function";
  }
  return hoisted();
}
console.log(parent());

// Output: “TypeError: hoisted is not a function”
// Reason: Now, in such a case of multiple declarations(variable and function in the same scope) with the same identifier, the hoisting of variables is simply IGNORED.
// The the interpreter comes across the function declaration and hoists it.
// Finally, the statement of variable assignment (which was not hoisted) is executed and “I’m a variable” is assigned to hoisted, which is a simple string value and not a function. Hence the error!.
```

#### Question 7 

```js
var myVar = "foo";
(function () {
  console.log("Original value was: " + myVar);
  var myVar = "bar";
  console.log("New value is: " + myVar);
})();

// Output: Original value was: undefined
// Output: New value is: bar
// Reason: functional level scoping
```
