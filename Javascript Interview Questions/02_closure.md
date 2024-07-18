## Closure

### What will be output of below question ?

#### Question 1

```
function outer() {
  var x = 10;

  function inner() {
    console.log(x);
  }

  return inner;
}

var innerFunc = outer();

innerFunc();

// Output: 10
// Reason: This is because the outer function returns the inner function.
// which has access to the x variable declared in the outer function's scope.
// When innerFunc is called, it logs the value of x, which is 10.
```

#### Question 2

```
function outer() {
  var x = 10;

  function inner() {
    console.log(x);
  }

  x = 20;

  return inner;
}

var innerFunc = outer();

innerFunc();

// Output: 20
// Reason: This is because the inner function has access to the x variable in the outer function's scope,
// and that variable is assigned the value of 20 before the inner function is returned. When innerFunc is called,
// it logs the current value of x, which is 20
```

#### Question 3

```
function outer() {
  var x = 10;

  function inner() {
    var y = 5;

    console.log(x + y);
  }

  return inner;
}

var innerFunc = outer();

innerFunc();

// Output: 15
// Reason: This is because the inner function has access to both the x variable declared in the outer function's scope
// and the y variable declared within the inner function's scope. When innerFunc is called, it logs the sum of x and y, which is 15.
```

#### Question 4

```
function outer() {
  var x = 10;

  function inner() {
    var y = 5;

    console.log(x + y);
  }

  var x = 20;

  return inner;
}

var innerFunc = outer();

innerFunc();

// Output: 25
// Reason: This is because the inner function has access to the x variable declared in the outer function's scope,
// which is reassigned the value of 20 before the inner function is returned. When innerFunc is called, it logs the sum of the current value of x and y, which is 25.
```

#### Question 5

```
function outer() {
  var x = 10;

  function inner() {
    var y = 5;

    console.log(x + y);

    x = 20;
  }

  return inner;
}

var innerFunc = outer();

innerFunc();

innerFunc();

// Output: 15
// Output: 25
// Reason: This is because the inner function has access to the x variable declared in the outer function's scope,
// which is initially assigned the value of 10. When innerFunc is called for the first time,
// it logs the sum of x and y, which is 15, and then reassigns the value of x to 20. When innerFunc is called for the second time,
// it logs the sum of the new value of x and y, which is 25.
```
