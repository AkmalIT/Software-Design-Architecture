# Behavioral Patterns

Behavioral design patterns are concerned with algorithms and the assignment of responsibilities between objects. These patterns describe not just the patterns of objects or classes but also the way they communicate and interact.

Here are the key behavioral patterns from the Gang of Four:

1. **Chain of Responsibility**

**Intent**: Passes a request along a chain of handlers. Each handler either processes the request or passes it to the next handler in the chain.

**Example in TypeScript**:

```typescript
abstract class Handler {
  private nextHandler: Handler | null = null;

  public setNext(handler: Handler): Handler {
    this.nextHandler = handler;
    return handler;
  }

  public handle(request: string): string | null {
    if (this.nextHandler) {
      return this.nextHandler.handle(request);
    }
    return null;
  }
}

class ConcreteHandler1 extends Handler {
  public handle(request: string): string | null {
    if (request === "Request1") {
      return `ConcreteHandler1 handled ${request}`;
    }
    return super.handle(request);
  }
}

class ConcreteHandler2 extends Handler {
  public handle(request: string): string | null {
    if (request === "Request2") {
      return `ConcreteHandler2 handled ${request}`;
    }
    return super.handle(request);
  }
}

// Usage
const handler1 = new ConcreteHandler1();
const handler2 = new ConcreteHandler2();
handler1.setNext(handler2);

console.log(handler1.handle("Request1")); // Output: ConcreteHandler1 handled Request1
console.log(handler1.handle("Request2")); // Output: ConcreteHandler2 handled Request2
console.log(handler1.handle("UnknownRequest")); // Output: null
```

2. **Command**

**Intent**: Encapsulates a request as an object, thereby allowing users to parameterize clients with different requests, queue or log requests, and support undoable operations.

**Example in TypeScript**:

```typescript
interface Command {
  execute(): void;
}

class Receiver {
  public doSomething(message: string): void {
    console.log(`Receiver: ${message}`);
  }
}

class ConcreteCommand implements Command {
  private receiver: Receiver;
  private message: string;

  constructor(receiver: Receiver, message: string) {
    this.receiver = receiver;
    this.message = message;
  }

  public execute(): void {
    this.receiver.doSomething(this.message);
  }
}

class Invoker {
  private commands: Command[] = [];

  public addCommand(command: Command): void {
    this.commands.push(command);
  }

  public executeCommands(): void {
    for (const command of this.commands) {
      command.execute();
    }
  }
}

// Usage
const receiver = new Receiver();
const command1 = new ConcreteCommand(receiver, "Task 1");
const command2 = new ConcreteCommand(receiver, "Task 2");

const invoker = new Invoker();
invoker.addCommand(command1);
invoker.addCommand(command2);
invoker.executeCommands();
// Output:
// Receiver: Task 1
// Receiver: Task 2
```

3. **Iterator**

**Intent**: Provides a way to access elements of an aggregate object sequentially without exposing its underlying representation.

**Example in TypeScript**:

```typescript
interface Iterator<T> {
  current(): T;
  next(): T;
  hasNext(): boolean;
}

class ConcreteIterator<T> implements Iterator<T> {
  private collection: T[];
  private position: number = 0;

  constructor(collection: T[]) {
    this.collection = collection;
  }

  public current(): T {
    return this.collection[this.position];
  }

  public next(): T {
    const item = this.collection[this.position];
    this.position += 1;
    return item;
  }

  public hasNext(): boolean {
    return this.position < this.collection.length;
  }
}

// Usage
const collection = [1, 2, 3, 4];
const iterator = new ConcreteIterator<number>(collection);

while (iterator.hasNext()) {
  console.log(iterator.next()); // Output: 1, 2, 3, 4
}
```

4. **Mediator**

**Intent**: Defines an object that encapsulates how a set of objects interact, promoting loose coupling by preventing objects from referring to each other explicitly.

**Example in TypeScript**:

