## Currying

### What is currying ?
* Currying is an advanced function in JavaScript which is used for the manipulation of functions' arguments and parameters.
* It was named after "Haskell B. Curry". The concept of currying in Javascript comes from the Lambda calculus.
* Currying takes a function that receives more than one parameter and breaks it into a series of unray (one parameter) functions.
* Hence, the currying function takes only one parameter at a time.

#### Uses of Currying Function
* Currying in JavaScript can be for the following reasons:
* Currying is helpful in Event handling.
* By using the currying function, we can avoid passing the same variable many times.
* Currying in JavaScript can be used to make a higher-order function.


#### Question 1 - Evaluate(”sum”)(2)(4) ⇒ 2+4 = 6 on basis of input given to first param.

```js
function sum(operation) {
  return (a) => {
    return (b) => {
      if (operation === "sum") return a + b;
      else if (operation === "multiply") return a * b;
      else if (operation === "divide") return a / b;
      else if (operation === "subtract") return a - b;
      else return "No / Invalid Operation Selected";
    };
  };
}
```

#### Question 2 - Write a currying function that takes infinite arguments.

> sum(1)(2)(3)(4)..(n)()

```js
const sum = function (a) {
  return function (b) {
    return function (c) {
      return function (d) {
        ...
        ...
        ...
        return a + b + c + d + ... + n;
      };
    };
  };
};

//recursive solution
const sum = function (a) {
  return function (b) {
    if (b) {
      return sum(a + b);
    } else {
      return a;
    }
  };
};

// The above recursive solution, will keep returning a function (the sum function in above case, until arguments are provided)
// While returning a function each time, the arguments are added and the sum function gets called
// The sum function returns a function with the value passed in parameter 'a' stored in lexical scope or through the closure concept
// Once there are no more arguments specified, we simply return the value of 'a' which is the added total result

// In ES6 syntax
const sum = (a) => {
  return (b) => {
    if (b) {
      return sum(a + b);
    } else {
      return a;
    }
  };
};

// Simplified to one line
const sum = a => b => b ? sum(a + b) : a;
```
