# Indentation and Code Style

Indentation and code style play an important role in creating clean, readable, and maintainable code. They help us as developers quickly understand the structure and logic of a program, facilitating teamwork and reducing the number of errors.

# Indentations

1. **Select between spaces and tabs**:

- **Spaces**: Using spaces usually provides more predictable formatting because the space is always the same width.
- **Tabulation**: Tab allows developers to adjust the indent width to their liking within the editor, but can lead to alignment issues across editors.

2. **Consistency**: 

- It is important to use the same indentation method throughout the project. Many teams choose spaces (usually 2 or 4 spaces) or tabs, but the key is to stick to the method you choose.

- Example: 

```javascript
// Consistent indentation

if (isConditionTrue) {
    doSomething();
}
```

3. **Recommendations for indentation**:

- **JavaScript**: Typically 2 spaces are used for indentation.
- **Python**: PEP 8 recommends using 4 spaces for indentation.
- **HTMl/CSS**: Typically 2 or 4 spaces are used for indentation.


# Code style

1. **Naming**: 

- **Variables and functions**:  Use camelCase descriptive names for variables and functions.

```javascript 
// ❌ 

let x = 5;
function foo() { }

// ✔

let userAge = 5;
function calculateSum() { }
```

- **Classes and constructors**: Use PascalCase for class and constructor names.

```javascript
// ❌
class user { }

// ✔
class User { }
```

2. **Formatting**: 

- **Brackets**: Use an opening parenthesis on the same line as the function or condition declaration.

```javascript
// ❌
if (isConditionTrue)
{
    doSomething();
}

// ✔
if (isConditionTrue) {
    doSomething();
}
```

- **Spaces around operators**: Add spaces around operators to improve readability.

```javascript
// ❌
let sum=x+y;

// ✔
let sum = x + y;
```

3. **Commenting**: 

- **Comments**: Comments should be used to explain complex or non-trivial parts of the code. Avoid excessive comments.

```javascript
// ❌
let age = 30; // We declare the age variable and assign it the value 30

// ✔
// User age is required to calculate insurance conditions
let userAge = 30;
```

4. **Consistency**: 

- Stick to the same formatting style and conventions throughout the project. This includes using consistent indentation, formatting parentheses, naming variables and functions, etc.

- Example: 

```javascript 
// ❌
function add(a,b){
return a+b;}

// ✔
function add(a, b) {
    return a + b;
}
```

5. **Tools for checking code style**:

- **ESLint**: For JavaScript and TypeScript.
- **Prettier**: Automatic code formatter for many languages.
- **Pylint and flake8**: For Python.
- **Stylelint**:  For CSS/SCSS.