```typescript
interface Mediator {
  notify(sender: object, event: string): void;
}

class ConcreteMediator implements Mediator {
  private component1: Component1;
  private component2: Component2;

  constructor(c1: Component1, c2: Component2) {
    this.component1 = c1;
    this.component1.setMediator(this);
    this.component2 = c2;
    this.component2.setMediator(this);
  }

  public notify(sender: object, event: string): void {
    if (event === "A") {
      console.log("Mediator reacts on A and triggers following operations:");
      this.component2.doC();
    }
    if (event === "D") {
      console.log("Mediator reacts on D and triggers following operations:");
      this.component1.doB();
      this.component2.doC();
    }
  }
}

class BaseComponent {
  protected mediator: Mediator;

  constructor(mediator?: Mediator) {
    this.mediator = mediator!;
  }

  public setMediator(mediator: Mediator): void {
    this.mediator = mediator;
  }
}

class Component1 extends BaseComponent {
  public doA(): void {
    console.log("Component 1 does A.");
    this.mediator.notify(this, "A");
  }

  public doB(): void {
    console.log("Component 1 does B.");
    this.mediator.notify(this, "B");
  }
}

class Component2 extends BaseComponent {
  public doC(): void {
    console.log("Component 2 does C.");
    this.mediator.notify(this, "C");
  }

  public doD(): void {
    console.log("Component 2 does D.");
    this.mediator.notify(this, "D");
  }
}

// Usage
const c1 = new Component1();
const c2 = new Component2();
const mediator = new ConcreteMediator(c1, c2);

c1.doA();
// Output:
// Component 1 does A.
// Mediator reacts on A and triggers following operations:
// Component 2 does C.

c2.doD();
// Output:
// Component 2 does D.
// Mediator reacts on D and triggers following operations:
// Component 1 does B.
// Component 2 does C.
```

5. **Memento**

**Intent**: Captures and externalizes an object's internal state so that the object can be restored to this state later without violating encapsulation.

**Example in TypeScript**:

```typescript
class Memento {
  private state: string;

  constructor(state: string) {
    this.state = state;
  }

  public getState(): string {
    return this.state;
  }
}

class Originator {
  private state: string;

  public setState(state: string): void {
    console.log(`Originator: Setting state to ${state}`);
    this.state = state;
  }

  public save(): Memento {
    console.log("Originator: Saving to Memento.");
    return new Memento(this.state);
  }

  public restore(memento: Memento): void {
    this.state = memento.getState();
    console.log(
      `Originator: State after restoring from Memento: ${this.state}`
    );
  }
}

class Caretaker {
  private mementos: Memento[] = [];
  private originator: Originator;

  constructor(originator: Originator) {
    this.originator = originator;
  }

  public backup(): void {
    console.log("Caretaker: Saving Originator's state...");
    this.mementos.push(this.originator.save());
  }

  public undo(): void {
    if (!this.mementos.length) {
      return;
    }
    const memento = this.mementos.pop()!;
    console.log("Caretaker: Restoring state to:", memento.getState());
    this.originator.restore(memento);
  }
}

// Usage
const originator = new Originator();
const caretaker = new Caretaker(originator);

originator.setState("State1");
caretaker.backup();

originator.setState("State2");
caretaker.backup();

originator.setState("State3");

caretaker.undo();
// Output:
// Caretaker: Restoring state to: State2
// Originator: State after restoring from Memento: State2

caretaker.undo();
// Output:
// Caretaker: Restoring state to: State1
// Originator: State after restoring from Memento: State1
```

6. **Observer**

**Intent**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Example in TypeScript**:

