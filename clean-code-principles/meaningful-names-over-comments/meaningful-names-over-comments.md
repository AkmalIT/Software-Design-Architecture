# Meaningful Names

Using meaningful names refers to the practice of giving variables, functions, classes, and other entities names that clearly describe their purpose or usage. Meaningful names improve the readability and understandability of the code, making it easier for others (and yourself) to understand what the code does without needing extensive comments or documentation.

### Guidelines for Meaningful Names

1. **Be Descriptive**: Names should convey the purpose of the variable, function, or class.
2. **Use Pronounceable Names**: Names should be easy to read and pronounce.
3. **Avoid Abbreviations**: Avoid using unclear abbreviations. Use full words unless an abbreviation is widely understood.
4. **Consistent Naming**: Use a consistent naming convention throughout the codebase.
5. **Avoid Generic Names**: Names like `data`, `temp`, and `info` are too generic and should be avoided.

## Benefits of Meaningful Names

1. **Readability**: Code becomes easier to read and understand.
2. **Maintainability**: Meaningful names make it easier to maintain and update the code.
3. **Collaboration**: Team members can more easily understand and work with the code.
4. **Less Reliance on Comments**: Clear names reduce the need for comments to explain what the code does.

## Example

### Poor Naming Example

```javascript
function d(x, y) {
  return x + y;
}

const n = "John";
const a = 25;
const p = "Engineer";

class p {
  constructor(n, a) {
    this.n = n;
    this.a = a;
  }
  getP() {
    return this.n + " is a " + this.a;
  }
}

// good example of meaningful names

function addNumbers(firstNumber, secondNumber) {
  return firstNumber + secondNumber;
}

const name = "John";
const age = 25;
const profession = "Engineer";

class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  getProfession() {
    return this.name + " is a " + this.profession;
  }
}
```
