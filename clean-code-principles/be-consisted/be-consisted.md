# Be Consistent


Being consistent refers to maintaining a consistent pattern. This can include using consistent naming conventions, data structures, and interfaces throughout the system, as well as adhering to established design principles and best practices. Consistency can help to make the system more maintainable, understandable, and extendable.

Consistency in coding can be applied to various aspects of a software project, including:

- **Naming Conventions**: Using a consistent style for naming variables, functions, classes, and other entities.
- **Code Structure**: Keeping the structure of the codebase consistent, such as file organization and layout.
- **Data Structures**: Using consistent data structures across the application to handle similar types of data.
- **Interfaces**: Designing interfaces in a uniform manner to ensure they are predictable and easy to use.

## Benefits of Consistency

1. **Maintainability**: Consistent code is easier to maintain because it follows a predictable pattern.
2. **Understandability**: New developers can understand consistent code more quickly.
3. **Extendability**: Consistent code is easier to extend and modify because the structure and conventions are predictable.

## Example

### Inconsistent Code Example

```javascript
// inconsistent naming conventions and structure
function calc_areaCircle(r) {
    return 3.14 * r * r;
}

function CalculateRectangleArea(width, height) {
    return width * height;
}

class sqr {
    constructor(side) {
        this.side = side;
    }
    Area() {
        return this.side * this.side;
    }
}

// consistent naming conventions and structure
function calculateCircleArea(radius) {
    return Math.PI * radius * radius;
}

function calculateRectangleArea(width, height) {
    return width * height;
}

class Square {
    constructor(side) {
        this.side = side;
    }
    calculateArea() {
        return this.side * this.side;
    }
}