```typescript
interface Observer {
  update(subject: Subject): void;
}

class Subject {
  private observers: Observer[] = [];
  private state: number;

  public attach(observer: Observer): void {
    const isExist = this.observers.includes(observer);
    if (isExist) {
      return console.log("Subject: Observer has been attached already.");
    }
    this.observers.push(observer);
    console.log("Subject: Attached an observer.");
  }

  public detach(observer: Observer): void {
    const observerIndex = this.observers.indexOf(observer);
    if (observerIndex === -1) {
      return console.log("Subject: Nonexistent observer.");
    }
    this.observers.splice(observerIndex, 1);
    console.log("Subject: Detached an observer.");
  }

  public notify(): void {
    console.log("Subject: Notifying observers...");
    for (const observer of this.observers) {
      observer.update(this);
    }
  }

  public someBusinessLogic(): void {
    console.log("Subject: I'm doing something important.");
    this.state = Math.floor(Math.random() * 10 + 1);
    console.log(`Subject: My state has just changed to: ${this.state}`);
    this.notify();
  }

  public getState(): number {
    return this.state;
  }
}

class ConcreteObserverA implements Observer {
  public update(subject: Subject): void {
    if (subject.getState() < 5) {
      console.log("ConcreteObserverA: Reacted to the event.");
    }
  }
}

class ConcreteObserverB implements Observer {
  public update(subject: Subject): void {
    if (subject.getState() === 0 || subject.getState() >= 5) {
      console.log("ConcreteObserverB: Reacted to the event.");
    }
  }
}

// Usage
const subject = new Subject();

const observer1 = new ConcreteObserverA();
subject.attach(observer1);

const observer2 = new ConcreteObserverB();
subject.attach(observer2);

subject.someBusinessLogic();
// Output:
// Subject: I'm doing something important.
// Subject: My state has just changed to: 4
// Subject: Notifying observers...
// ConcreteObserverA: Reacted to the event.

subject.someBusinessLogic();
// Output:
// Subject: I'm doing something important.
// Subject: My state has just changed to: 8
// Subject: Notifying observers...
// ConcreteObserverB: Reacted to the event.
```

7. **State**

**Intent**: Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

**Example in TypeScript**:

```typescript
interface State {
  handle(context: Context): void;
}

class Context {
  private state: State;

  constructor(state: State) {
    this.transitionTo(state);
  }

  public transitionTo(state: State): void {
    console.log(`Context: Transition to ${(<any>state).constructor.name}.`);
    this.state = state;
    this.state.handle(this);
  }

  public request(): void {
    this.state.handle(this);
  }
}

class ConcreteStateA implements State {
  public handle(context: Context): void {
    console.log("ConcreteStateA handles request.");
    context.transitionTo(new ConcreteStateB());
  }
}

class ConcreteStateB implements State {
  public handle(context: Context): void {
    console.log("ConcreteStateB handles request.");
    context.transitionTo(new ConcreteStateA());
  }
}

// Usage
const context = new Context(new ConcreteStateA());
context.request();
// Output:
// Context: Transition to ConcreteStateA.
// ConcreteStateA handles request.
// Context: Transition to ConcreteStateB.

context.request();
// Output:
// ConcreteStateB handles request.
// Context: Transition to ConcreteStateA.
```

8. **Strategy**

**Intent**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

**Example in TypeScript**:

```typescript
interface Strategy {
  execute(a: number, b: number): number;
}

class ConcreteStrategyAdd implements Strategy {
  public execute(a: number, b: number): number {
    return a + b;
  }
}

class ConcreteStrategySubtract implements Strategy {
  public execute(a: number, b: number): number {
    return a - b;
  }
}

class ConcreteStrategyMultiply implements Strategy {
  public execute(a: number, b: number): number {
    return a * b;
  }
}

class Context {
  private strategy: Strategy;

  constructor(strategy: Strategy) {
    this.strategy = strategy;
  }

  public setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  public executeStrategy(a: number, b: number): number {
    return this.strategy.execute(a, b);
  }
}

// Usage
const context = new Context(new ConcreteStrategyAdd());
console.log("Addition:", context.executeStrategy(5, 3)); // Output: Addition: 8

context.setStrategy(new ConcreteStrategySubtract());
console.log("Subtraction:", context.executeStrategy(5, 3)); // Output: Subtraction: 2

context.setStrategy(new ConcreteStrategyMultiply());
console.log("Multiplication:", context.executeStrategy(5, 3)); // Output: Multiplication: 15
```

9. **Template Method**

**Intent**: Defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.

**Example in TypeScript**:

