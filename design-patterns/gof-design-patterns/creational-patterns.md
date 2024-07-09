# Creational Patterns

Creational design patterns deal with object creation mechanisms, aiming to create objects in a manner suitable for the situation. They help make the system independent of how its objects are created, composed, and represented. Here are the key creational patterns from the Gang of Four:

1. **Singleton**

**Intent**: Ensures a class has only one instance and provides a global point of access to it.

**Example in TypeScript**:

```typescript
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }

  public sayHello(): void {
    console.log("Hello from Singleton");
  }
}

// Usage
const singleton1 = Singleton.getInstance();
const singleton2 = Singleton.getInstance();

console.log(singleton1 === singleton2); // Output: true

singleton1.sayHello(); // Output: Hello from Singleton
```

2. **Factory Method**

**Intent**: Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created.

**Example in TypeScript**:

```typescript
interface Product {
  operation(): string;
}

class ConcreteProductA implements Product {
  public operation(): string {
    return "ConcreteProductA";
  }
}

class ConcreteProductB implements Product {
  public operation(): string {
    return "ConcreteProductB";
  }
}

abstract class Creator {
  public abstract factoryMethod(): Product;

  public someOperation(): string {
    const product = this.factoryMethod();
    return `Creator: The same creator's code has just worked with ${product.operation()}`;
  }
}

class ConcreteCreatorA extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProductA();
  }
}

class ConcreteCreatorB extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProductB();
  }
}

// Usage
const creatorA = new ConcreteCreatorA();
console.log(creatorA.someOperation());

const creatorB = new ConcreteCreatorB();
console.log(creatorB.someOperation());
```

3. **Abstract Factory**

**Intent**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Example in TypeScript**:

```typescript
interface AbstractFactory {
  createProductA(): AbstractProductA;
  createProductB(): AbstractProductB;
}

class ConcreteFactory1 implements AbstractFactory {
  public createProductA(): AbstractProductA {
    return new ConcreteProductA1();
  }

  public createProductB(): AbstractProductB {
    return new ConcreteProductB1();
  }
}

class ConcreteFactory2 implements AbstractFactory {
  public createProductA(): AbstractProductA {
    return new ConcreteProductA2();
  }

  public createProductB(): AbstractProductB {
    return new ConcreteProductB2();
  }
}

interface AbstractProductA {
  usefulFunctionA(): string;
}

class ConcreteProductA1 implements AbstractProductA {
  public usefulFunctionA(): string {
    return "The result of the product A1.";
  }
}

class ConcreteProductA2 implements AbstractProductA {
  public usefulFunctionA(): string {
    return "The result of the product A2.";
  }
}

interface AbstractProductB {
  usefulFunctionB(): string;
}

class ConcreteProductB1 implements AbstractProductB {
  public usefulFunctionB(): string {
    return "The result of the product B1.";
  }
}

class ConcreteProductB2 implements AbstractProductB {
  public usefulFunctionB(): string {
    return "The result of the product B2.";
  }
}

// Usage
const factory1 = new ConcreteFactory1();
const productA1 = factory1.createProductA();
const productB1 = factory1.createProductB();

console.log(productA1.usefulFunctionA());
console.log(productB1.usefulFunctionB());

const factory2 = new ConcreteFactory2();
const productA2 = factory2.createProductA();
const productB2 = factory2.createProductB();

console.log(productA2.usefulFunctionA());
console.log(productB2.usefulFunctionB());
```

4. **Builder**

**Intent**: Separates the construction of a complex object from its representation so that the same construction process can create different representations.

**Example in TypeScript**:

```typescript
class Product {
  public parts: string[] = [];

  public listParts(): void {
    console.log(`Product parts: ${this.parts.join(", ")}`);
  }
}

interface Builder {
  buildPartA(): void;
  buildPartB(): void;
  buildPartC(): void;
}

class ConcreteBuilder implements Builder {
  private product: Product;

  constructor() {
    this.reset();
  }

  public reset(): void {
    this.product = new Product();
  }

  public buildPartA(): void {
    this.product.parts.push("PartA");
  }

  public buildPartB(): void {
    this.product.parts.push("PartB");
  }

  public buildPartC(): void {
    this.product.parts.push("PartC");
  }

  public getProduct(): Product {
    const result = this.product;
    this.reset();
    return result;
  }
}

class Director {
  private builder: Builder;

  public setBuilder(builder: Builder): void {
    this.builder = builder;
  }

  public buildMinimalViableProduct(): void {
    this.builder.buildPartA();
  }

  public buildFullFeaturedProduct(): void {
    this.builder.buildPartA();
    this.builder.buildPartB();
    this.builder.buildPartC();
  }
}

// Usage
const director = new Director();
const builder = new ConcreteBuilder();
director.setBuilder(builder);

console.log("Standard basic product:");
director.buildMinimalViableProduct();
builder.getProduct().listParts();

console.log("Standard full-featured product:");
director.buildFullFeaturedProduct();
builder.getProduct().listParts();

console.log("Custom product:");
builder.buildPartA();
builder.buildPartC();
builder.getProduct().listParts();
```

5. **Prototype**

**Intent**: Specifies the kinds of objects to create using a prototypical instance and creates new objects by copying this prototype.

**Example in TypeScript**:

```typescript
class Prototype {
  public primitive: any;
  public component: object;
  public circularReference: ComponentWithBackReference;

  public clone(): this {
    const clone = Object.create(this);

    clone.component = Object.create(this.component);

    clone.circularReference = {
      ...this.circularReference,
      prototype: { ...this },
    };

    return clone;
  }
}

class ComponentWithBackReference {
  public prototype;

  constructor(prototype: Prototype) {
    this.prototype = prototype;
  }
}

// Usage
const p1 = new Prototype();
p1.primitive = 245;
p1.component = new Date();
p1.circularReference = new ComponentWithBackReference(p1);

const p2 = p1.clone();

console.log(p1.primitive === p2.primitive); // true
console.log(p1.component === p2.component); // false
console.log(p1.circularReference === p2.circularReference); // false
console.log(p1.circularReference.prototype === p2.circularReference.prototype); // false
```

# Summary

Creational patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code. Each pattern addresses different issues related to object creation, allowing developers to choose the one that best fits their specific needs. Feel free to ask for more details or examples on any of these patterns!
