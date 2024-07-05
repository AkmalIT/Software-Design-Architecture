# SOLID

**SOLID** is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable. These principles are:

1. **S**ingle Responsibility Principle (SRP)
2. **O**pen/Closed Principle (OCP)
3. **L**iskov Substitution Principle (LSP)
4. **I**nterface Segregation Principle (ISP)
5. **D**ependency Inversion Principle (DIP)

Let's explore each of these principles in detail with examples in TypeScript.

# Single Responsibility Principle (SRP)

**Definition**: A class should have only one reason to change, meaning it should have only one job or responsibility.

**Why SRP is Important**:

- **Maintains Focus**: Each class has a single responsibility, making it easier to understand.
- **Reduces Complexity**: Simplifies the code by limiting the scope of each class.
- **Enhances Maintainability**: Easier to update and refactor.

**Real-Life Analogy**: Think of a utility knife. While it might have multiple tools, each tool performs a single specific function (e.g., a knife for cutting, a screwdriver for driving screws).

**Example Without SRP**:

```typescript
class User {
  constructor(public username: string, public password: string) {}

  validatePassword(): boolean {
    // Validation logic
    return this.password.length > 6;
  }

  save(): void {
    // Database saving logic
    console.log("User saved to database");
  }
}
```

Example With SRP:

```typescript
class User {
  constructor(public username: string, public password: string) {}
}

class UserValidator {
  static validatePassword(user: User): boolean {
    return user.password.length > 6;
  }
}

class UserRepository {
  static save(user: User): void {
    console.log("User saved to database");
  }
}
```

# Open/Closed Principle (OCP)

**Definition**: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

**Why OCP is Important**:

- **Promotes Extensibility**: New functionality can be added without changing existing code.
- **Enhances Stability**: Reduces the risk of introducing bugs in existing code.

**Real-Life Analogy**: A smartphone operating system allows new apps to be installed without modifying the OS itself.

**Example Without OCP**:

```typescript
class Shape {
  type: string;
  constructor(type: string) {
    this.type = type;
  }
}

class AreaCalculator {
  calculateArea(shape: Shape): number {
    if (shape.type === "circle") {
      // Calculate area of circle
    } else if (shape.type === "rectangle") {
      // Calculate area of rectangle
    }
    return 0;
  }
}
```

**Example With OCP**:

```typescript
interface Shape {
  calculateArea(): number;
}

class Circle implements Shape {
  constructor(private radius: number) {}

  calculateArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

class Rectangle implements Shape {
  constructor(private width: number, private height: number) {}

  calculateArea(): number {
    return this.width * this.height;
  }
}

class AreaCalculator {
  calculateArea(shape: Shape): number {
    return shape.calculateArea();
  }
}
```

# Liskov Substitution Principle (LSP)

**Definition**: Objects of a superclass should be replaceable with objects of a subclass without affecting the functionality.

**Why LSP is Important**:

- **Ensures Correctness**: Subclasses can stand in for their base classes without causing errors.
- **Promotes Reusability**: Subtypes can be reused wherever the base type is expected.

**Real-Life Analogy**: A credit card should be replaceable with a debit card when making a payment without affecting the transaction process.

**Example Without LSP**:

```typescript
class Bird {
  fly(): void {
    console.log("Flying");
  }
}

class Ostrich extends Bird {
  fly(): void {
    throw new Error("Ostriches can't fly");
  }
}
```

**Example With LSP**:

```typescript
class Bird {
  move(): void {
    console.log("Moving");
  }
}

class FlyingBird extends Bird {
  fly(): void {
    console.log("Flying");
  }
}

class Ostrich extends Bird {
  move(): void {
    console.log("Running");
  }
}

class Sparrow extends FlyingBird {}
```

# Interface Segregation Principle (ISP)

**Definition**: Clients should not be forced to depend on interfaces they do not use. Split large interfaces into smaller, more specific ones.

**Why ISP is Important**:

- **Improves Cohesion**: Interfaces are more focused and easier to implement.
- **Enhances Flexibility**: Clients depend only on the methods they need.

**Real-Life Analogy**: A remote control for a TV should not have buttons for functions that the TV does not support.

**Example Without ISP**:

```typescript
interface Worker {
  work(): void;
  eat(): void;
}

class HumanWorker implements Worker {
  work(): void {
    console.log("Human working");
  }

  eat(): void {
    console.log("Human eating");
  }
}

class RobotWorker implements Worker {
  work(): void {
    console.log("Robot working");
  }

  eat(): void {
    throw new Error("Robots don't eat");
  }
}
```

**Example With ISP**:

```typescript
interface Workable {
  work(): void;
}

interface Eatable {
  eat(): void;
}

class HumanWorker implements Workable, Eatable {
  work(): void {
    console.log("Human working");
  }

  eat(): void {
    console.log("Human eating");
  }
}

class RobotWorker implements Workable {
  work(): void {
    console.log("Robot working");
  }
}
```

# Dependency Inversion Principle (DIP)

**Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). Abstractions should not depend on details. Details should depend on abstractions.

**Why DIP is Important**:

- **Enhances Flexibility**: Promotes a design that is more flexible and easier to modify.
- **Improves Testability**: Simplifies unit testing by allowing dependencies to be easily replaced with mocks or stubs.

**Real-Life Analogy**: An electric outlet (high-level module) should not depend on the type of device plugged into it (low-level module). Both depend on a standard plug interface.

**Example Without DIP**:

```typescript
class LightBulb {
  turnOn(): void {
    console.log("Light bulb turned on");
  }
}

class Switch {
  private bulb: LightBulb;

  constructor(bulb: LightBulb) {
    this.bulb = bulb;
  }

  operate(): void {
    this.bulb.turnOn();
  }
}

const bulb = new LightBulb();
const switchInstance = new Switch(bulb);
switchInstance.operate();
```

**Example With DIP**:

```typescript
interface Switchable {
  turnOn(): void;
}

class LightBulb implements Switchable {
  turnOn(): void {
    console.log("Light bulb turned on");
  }
}

class Fan implements Switchable {
  turnOn(): void {
    console.log("Fan turned on");
  }
}

class Switch {
  private device: Switchable;

  constructor(device: Switchable) {
    this.device = device;
  }

  operate(): void {
    this.device.turnOn();
  }
}

const bulb = new LightBulb();
const fan = new Fan();

const bulbSwitch = new Switch(bulb);
bulbSwitch.operate();

const fanSwitch = new Switch(fan);
fanSwitch.operate();
```

# Summary

- **Single Responsibility Principle (SRP)**: A class should have one and only one reason to change.
- **Open/Closed Principle (OCP)**: Classes should be open for extension but closed for modification.
- **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types.
- **Interface Segregation Principle (ISP)**: No client should be forced to depend on methods it does not use.
- **Dependency Inversion Principle (DIP)**: Depend on abstractions, not on concretions.
