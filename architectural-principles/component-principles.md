# Component Principles

Component principles are guidelines and best practices for designing, implementing, and managing software components in a way that ensures modularity, reusability, and maintainability. These principles are crucial in component-based software engineering, where systems are built by assembling reusable and independent components.

# Key Component Principles

1. **Reusability**

**Intent**: Design components that can be used in different systems or in various parts of the same system without modification.

**Example**: A user authentication component that can be used in multiple applications.

2. **Replaceability**

**Intent**: Ensure that components can be replaced with others without affecting the system as a whole, provided they adhere to the same interface.

**Example**: Replacing a logging component with another that has a different implementation but the same interface.

3. **Extensibility**

**Intent**: Design components to be extendable, allowing new functionality to be added without modifying existing code.

**Example**: A reporting component that allows for new report types to be added via plugins.

4. **Encapsulation**

**Intent**: Hide the internal details of a component and expose only what is necessary through well-defined interfaces.

**Example**: A database access component that exposes methods for querying data but hides the underlying database connection details.

5. **Cohesion**

**Intent**: Ensure that a component is focused on a single task or related tasks, leading to higher maintainability and understanding.

**Example**: A component dedicated solely to handling payment processing.

6. **Coupling**

**Intent**: Minimize dependencies between components to enhance modularity and ease of maintenance.

**Example**: Using interfaces or dependency injection to reduce direct dependencies between components.

# Component Principles Examples in TypeScript

**Reusability Example**

```typescript
class AuthComponent {
  public login(username: string, password: string): boolean {
    // Logic for authenticating the user
    return username === "user" && password === "pass";
  }
}

// Usage in different parts of the application
const auth = new AuthComponent();
console.log(auth.login("user", "pass")); // Output: true
```

**Replaceability Example**

```typescript
interface Logger {
  log(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log(message);
  }
}

class FileLogger implements Logger {
  log(message: string): void {
    // Logic to log message to a file
  }
}

// Usage
const logger: Logger = new ConsoleLogger();
logger.log("This is a log message.");
```

**Extensibility Example**

```typescript
interface Report {
  generate(): string;
}

class SalesReport implements Report {
  generate(): string {
    return "Sales Report Data";
  }
}

class ReportManager {
  private reports: Report[] = [];

  addReport(report: Report): void {
    this.reports.push(report);
  }

  generateAllReports(): void {
    this.reports.forEach((report) => console.log(report.generate()));
  }
}

// Usage
const reportManager = new ReportManager();
reportManager.addReport(new SalesReport());
reportManager.generateAllReports();
// Output: Sales Report Data
```

**Encapsulation Example**

```typescript
class DatabaseComponent {
  private connection: any; // Imagine this is the database connection

  constructor() {
    this.connection = this.connect();
  }

  private connect(): any {
    // Logic to establish a database connection
    return {};
  }

  public query(sql: string): any {
    // Logic to execute a query
    return {};
  }
}

// Usage
const db = new DatabaseComponent();
const result = db.query("SELECT * FROM users");
```

**Cohesion Example**

```typescript
class PaymentProcessor {
  public processPayment(amount: number): boolean {
    // Logic to process payment
    return true;
  }
}

// Usage
const paymentProcessor = new PaymentProcessor();
paymentProcessor.processPayment(100);
```

**Coupling Example**

```typescript
interface PaymentGateway {
  process(amount: number): boolean;
}

class StripeGateway implements PaymentGateway {
  process(amount: number): boolean {
    // Logic to process payment with Stripe
    return true;
  }
}

class PaymentService {
  private gateway: PaymentGateway;

  constructor(gateway: PaymentGateway) {
    this.gateway = gateway;
  }

  public pay(amount: number): boolean {
    return this.gateway.process(amount);
  }
}

// Usage
const stripeGateway = new StripeGateway();
const paymentService = new PaymentService(stripeGateway);
paymentService.pay(100);
```
