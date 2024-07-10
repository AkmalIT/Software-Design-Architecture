# Posa

POSA (Pattern-Oriented Software Architecture) patterns are a collection of design patterns that focus on software architecture. These patterns were documented in the four-volume "Pattern-Oriented Software Architecture" book series by Frank Buschmann, Regine Meunier, Hans Rohnert, Peter Sommerlad, and Michael Stal. The patterns in POSA are categorized into different groups based on their architectural significance and usage.

# Key POSA Patterns

1. **Layers**

**Intent**: Structure an application into groups of subtasks in which each group of subtasks is at a particular level of abstraction.

**Example**:

- Presentation Layer (UI)
- Application Layer (Business Logic)
- Data Access Layer (Database interaction)

2. **Pipes and Filters**

**Intent**: Break down a task into a sequence of processing steps (filters) connected by channels (pipes).

**Example**:

- Unix shell commands connected with pipes (e.g., cat file | grep keyword | sort)

3. **Broker**

**Intent**: Structure distributed software systems with decoupled components that interact by remote service invocations.

**Example**:

- Middleware systems such as CORBA, DCOM, or Java RMI

4. **Model-View-Controller (MVC)**

**Intent**: Decouple the way information is presented to the user from the way it is manipulated and stored.

**Example**:

- Web applications where the model represents the data, the view displays the data, and the controller handles user input.

5. **Microkernel (Plugin)**

**Intent**: Adapt a system to changing requirements by separating a minimal functional core from extended functionality and customer-specific parts.

**Example**:

- Eclipse IDE with its core platform and various plugins.

6. **Blackboard**

**Intent**: Solve complex problems that can be decomposed into independent subtasks with a common repository (blackboard) for sharing partial solutions.

**Example**:

- Speech recognition systems, where different modules (e.g., phoneme recognizers, grammar analyzers) work on a shared blackboard to refine their results.

7. **Event-Bus**

**Intent**: Decouple event producers from event consumers to enable highly scalable and dynamic applications.

**Example**:

- Event-driven architectures in systems like Node.js or event-stream processing systems.

8. **Publisher-Subscriber**

**Intent**: Allow multiple subscribers to listen to events from a publisher without them knowing about each other.

**Example**:

- News distribution systems where articles are published to subscribers.

# POSA Examples in TypeScript

**Layers Pattern Example**

```typescript
class DataAccessLayer {
  public getData(): string {
    return "Data from database";
  }
}

class BusinessLogicLayer {
  private dal: DataAccessLayer;

  constructor(dal: DataAccessLayer) {
    this.dal = dal;
  }

  public processData(): string {
    const data = this.dal.getData();
    return `Processed ${data}`;
  }
}

class PresentationLayer {
  private bll: BusinessLogicLayer;

  constructor(bll: BusinessLogicLayer) {
    this.bll = bll;
  }

  public render(): void {
    const result = this.bll.processData();
    console.log(`Rendering: ${result}`);
  }
}

// Usage
const dal = new DataAccessLayer();
const bll = new BusinessLogicLayer(dal);
const pl = new PresentationLayer(bll);
pl.render();
// Output: Rendering: Processed Data from database
```

**Pipes and Filters Pattern Example**

```typescript
class Pipe {
  private filters: ((data: string) => string)[] = [];

  public addFilter(filter: (data: string) => string): void {
    this.filters.push(filter);
  }

  public process(data: string): string {
    return this.filters.reduce((acc, filter) => filter(acc), data);
  }
}

// Filters
const toUpperCase = (data: string) => data.toUpperCase();
const removeSpaces = (data: string) => data.replace(/\s+/g, "");

// Usage
const pipe = new Pipe();
pipe.addFilter(toUpperCase);
pipe.addFilter(removeSpaces);

const result = pipe.process("Hello World");
console.log(result); // Output: HELLOWORLD
```

**Broker Pattern Example**

```typescript
interface Service {
  execute(): string;
}

class ConcreteService1 implements Service {
  public execute(): string {
    return "Service1 execution";
  }
}

class ConcreteService2 implements Service {
  public execute(): string {
    return "Service2 execution";
  }
}

class Broker {
  private services: { [key: string]: Service } = {};

  public registerService(name: string, service: Service): void {
    this.services[name] = service;
  }

  public callService(name: string): string {
    const service = this.services[name];
    if (service) {
      return service.execute();
    }
    return `Service ${name} not found`;
  }
}

// Usage
const broker = new Broker();
broker.registerService("service1", new ConcreteService1());
broker.registerService("service2", new ConcreteService2());

console.log(broker.callService("service1")); // Output: Service1 execution
console.log(broker.callService("service2")); // Output: Service2 execution
```

**Publisher-Subscriber Pattern Example**

```typescript
class Publisher {
  private subscribers: ((message: string) => void)[] = [];

  public subscribe(subscriber: (message: string) => void): void {
    this.subscribers.push(subscriber);
  }

  public publish(message: string): void {
    this.subscribers.forEach((sub) => sub(message));
  }
}

// Usage
const publisher = new Publisher();

const subscriber1 = (message: string) =>
  console.log(`Subscriber1 received: ${message}`);
const subscriber2 = (message: string) =>
  console.log(`Subscriber2 received: ${message}`);

publisher.subscribe(subscriber1);
publisher.subscribe(subscriber2);

publisher.publish("Hello, Subscribers!");
// Output:
// Subscriber1 received: Hello, Subscribers!
// Subscriber2 received: Hello, Subscribers!
```
