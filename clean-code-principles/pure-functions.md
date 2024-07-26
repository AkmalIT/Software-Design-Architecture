# Pure Function

A pure function is a function that meets the basic conditions:

1. **Determinism**: Given the same input data, it always returns the same result.
2. **No side effects**: Does not change the external state, is not dependent on it, and does not cause any changes outside its own context.

# Why are pure functions needed?

1. **Ease of testing**: Pure functions are easy to test because they do not depend on external state. To check the correct operation, it is enough to test them with different input data.
2. **Predictability**: They behave predictably, which makes them reliable and reduces the likelihood of errors.
3. **Parallelism and caching**: Pure functions can be executed in parallel and their results can be cached, since there is no dependence on external state.
4. **Simplify debugging**: Easier to debug code since each pure function is independent and predictable.

# Example 1

Here's a simple example of a pure function in JavaScript:

```javascript
// Pure function that returns the sum of two numbers
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5 (always returns the same result for the same input data)
```

# Example 2

An example of a function that is not pure:

```javascript
let counter = 0;

// The function increments the global counter - this is a side effect
function incrementCounter() {
  counter++;
  return counter;
}

console.log(incrementCounter()); // 1
console.log(incrementCounter()); // 2 (the result depends on the external state)
```

# Example 3

Pure function that calculates the factorial of a number:

```javascript
// Pure function to calculate the factorial of a number
function factorial(n) {
  if (n === 0) {
    return 1;
  }
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
console.log(factorial(5)); // 120 (always returns the same result for the same input data)
```
