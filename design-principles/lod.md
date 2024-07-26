# LoD

**Law of Demeter (LoD)**, also known as the "Principle of Least Knowledge," is a design guideline for developing software that promotes loose coupling between components. The Law of Demeter encourages methods to only communicate with their immediate neighbors, reducing dependencies and making the system more maintainable.

# Why is the Law of Demeter Important?

1. **Reduces Coupling**: Minimizes dependencies between classes, leading to a more modular and maintainable system.
2. **Improves Encapsulation**: Promotes better encapsulation by limiting the exposure of internal details.
3. **Enhances Readability**: Makes code more readable and easier to understand by reducing the complexity of interactions.
4. **Simplifies Maintenance**: Easier to maintain and refactor code as changes in one class have minimal impact on others.

# Real-Life Analogy

**Library Books**: Imagine you want to borrow a book from a library. You wouldn't directly ask the book itself where it's located. Instead, you would ask a librarian (the immediate neighbor) who can fetch the book for you. The librarian knows the internal organization of the library, so you don't need to.

# Example of Law of Demeter in Code

**Without the Law of Demeter**

```typescript
class Engine {
  start() {
    console.log("Engine started");
  }
}

class Car {
  engine: Engine;

  constructor() {
    this.engine = new Engine();
  }

  getEngine() {
    return this.engine;
  }
}

class Driver {
  startCar(car: Car) {
    // Directly accessing the engine of the car
    car.getEngine().start();
  }
}

const car = new Car();
const driver = new Driver();
driver.startCar(car);
```

In this example, the Driver class directly accesses the Engine of the Car, which violates the Law of Demeter.

**With the Law of Demeter**

```typescript
class Engine {
  start() {
    console.log("Engine started");
  }
}

class Car {
  private engine: Engine;

  constructor() {
    this.engine = new Engine();
  }

  startEngine() {
    this.engine.start();
  }
}

class Driver {
  startCar(car: Car) {
    // Using Car's method to start the engine, adhering to the Law of Demeter
    car.startEngine();
  }
}

const car = new Car();
const driver = new Driver();
driver.startCar(car);
```

By introducing the startEngine method in the Car class, the Driver no longer directly accesses the Engine, adhering to the Law of Demeter.

# Benefits of Using the Law of Demeter

1. **Modularity**: Promotes modular design by limiting the interaction between different parts of the system.
2. **Encapsulation**: Strengthens encapsulation by keeping internal details hidden.
3. **Maintainability**: Easier to maintain and refactor as changes are localized.
4. **Reduced Complexity**: Reduces the complexity of the code by limiting the number of objects a method interacts with.

# Guidelines for Implementing the Law of Demeter

1. **Limit Method Calls**: A method should only call methods on the following:

- The object itself.
- Objects passed as arguments.
- Objects it creates.
- Directly held component objects.

2. **Encapsulate Internal Objects**: Provide methods that handle interactions with internal objects to prevent external objects from directly accessing them.
3. **Use Facades or Wrappers**: Introduce facades or wrapper classes to simplify interactions between complex subsystems.
