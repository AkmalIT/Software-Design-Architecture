# Structural Patterns

Structural design patterns deal with object composition and the relationships between entities. They help ensure that if one part of a system changes, the entire system does not need to change. These patterns simplify the structure by identifying the relationships.

Here are the key structural patterns from the Gang of Four:

1. **Adapter**

**Intent**: Allows incompatible interfaces to work together by wrapping an existing class with a new interface.

**Example in TypeScript**:

```typescript
// Existing interface
class Adaptee {
  public specificRequest(): string {
    return "Adaptee specific request";
  }
}

// New interface
interface Target {
  request(): string;
}

// Adapter class
class Adapter implements Target {
  private adaptee: Adaptee;

  constructor(adaptee: Adaptee) {
    this.adaptee = adaptee;
  }

  public request(): string {
    return `Adapter: ${this.adaptee.specificRequest()}`;
  }
}

// Usage
const adaptee = new Adaptee();
const adapter = new Adapter(adaptee);
console.log(adapter.request()); // Output: Adapter: Adaptee specific request
```

2. **Bridge**

**Intent**: Decouples an abstraction from its implementation so that the two can vary independently.

**Example in TypeScript**:

```typescript
// Abstraction
class Abstraction {
  protected implementation: Implementation;

  constructor(implementation: Implementation) {
    this.implementation = implementation;
  }

  public operation(): string {
    return `Abstraction: Base operation with: ${this.implementation.operationImplementation()}`;
  }
}

// Implementation interface
interface Implementation {
  operationImplementation(): string;
}

// Concrete Implementations
class ConcreteImplementationA implements Implementation {
  public operationImplementation(): string {
    return "ConcreteImplementationA";
  }
}

class ConcreteImplementationB implements Implementation {
  public operationImplementation(): string {
    return "ConcreteImplementationB";
  }
}

// Extended Abstraction
class ExtendedAbstraction extends Abstraction {
  public operation(): string {
    return `ExtendedAbstraction: Extended operation with: ${this.implementation.operationImplementation()}`;
  }
}

// Usage
const implementationA = new ConcreteImplementationA();
const implementationB = new ConcreteImplementationB();

const abstraction = new Abstraction(implementationA);
console.log(abstraction.operation()); // Output: Abstraction: Base operation with: ConcreteImplementationA

const extendedAbstraction = new ExtendedAbstraction(implementationB);
console.log(extendedAbstraction.operation()); // Output: ExtendedAbstraction: Extended operation with: ConcreteImplementationB
```

3. **Composite**

**Intent**: Composes objects into tree structures to represent part-whole hierarchies, allowing individual objects and compositions of objects to be treated uniformly.

**Example in TypeScript**:

```typescript
// Component
abstract class Component {
  protected parent: Component | null = null;

  public setParent(parent: Component | null) {
    this.parent = parent;
  }

  public getParent(): Component | null {
    return this.parent;
  }

  public add(component: Component): void {}

  public remove(component: Component): void {}

  public isComposite(): boolean {
    return false;
  }

  public abstract operation(): string;
}

// Leaf
class Leaf extends Component {
  public operation(): string {
    return "Leaf";
  }
}

// Composite
class Composite extends Component {
  protected children: Component[] = [];

  public add(component: Component): void {
    this.children.push(component);
    component.setParent(this);
  }

  public remove(component: Component): void {
    const componentIndex = this.children.indexOf(component);
    this.children.splice(componentIndex, 1);
    component.setParent(null);
  }

  public isComposite(): boolean {
    return true;
  }

  public operation(): string {
    const results = [];
    for (const child of this.children) {
      results.push(child.operation());
    }
    return `Branch(${results.join("+")})`;
  }
}

// Usage
const tree = new Composite();
const branch1 = new Composite();
branch1.add(new Leaf());
branch1.add(new Leaf());

const branch2 = new Composite();
branch2.add(new Leaf());

tree.add(branch1);
tree.add(branch2);

console.log(tree.operation()); // Output: Branch(Branch(Leaf+Leaf)+Branch(Leaf))
```

4. **Decorator**

**Intent**: Adds additional functionality to an object dynamically.

**Example in TypeScript**:

```typescript
// Component
interface Component {
  operation(): string;
}

// Concrete Component
class ConcreteComponent implements Component {
  public operation(): string {
    return "ConcreteComponent";
  }
}

// Base Decorator
class Decorator implements Component {
  protected component: Component;

  constructor(component: Component) {
    this.component = component;
  }

  public operation(): string {
    return this.component.operation();
  }
}

// Concrete Decorators
class ConcreteDecoratorA extends Decorator {
  public operation(): string {
    return `ConcreteDecoratorA(${super.operation()})`;
  }
}

class ConcreteDecoratorB extends Decorator {
  public operation(): string {
    return `ConcreteDecoratorB(${super.operation()})`;
  }
}

// Usage
const simple = new ConcreteComponent();
console.log(simple.operation()); // Output: ConcreteComponent

const decoratorA = new ConcreteDecoratorA(simple);
console.log(decoratorA.operation()); // Output: ConcreteDecoratorA(ConcreteComponent)

const decoratorB = new ConcreteDecoratorB(decoratorA);
console.log(decoratorB.operation()); // Output: ConcreteDecoratorB(ConcreteDecoratorA(ConcreteComponent))
```

