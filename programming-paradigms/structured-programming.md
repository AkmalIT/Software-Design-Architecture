# Structured

**Structured Programming** is a programming paradigm aimed at improving the clarity, quality, and development time of software by using structured control flow constructs. It emphasizes the use of sequences, selection, and iteration to create clear and easily understandable programs.

**Key Characteristics**:

1. **Modularity**: Programs are divided into modules or subroutines, each with a single entry and exit point.
2. **Control Structures**: Uses three main types of control structures: sequence, selection (if-then-else), and iteration (loops).
3. **Avoidance of Goto Statements**: Replaces the use of "goto" statements with structured control constructs to improve readability and maintainability.
4. **Top-Down Design**: Starts with a high-level overview of the system and breaks it down into more manageable parts.

# Real-Life Analogy

**Structured Assembly Line**: Imagine an assembly line in a factory. Each station (module) on the line has a specific task (subroutine). The product moves through each station in a sequence, with decisions (if-then-else) determining the path (e.g., whether to paint the product red or blue). The process repeats (loops) for each product.

**Examples of Structured Programming Languages**:

- **C**: A language designed with structured programming principles.
- **Pascal**: Known for its strong emphasis on structured programming.
- **Java**: Uses structured programming principles in its design.

# Structured Programming in JavaScript

JavaScript supports structured programming, allowing developers to write clear and modular code using functions, loops, and conditionals.

**Examples**:

1. **Using Functions for Modularity**:

- Breaking down tasks into smaller, reusable functions.

```javascript
// Function for calculating factorial
function factorial(n) {
  if (n === 0) {
    return 1;
  }
  return n * factorial(n - 1);
}

console.log(factorial(5)); // Output: 120
```

2. **Control Structures (Sequence, Selection, Iteration)**:

- Using if-else and loops to control the flow of the program.

```javascript
// Structured programming example with control structures
function checkNumber(num) {
  if (num > 0) {
    console.log("Positive number");
  } else if (num < 0) {
    console.log("Negative number");
  } else {
    console.log("Zero");
  }
}

for (let i = -1; i <= 1; i++) {
  checkNumber(i);
}
// Output:
// Negative number
// Zero
// Positive number
```

3. **Top-Down Design**:

- Starting with a high-level function and breaking it down into smaller sub-functions.

```javascript
// Top-down design example
function main() {
  greetUser();
  const result = performCalculation(5, 3);
  displayResult(result);
}

function greetUser() {
  console.log("Welcome to the program!");
}

function performCalculation(a, b) {
  return a + b;
}

function displayResult(result) {
  console.log("The result is:", result);
}

main();
// Output:
// Welcome to the program!
// The result is: 8
```

# Benefits of Structured Programming:

1. **Readability**: Improves the readability and understandability of the code.
2. **Maintainability**: Easier to maintain and modify due to clear structure and modular design.
3. **Debugging**: Simplifies debugging by isolating different parts of the program.
4. **Reusability**: Promotes code reuse through functions and modules.

# Guidelines for Structured Programming:

1. **Use Functions**: Break down tasks into smaller functions or modules.
2. **Control Flow Structures**: Use sequence, selection (if-else), and iteration (loops) instead of goto statements.
3. **Single Entry and Exit Points**: Ensure each module or function has a single entry and exit point.
4. **Top-Down Approach**: Start with a high-level design and break it down into more detailed parts.