```typescript
abstract class AbstractClass {
  public templateMethod(): void {
    this.baseOperation1();
    this.requiredOperation1();
    this.baseOperation2();
    this.requiredOperation2();
    this.hook1();
    this.baseOperation3();
    this.hook2();
  }

  protected baseOperation1(): void {
    console.log("AbstractClass says: I am doing the bulk of the work");
  }

  protected baseOperation2(): void {
    console.log(
      "AbstractClass says: But I let subclasses override some operations"
    );
  }

  protected baseOperation3(): void {
    console.log(
      "AbstractClass says: But I am doing the bulk of the work anyway"
    );
  }

  protected abstract requiredOperation1(): void;
  protected abstract requiredOperation2(): void;

  protected hook1(): void {}
  protected hook2(): void {}
}

class ConcreteClass1 extends AbstractClass {
  protected requiredOperation1(): void {
    console.log("ConcreteClass1 says: Implemented Operation1");
  }

  protected requiredOperation2(): void {
    console.log("ConcreteClass1 says: Implemented Operation2");
  }
}

class ConcreteClass2 extends AbstractClass {
  protected requiredOperation1(): void {
    console.log("ConcreteClass2 says: Implemented Operation1");
  }

  protected requiredOperation2(): void {
    console.log("ConcreteClass2 says: Implemented Operation2");
  }

  protected hook1(): void {
    console.log("ConcreteClass2 says: Overridden Hook1");
  }
}

// Usage
console.log("Same client code can work with different subclasses:");
const concreteClass1 = new ConcreteClass1();
concreteClass1.templateMethod();
// Output:
// AbstractClass says: I am doing the bulk of the work
// ConcreteClass1 says: Implemented Operation1
// AbstractClass says: But I let subclasses override some operations
// ConcreteClass1 says: Implemented Operation2
// AbstractClass says: But I am doing the bulk of the work anyway

console.log("");

console.log("Same client code can work with different subclasses:");
const concreteClass2 = new ConcreteClass2();
concreteClass2.templateMethod();
// Output:
// AbstractClass says: I am doing the bulk of the work
// ConcreteClass2 says: Implemented Operation1
// AbstractClass says: But I let subclasses override some operations
// ConcreteClass2 says: Implemented Operation2
// ConcreteClass2 says: Overridden Hook1
// AbstractClass says: But I am doing the bulk of the work anyway
```

10. **Visitor**

**Intent**: Lets you define a new operation without changing the classes of the elements on which it operates.

**Example in TypeScript**:

```typescript
interface Visitor {
  visitConcreteComponentA(element: ConcreteComponentA): void;
  visitConcreteComponentB(element: ConcreteComponentB): void;
}

interface Component {
  accept(visitor: Visitor): void;
}

class ConcreteComponentA implements Component {
  public accept(visitor: Visitor): void {
    visitor.visitConcreteComponentA(this);
  }

  public exclusiveMethodOfConcreteComponentA(): string {
    return "A";
  }
}

class ConcreteComponentB implements Component {
  public accept(visitor: Visitor): void {
    visitor.visitConcreteComponentB(this);
  }

  public specialMethodOfConcreteComponentB(): string {
    return "B";
  }
}

class ConcreteVisitor1 implements Visitor {
  public visitConcreteComponentA(element: ConcreteComponentA): void {
    console.log(
      `${element.exclusiveMethodOfConcreteComponentA()} + ConcreteVisitor1`
    );
  }

  public visitConcreteComponentB(element: ConcreteComponentB): void {
    console.log(
      `${element.specialMethodOfConcreteComponentB()} + ConcreteVisitor1`
    );
  }
}

class ConcreteVisitor2 implements Visitor {
  public visitConcreteComponentA(element: ConcreteComponentA): void {
    console.log(
      `${element.exclusiveMethodOfConcreteComponentA()} + ConcreteVisitor2`
    );
  }

  public visitConcreteComponentB(element: ConcreteComponentB): void {
    console.log(
      `${element.specialMethodOfConcreteComponentB()} + ConcreteVisitor2`
    );
  }
}

// Usage
const components: Component[] = [
  new ConcreteComponentA(),
  new ConcreteComponentB(),
];

const visitor1 = new ConcreteVisitor1();
const visitor2 = new ConcreteVisitor2();

console.log(
  "Client code works with all visitors via the base Visitor interface:"
);
for (const component of components) {
  component.accept(visitor1);
  component.accept(visitor2);
}
// Output:
// A + ConcreteVisitor1
// B + ConcreteVisitor1
// A + ConcreteVisitor2
// B + ConcreteVisitor2
```

# Summary

Behavioral patterns focus on how objects interact and communicate with each other, ensuring that systems are flexible and efficient. They help manage complex control flows, delegation, and distribution of responsibilities, making the system more robust and maintainable. Let me know if you need more examples or explanations on any of these patterns!