5. **Facade**

**Intent**: Provides a simplified interface to a complex subsystem.

**Example in TypeScript**:

```typescript
// Complex Subsystem
class Subsystem1 {
  public operation1(): string {
    return "Subsystem1: Ready!";
  }

  public operationN(): string {
    return "Subsystem1: Go!";
  }
}

class Subsystem2 {
  public operation1(): string {
    return "Subsystem2: Get ready!";
  }

  public operationZ(): string {
    return "Subsystem2: Fire!";
  }
}

// Facade
class Facade {
  protected subsystem1: Subsystem1;
  protected subsystem2: Subsystem2;

  constructor(subsystem1: Subsystem1, subsystem2: Subsystem2) {
    this.subsystem1 = subsystem1;
    this.subsystem2 = subsystem2;
  }

  public operation(): string {
    let result = "Facade initializes subsystems:\n";
    result += this.subsystem1.operation1() + "\n";
    result += this.subsystem2.operation1() + "\n";
    result += "Facade orders subsystems to perform the action:\n";
    result += this.subsystem1.operationN() + "\n";
    result += this.subsystem2.operationZ() + "\n";
    return result;
  }
}

// Usage
const subsystem1 = new Subsystem1();
const subsystem2 = new Subsystem2();
const facade = new Facade(subsystem1, subsystem2);
console.log(facade.operation());
```

6. **Flyweight**

**Intent**: Reduces the cost of creating and manipulating a large number of similar objects by sharing common parts of the state between multiple objects.

**Example in TypeScript**:

```typescript
class Flyweight {
  private sharedState: any;

  constructor(sharedState: any) {
    this.sharedState = sharedState;
  }

  public operation(uniqueState: any): void {
    const s = JSON.stringify(this.sharedState);
    const u = JSON.stringify(uniqueState);
    console.log(`Flyweight: Displaying shared (${s}) and unique (${u}) state.`);
  }
}

class FlyweightFactory {
  private flyweights: { [key: string]: Flyweight } = <any>{};

  constructor(initialFlyweights: string[][]) {
    for (const state of initialFlyweights) {
      this.flyweights[this.getKey(state)] = new Flyweight(state);
    }
  }

  private getKey(state: string[]): string {
    return state.join("_");
  }

  public getFlyweight(sharedState: string[]): Flyweight {
    const key = this.getKey(sharedState);

    if (!(key in this.flyweights)) {
      console.log(
        "FlyweightFactory: Can't find a flyweight, creating new one."
      );
      this.flyweights[key] = new Flyweight(sharedState);
    } else {
      console.log("FlyweightFactory: Reusing existing flyweight.");
    }

    return this.flyweights[key];
  }

  public listFlyweights(): void {
    const count = Object.keys(this.flyweights).length;
    console.log(`FlyweightFactory: I have ${count} flyweights:`);
    for (const key in this.flyweights) {
      console.log(key);
    }
  }
}

// Usage
const factory = new FlyweightFactory([
  ["Chevrolet", "Camaro2018", "pink"],
  ["Mercedes Benz", "C300", "black"],
  ["Mercedes Benz", "C500", "red"],
  ["BMW", "M5", "red"],
  ["BMW", "X6", "white"],
]);

factory.listFlyweights();

const addCarToPoliceDatabase = (
  ff: FlyweightFactory,
  plates: string,
  owner: string,
  brand: string,
  model: string,
  color: string
) => {
  console.log("\nClient: Adding a car to database.");
  const flyweight = ff.getFlyweight([brand, model, color]);

  // The client code either stores or calculates extrinsic state and passes it
  // to the flyweight's methods.
  flyweight.operation([plates, owner]);
};

addCarToPoliceDatabase(factory, "CL234IR", "Antony Starr: Homelander", "BMW", "M5", "red");
addCarToPoliceDatabase(factory, "CL234IR", "Karl Urban: Butcher", "BMW", "X1", "red");

factory.listFlyweights();
```

7. **Proxy**

**Intent**: Provides a surrogate or placeholder for another object to control access to it.

**Example in TypeScript**:

```typescript
interface Subject {
  request(): void;
}

class RealSubject implements Subject {
  public request(): void {
    console.log("RealSubject: Handling request.");
  }
}

class Proxy implements Subject {
  private realSubject: RealSubject;

  constructor(realSubject: RealSubject) {
    this.realSubject = realSubject;
  }

  public request(): void {
    if (this.checkAccess()) {
      this.realSubject.request();
      this.logAccess();
    }
  }

  private checkAccess(): boolean {
    console.log("Proxy: Checking access prior to firing a real request.");
    return true;
  }

  private logAccess(): void {
    console.log("Proxy: Logging the time of request.");
  }
}

// Usage
const realSubject = new RealSubject();
const proxy = new Proxy(realSubject);
proxy.request();
```

# Summary

Structural patterns focus on how classes and objects are composed to form larger structures, providing flexibility and efficiency. They help ensure that if one part of a system changes, the entire system does not need to change, making the codebase more maintainable and scalable. Feel free to ask for more details or examples on any of these patterns!
