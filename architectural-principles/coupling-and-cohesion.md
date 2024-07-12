# Coupling and Cohesion

**Coupling and Cohesion** are fundamental concepts in software engineering that describe how closely related and dependent software modules are, and how well the elements within a module belong together. Understanding and managing coupling and cohesion is crucial for creating maintainable, scalable, and robust software systems.

# Coupling

**Coupling** refers to the degree of direct knowledge that one module has about another. It measures how tightly interconnected different modules are within a system. The goal is to minimize coupling to reduce the ripple effect of changes and to increase modularity.

**Types of Coupling**

1. **Content Coupling**: One module directly modifies or relies on the internal workings of another module. This is the highest degree of coupling and should be avoided.

- Example: Module A changes the data inside Module B directly.

2. **Common Coupling**: Multiple modules share the same global data. Changes to this data affect all modules that access it.

- Example: Several modules modify a shared global variable.

3. **External Coupling**: Modules interact with external tools or hardware.

- Example: Modules that access a specific file format or a database.

4. **Control Coupling**: One module controls the behavior of another by passing control information (e.g., flags).

- Example: A module passes a control flag to another module to dictate its behavior.

5. **Stamp Coupling (Data-structured Coupling)**: Modules share a composite data structure, and use only part of it.

- Example: Passing an entire object to a function that only needs one attribute.

6. **Data Coupling**: Modules share data through parameters. This is the least severe form of coupling and is generally acceptable.

- Example: A function takes parameters and returns a result without side effects.

**Benefits of Low Coupling**

- **Maintainability**: Easier to update or modify one module without affecting others.
- **Reusability**: Modules can be reused in different systems with minimal changes.
- **Testability**: Easier to test modules independently.

# Cohesion

**Cohesion** refers to how closely related and focused the responsibilities of a single module are. High cohesion within a module is desirable as it means the module is focused on a single task or a group of related tasks.

**Types of Cohesion**

1. **Functional Cohesion**: All elements within the module contribute to a single well-defined task.

- Example: A module that handles all the operations related to user authentication.

2. **Sequential Cohesion**: Elements within a module are related by the sequence in which they are executed.

- Example: A module that processes data in a pipeline, where the output of one process is the input for the next.

3. **Communicational Cohesion**: Elements within a module operate on the same data or contribute to the same task.

- Example: A module that reads, updates, and displays a customer record.

4. **Procedural Cohesion**: Elements within a module are related by their control flow.

- Example: A module that performs a series of steps in a specific order.

5. **Temporal Cohesion**: Elements within a module are related by the timing of their execution.

- Example: Initialization functions that must be called during system startup.

6. **Logical Cohesion**: Elements within a module are related logically and are grouped together.

- Example: A module that contains various unrelated error handling routines.

7. **Coincidental Cohesion**: Elements within a module have no meaningful relationship. This is the lowest form of cohesion and should be avoided.

- Example: A utility module that contains a mix of unrelated functions.

**Benefits of High Cohesion**

- **Maintainability**: Easier to understand and modify a module that has a single responsibility.
- **Reusability**: Modules with a single, well-defined purpose are easier to reuse.
- **Robustness**: High cohesion reduces the likelihood of errors since related functionality is localized.

# Examples in TypeScript

**Example of Low Coupling**

```typescript
// Low Coupling Example
interface PaymentGateway {
  processPayment(amount: number): boolean;
}

class StripePaymentGateway implements PaymentGateway {
  processPayment(amount: number): boolean {
    console.log(`Processing payment of ${amount} via Stripe.`);
    return true;
  }
}

class OrderService {
  private paymentGateway: PaymentGateway;

  constructor(paymentGateway: PaymentGateway) {
    this.paymentGateway = paymentGateway;
  }

  placeOrder(amount: number): void {
    if (this.paymentGateway.processPayment(amount)) {
      console.log("Order placed successfully.");
    } else {
      console.log("Order failed.");
    }
  }
}

const paymentGateway = new StripePaymentGateway();
const orderService = new OrderService(paymentGateway);
orderService.placeOrder(100);
```

**Example of High Cohesion**

```typescript
// High Cohesion Example
class UserAuthenticator {
  private users = [
    { username: "user1", password: "pass1" },
    { username: "user2", password: "pass2" },
  ];

  authenticate(username: string, password: string): boolean {
    const user = this.users.find(
      (user) => user.username === username && user.password === password
    );
    return !!user;
  }
}

class UserProfile {
  getUserProfile(username: string): string {
    return `Profile of ${username}`;
  }
}

class AuthenticationService {
  private authenticator = new UserAuthenticator();
  private userProfile = new UserProfile();

  login(username: string, password: string): string {
    if (this.authenticator.authenticate(username, password)) {
      return this.userProfile.getUserProfile(username);
    } else {
      return "Authentication failed.";
    }
  }
}

const authService = new AuthenticationService();
console.log(authService.login("user1", "pass1")); // Output: Profile of user1
console.log(authService.login("user1", "wrongpass")); // Output: Authentication failed.
```

# Real-Life Analogy

**Coupling**: Think of coupling as the extent to which different departments in a company depend on each other to perform their tasks. If the marketing department cannot function without constant input from the engineering department (high coupling), then any changes in engineering processes can significantly disrupt marketing.

**Cohesion**: Think of cohesion as the degree to which tasks within a single department are related. A highly cohesive marketing department focuses solely on marketing activities (advertising, market research, etc.), making it more efficient and easier to manage.

# Summary

Coupling and cohesion are critical concepts in software design that impact the modularity, maintainability, and overall quality of software systems. By striving for low coupling and high cohesion, developers can create systems that are easier to maintain, understand, and extend.
